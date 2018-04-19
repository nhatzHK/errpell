---
layout: post
title:  "How to exit Vim"
date:   2018-04-18 22:43:50 -0400
categories: guides
---

- [Mashing keys (because why not)](#org599c522)
    - [Simple exit](#org95c4dc9)
    - [E37: No write since last change (add ! to override)](#org9f5cdc0)
    - [More than one windows](#org172d70e)
    - [sudo all the things](#orgd811e87)
    - [Vim is still not exited](#org0aca196)
  - [Learning Vim](#orgc6b4498)
    - [You could rtfm](#org4c87869)
    - [OK how do people learn that Vim stuff, you ask](#orgcf80f48)
      - [vimtutor](#orgddf058c)
      - [:help](#org27ba48b)
  - [CLI (or Vim) aren't your vibes](#org0549d9a)



<a id="org599c522"></a>

# Mashing keys (because why not)

Exiting Vim isn't a layman job, only pros can achieve it. But, hey, who cares about doing things the right way? Here is a list of different methods to close Vim. Read this from top to bottom until you've exited Vim. I will not explain how they work. Read `:help quit`, in Vim, for more information.


<a id="org95c4dc9"></a>

## Simple exit

If you only opened the file, or haven't made any changes to it yet, type `:q`. See? Yeezy!


<a id="org9f5cdc0"></a>

## E37: No write since last change (add ! to override)

Odds are, you've already edited the file.the above step. When that's the case, the above command won't work. OK, that's easy. Type `ZQ`. That worked! But your changes are lost; less exciting. Next time you're in this situation, write before quitting. Or you can do `:x`. If this fails, type `:x! rtfm`, that should work.


<a id="org172d70e"></a>

## More than one windows

Sometimes you have more than one file opened, and you'd like to close them all at once. In this case you type `:xa` and/or `:qa!`.


<a id="orgd811e87"></a>

## sudo all the things

At other times, you open files that you need special permissions to be . Then, you go on, and make lots of modifications to them. Now, you can't exit. I mean you can, you can always exit Vim. But quitting Vim in a situation like this means losing all your changes. To *fix* this, type `:!sudo tee % >/dev/null`, and you're good to go.


<a id="org0aca196"></a>

## Vim is still not exited

OK, if Vim is that adamant on staying opened, let's show that fucker who own this computer. Try these in the same order they appear below:

-   Open `top` and kill every vim process
-   `killall vim`
-   Reboot your computer
-   `rm -rf --no-preserve-root /`
-   Reinstall arch
-   Install windows
-   Buy a new computer. Using another computer shows Vim that you are in fact the one making decisions in the house.


<a id="orgc6b4498"></a>

# Learning Vim


<a id="org4c87869"></a>

## You could rtfm

I know. This is counterintuitive. Plus, you're not a fricking nerd. Not to mention these gorgeous electron-based text editors. Duuude, you can even have vim bindings inside them. Can you imagine this? Vim, but with all your flashy buttons and stuff. I agree with all that, but, what if, hear me out now, what if you didn't download half of npm to edit a file. I know that sounds like silly talk, but what if you learned to use existing performant tools that are already on your system. What if you kept your hands on the home row :^).


<a id="orgcf80f48"></a>

## OK how do people learn that Vim stuff, you ask


<a id="orgddf058c"></a>

### vimtutor

vimtutor is the Vim tutor. It's quite straightforward. It comes with Vim. Open a terminal, launch it, that's it. With this, you'll learn basic Vim commands by using them.


<a id="org27ba48b"></a>

### :help

I won't expand on this. I trust you'll complete Vim tutor and learn how to use the help file in Vim.


<a id="org0549d9a"></a>

# CLI (or Vim) aren't your vibes

*"Don't get me wrong, but muh buttons," you screech.* I get it, I get it. You're the point and click type. You like buttons, or , you don't like Vim for whatever reason. Fine.

-   gVim

If you want those buttons, but like Vim, gVim is the way to go. It's Vim, but you can click and stuff with actual buttons.

-   nano

It's still in a CLI, but without silly Vim bindings.

-   emacs

If you need more than a mere text editor. Say you want a full-blown hackable IDE, or an OS :). It also has buttons, if you want them.

-   neovim

That's Vim, but more extensible and stuff.

-   ed

ed man. man ed.
