---
title: "Fuzzy File Finding (and warm fuzzy feelings)"
date: 2019-01-24T21:05:03+01:00
author: "Jens-Christian Fischer"
description: "fzf - fuzzy find on the command line"
image: ""
categories: ["musings"]
tags: ["zsh", "cli", "find"]
language: en
slug:
type: post
---
While my day job is managing a team of 8 engineers (which means a lot of meetings), I do get to 
work with the CLI from time to time. As you might know, working on the CLI means navigating
deep dirctory structures and working with millions of files. It doesn't matter if you 
are into operations or into development, working with directories and files are going to be your bread and
butter operations.

For development work, I tend to use on the of the [JetBrains](https://jetbrains.com) IDEs (RubyMine, PyCharm)
because I like how the IDEs support you while developping. One of their lovely features is the fuzzy finder
when opening files. You start typing letters and the IDE will filter down the files by the letters you typed
as they appear in the path or the filename. So typing `ser/crop` would select the file `rails/app/services/openstack/create_openstack_project.rb`

{{< figure src="rubymine.png" alt="Rubymine Example" caption="Selecting files in RubyMine">}}

Today, I happend upon the article [Simple Note-Taking with fzf and Vim](https://medium.com/adorableio/simple-note-taking-with-fzf-and-vim-2a647a39cfa) 
that introduced me to [fzf](https://github.com/junegunn/fzf), the _Fuzzy File Finder_. Installation (on OS X) is a 
`brew install fzf` away. When you run `fzf` it will by default start to show all files in the current directory and by typing, it will
start to filter down the list. Press `Return` to copy and paste the selected file on the command line. You can also pipe in content to `fzf` 
making it handy to filter down long lists of data.

There are a few shortcuts that make life easier: `CTRL-T` can be used to invoke `fzf` after having started a command (like `vi`) 
to select a filename:

{{< figure src="fzf-shell.png" alt="shell example" caption="Selecting files to edit with the 'CTRL-T' shortcut" >}}

`CTRL-R` allows you to select command from the shells history.

I am using [Oh My ZSH](https://github.com/robbyrussell/oh-my-zsh) to configure `zsh` and it ships with a plugin for `fzf`. I just had to
add the `FZF_BASE` variable and `fzf` to the plugins line in `~/.zshrc`:

{{< highlight "bash" >}}
export FZF_BASE=/usr/local/bin/fzf

plugins=(git pyenv osx fzf)
{{< /highlight >}} 

I also had to set my zsh to `emacs` mode (I was using `vi` mode, which is non-default) by deleting the line `bindkey -v` in the `.zshrc` file 
to make the `CTRL-T` and `CTRL-R` shortcuts work. (I rarely edit my command line entries, and I always got confused by it being in `vi` mode
so no big loss there.

`fzf` comes with plenty of [usage examples in the fzf wiki](https://github.com/junegunn/fzf/wiki/examples) which I will explore over time.

Another post, [How FZF and ripgrep improved my workflow](https://medium.com/@sidneyliebrand/how-fzf-and-ripgrep-improved-my-workflow-61c7ca212861) 
has even more tips and tricks on how to use it.


