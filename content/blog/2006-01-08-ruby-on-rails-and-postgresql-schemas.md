---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2006-01-08 09:11:51+00:00
layout: post
link: https://invisible.ch/2006/01/08/ruby-on-rails-and-postgresql-schemas/
slug: ruby-on-rails-and-postgresql-schemas
tags: ["blog"]
title: Ruby on Rails and PostgreSQL Schemas
type: post
wordpress_id: 500
---

I'm working on a Rails application on a Postgres DB Server. Our client has decided to change the database so that it uses db-schemas in order to simplify administration of rights on the database. However, he has also introduced tables with identical names in different schemas.

Our rails application was already fairly well underway, so there were some substantial changes to be made. Here's what I've learned in the process:

### Models ###
Changing the models is the easy part: I just added a *set_table_name* call to each model:

    class SomeModel < ActiveRecord::Base
        set_table_name 'schema.some_models'
    end

That leads us to the 

### Tests ###

Now it starts to get ugly: In general, the unit and functional tests use *fixtures :some_models* to load the fixtures. However, the code that actually loads the fixtures is completely unaware of the *set_table_name* call in the model and assumes that the :some_models symbol represents the table name. Of course you can't use a symbol like :schema.some_models because dots have no place in a symbol.

I then patched line 240 in activerecord/lib/activerecord/fixtures.rb to read:

      def self.create_fixtures(fixtures_directory, *table_names)
          table_names = table_names.flatten.map { |n| n.to_s.gsub(/__/, '.') }
    
that allowed me to specify my fixtures like this:

      fixtures :schema__some_models

where the double underscore would be replaced by a dot.

However, still not enough, because now PostgreSQL was acting up on the dropping and creating of the test database. I got the following error: *createdb: database creation failed: ERROR:  source database "template1" is being accessed by other users*

Googling around, it seems that one should use "template0" instead of "template1" when using *createdb* to create a new database in Postgres. In typical "So I'll remove the cause. But not the symptom" fashion, I found "vendor/rails/railities/lib/task/databases.rake" and changed line 109 to read:

    `createdb #{enc_option} -U "#{abcs["test"]["username"]}" -T template0 #{abcs["test"]["database"]}`
 
Now, the test database is being created. Hints on how to fix this for good appreciated!

### Preloading of fixtures ###

Therefore, I decided to use preloaded fixtures. The following change in *test/test_helper.rb* enables this:

         self.pre_loaded_fixtures = true

Then I created a file that will change the way, Rake works: *lib/tasks/000_change_rake.rake*

    # Rake allows the same task name to be specified multiple times, where 
    # each successive task definition appends to a list of actions to 
    # perform. Therefore, an application specific task cannot redefine a 
    # previously defined task. These methods here allow tasks to be 
    # redefined and renamed. 

    module Rake 
        class Task 

            # Clear all existing actions for the given task and then set the 
            # action for the task to the given block. 
            def self.redefine_task(args, &block) 
                task_name, deps = resolve_args(args) 
                TASKS.delete(task_name.to_s) 
                define_task(args, &block) 
            end 
        
            def remove_prerequisite(task_name) 
                name = task_name.to_s 
                @prerequisites.delete(name) 
            end
        
            def add_prerequisite(task_name)
                name = task_name.to_s
                @prerequisites.add(name)
            end
        end 
    end 
    
    # Clear all existing actions for the given task and then set the 
    # action for the task to the given block. 
    def redefine_task(args, &block) 
        Rake::Task.redefine_task(args, &block) 
    end 
    
    # Alias one task name to another task name. This let's a following 
    # task rename the original task and still depend upon it. 
    def alias_task(new_name, old_name) 
        Rake::Task::TASKS[new_name.to_s] = 
        Rake::Task::TASKS.delete(old_name.to_s) 
    end 

This is based on code by Peter Fitzgibbons and comes from the Rails Mailing list. Having this in place, I can do the following in *lib/tasks/my_tests.rake*

    
    desc "Load fixtures data into the development database"
    task :load_fixtures_to_test => :environment do
        ActiveRecord::Base.establish_connection(:test)
        require 'active_record/fixtures'
        Fixtures.create_fixtures("test/fixtures", ActiveRecord::Base.configurations["all_fixtures_load_order"])
        puts "Loaded these fixtures: " + ActiveRecord::Base.configurations["all_fixtures_load_order"].collect { |f| f.to_s }.join(', ')
    end

    Rake::Task.lookup(:test_units).add_prerequisite(:load_fixtures_to_test) 
    Rake::Task.lookup(:test_functionals).add_prerequisite(:load_fixtures_to_test) 
    Rake::Task.lookup(:recent).add_prerequisite(:load_fixtures_to_test) 

To define, what fixtures to load (and important if you have foreign key constraints in what order, expand your *database.yml* file with the following information:

    all_fixtures_load_order:
      - :schema1__models
      - :schema2__models
      - :schema2__other_models


Now the fixtures are loaded (in the correct order) to the test database before the tests are run.

### Fixtures ###

However, in my case, the database has a lot of foreign key constraints defined. Most of the data is already in the database, filled by automatic processes. So just generating a couple of test-fixtures was quite difficult, because there were chains of constraints. Plugins to the rescue! The [ar_fixture][1] expands all models to include methods that allow dumping the contents of a table to a YAML file.

So a quick
 
    ruby script/runner "SomeModel.to_fixture"

dumps that table to a yml file. All nice and dandy unless you happen to have 1.5 million rows in a table.... I patched the *to_fixture* method thusly:

    # Write a file that can be loaded with fixture :some_table in tests.
    def self.to_fixture(limit = 0)
      write_file(File.expand_path("test/fixtures/#{table_name}.yml", RAILS_ROOT), 
          self.find(:all, :limit => limit).inject({}) { |hsh, record| 
              hsh.merge("record_#{record.id}" => record.attributes) 
            }.to_yaml)
    end

to allow for 

    ruby script/runner "SomeModel.to_fixture(100)"

to only export the first 100 rows of the database.

### Testing ###


Running the tests reveals some more problems:

    24) Error:
    test_truth(VulnerabilityTest):
    NoMethodError: undefined method `models' for #
      /Users/jcf/dev/log-schema/vendor/rails/actionpack/lib/action_controller/test_process.rb:377:in `method_missing'
      ./test/unit/model_test.rb:7:in `test_truth'

This is caused by the *models(:first)* call in test_truth. I just stripped those and use *Model.find(1)* instead.

### Finishing ###

This "small change" in the db schema took me more than two days to rectify in the rails application. So yes, Rails is an environment, that makes you incredible productive. But when you run into legacy databases (or databases that don't quite follow the way Rails thinks they should be) be prepared to spend some time on beating rails into submission :-)


[1]: https://nubyonrails.topfunky.com/articles/2005/12/27/dump-or-slurp-yaml-reference-data


Technorati Tags: [development](https://www.technorati.com/tag/development), [postgresql](https://www.technorati.com/tag/postgresql), [rubyonrails](https://www.technorati.com/tag/rubyonrails)
