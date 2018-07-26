---
layout: post
title: "How to exit Vim"
category: guide
tags: programming
---

Quit vim one way or another.

First published [here](https://programming.im/guides/7) on July 8, 2018.
<!--more-->

- [Mashing keys (because why not)](#mashing-keys-because-why-not)
  - [Simple exit](#simple-exit)
  - [E37: No write since last change (add ! to override)](#e37-no-write-since-last-change-add-to-override)
  - [More than one window](#more-than-one-window)
  - [sudo all the things](#sudo-all-the-things)
  - [Vim is still not exited](#vim-is-still-not-exited)
- [Learning Vim](#learning-vim)
  - [You could rtfm](#you-could-rtfm)
  - [OK how do people learn that Vim stuff, you ask](#ok-how-do-people-learn-that-vim-stuff-you-ask)
    - [vimtutor](#vimtutor)
    - [:help](#help)
- [CLI (or Vim) aren't your vibes](#cli-or-vim-arent-your-vibes)



# Mashing keys (because why not)

Exiting Vim isn't the layman's job; only pros can achieve it. But, hey, who cares about doing things the right way? Here is a list of different methods for closing Vim. Read this from top to bottom until you've exited Vim. I will not explain how they work. Read `:help quit` in Vim for more information.


## Simple exit

If you have only opened the file, or haven't made any changes to it yet, type `:q`. See? Yeezy!


## E37: No write since last change (add ! to override)

Odds are, you've already edited the file, nullifying the effectivity of the above step. When this is the case, the above command won't work. OK, that's easy to work around. Type `ZQ`. That worked! But you lost your changes; less exciting. Next time you're in this situation, write before quitting. Or, you can do `:x`. If this fails, type `:x! rtfm`, that should work.


## More than one window

Sometimes you have more than one file opened, and you'd like to close them all at once. In this case you type `:xa` and/or `:qa!`.


## sudo all the things

At other times, you open files that you need special permissions to write to. Then you go on and make lots of modifications to them. Now, you can't exit. I mean you can, you can always exit Vim, but quitting Vim in a situation like this means losing all your changes. To *fix* this, type `:!sudo tee % >/dev/null`, and you're good to go.


## Vim is still not exited

OK, if Vim is that adamant on staying opened, let's show that fucker who owns this computer. Try these in the order they appear below:

-   Open `top` and kill every vim process
-   `killall vim`
-   Reboot your computer
-   `rm -rf --no-preserve-root /`
-   Reinstall arch
-   Install windows
-   Buy a new computer. Using another computer shows Vim that you are in fact the one making decisions in the house.


# Learning Vim


## You could rtfm

I know, this is counterintuitive. Plus, you're not a fricking nerd. Not to mention the existence of these gorgeous electron-based text editors. Duuude, you can even have vim bindings inside them. Can you imagine this? Vim, but with all your flashy buttons and stuff. I agree with all that, but, what if you didn't download half of npm to edit a file? I know this sounds like silly talk, but hear me out. What if you learned to use tools that are already on your system and perform well? What if you kept your hands on the home row :^)?


## OK how do people learn that Vim stuff, you ask


### vimtutor

vimtutor is the Vim tutor. It's quite straightforward. It comes with Vim. Open a terminal, launch it, that's it. With this, you'll learn basic Vim commands by using them.


### :help

I won't expand on this. I trust you'll complete Vim tutor and learn how to use the help file in Vim.


# CLI (or Vim) aren't your vibes

*"Don't get me wrong, but muh buttons," you screech.* I get it, I get it. You're the point and click type. You like buttons or you don't like Vim for whatever reason. Fine.

-   gVim

If you want those buttons but like Vim, gVim is the way to go. It's Vim, but you can click and stuff with actual buttons.

-   nano

It's still in a CLI, but without silly Vim bindings.

-   emacs

If you need more than a mere text editor. Say you want a full-blown hackable IDE, or an OS :). It also has buttons, if you want them.

-   neovim

This is Vim, but made by another developer with a new and clean codebase. It has a python api and cool exclusive plugins. It also maintains backwards compatibility with vim plugins.

-   ed

 ed man. man ed.
