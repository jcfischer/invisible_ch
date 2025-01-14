---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2005-01-15 16:45:39+00:00
layout: post
link: https://invisible.ch/2005/01/15/markov-chains-in-ruby/
slug: markov-chains-in-ruby
tags: ["blog"]
title: Markov Chains in Ruby
type: post
wordpress_id: 361
---

Writing text and playing with text is all good fun. Using [Markov Chains][1] one can generate text that is almost readable, almost understandable, but not quite. Markov Chains analyses the frequency of words in relation to another. 

Analysing text basically means counting which words follow each other. Producing text is done by picking a word and then looking up which word has come up after that in the text samples, picking one and then using this new word as the basis for determining the next one.

For a [game project][2] we are working on, I need this functionality. Because Amuda is written in [Ruby][3] using [Ruby On Rails][4] as it's MVC framework, I also wanted to do the Markov Chains in Ruby. Because there don't seem to be any Ruby implementation, I ported [Gary Burds Markov Chain Generator][5]. For those interested, read on to see the code -- and if any Ruby-Gurus are out there, please help me improve my "Ruby-Fu", I'm still a beginner in this language.

[1]: https://en.wikipedia.org/wiki/Markov_chain
[2]: https://www.amuda.ch
[3]: https://www.ruby-lang.org
[4]: https://www.rubyonrails.org
[5]: https://gary.burd.info/2003/11/markov-chain-generator.html
<!-- more -->
Here we go

        #  Markov Chain Generator
        # based on the Python version by Gary Burd: https://gary.burd.info/2003/11/markov-chain-generator.html
        # Released into the public domain, please keep this notice intact
        # (c) InVisible GmbH    
        # https://www.invisible.ch
        # 

    require "YAML"

    class Array
      # return a random element of the array, similar to random.choice in python
      def choice
        self[ rand(self.size) ]
      end
    end

    class MarkovTool

      attr_accessor :markov_data
    
      def initialize( markov_data = nil )
        # use an unlikely combination for end of paragraph marker
        @nlnl = "#-#-"
        @markov_data = markov_data if markov_data.class == Hash
        @markov_data ||= Hash.new
      end
    
      def new_key( key, word)
        return @nlnl if word == "\n" 
        return key if !word
        return word
      end
    
    
      def markov_data_from_words( words )
        key = @nlnl
        words.each do | word |
          @markov_data[ key ] ||= Array.new
          @markov_data[ key ] << word
          key = new_key( key, word )
        end
      end
    
      def words_from_markov_data
        key = @nlnl
        result = Array.new
        word = ""
        # repeat until we hit a newline or a full-stop, remove the last clause to get     paragraphs, 
        while word && word != "\n" && word[-1] != "."[0]
          word = @markov_data[ key ].choice rescue nil
          key = new_key( key, word )
          result << word
        end
        result
      end
    
      # analyze and add a string
      def words_from_string( line )
        result = Array.new
        words = line.split
        if words.size > 0
          words.each { | word | result << word }
        else
          result << "\n"
        end
        result
      end
  
      # analyze and add a file
      def words_from_file( f )
        result = Array.new
        File.foreach( f ) do | line |
          result << self.words_from_string( line )
        end
        result.flatten
      end
    
      # build a paragraphs out of the result array
      def paragraph_from_words( words )
        result = Array.new
        words.each do | word |
          result << word
        end
        result.join( " " )
      end

      # return a complete paragraph
      def get_paragraph
        wo = self.words_from_markov_data
    
        self.paragraph_from_words( wo )
      end

      def store_in_yaml( f )
        YAML.dump( @markov_data, f )
      end

      def load_from_yaml( f )
        @markov_data = YAML.load( f )
      end

    end

    if __FILE__ == $0 then

      m = MarkovTool.new
  
      # read exisiting markov data
      # File.open( "markov.yaml" ) { | yf | m.load_from_yaml( yf ) }

      if ARGV[0]
        # if we got a filename, read it, process it and store the markov data
        w = m.words_from_file( ARGV[0] )
        m.markov_data_from_words( w )
        File.open( "markov.yaml", "w" ) { | yf | m.store_in_yaml( yf ) }
      end
      # create a paragraph and display it
      p = m.get_paragraph
      puts p
    end
