---
layout: post
title: "Notes on my dev environment set up, try to mark down everything I did to set up my dev environemt"
tags: [ "Computer","Environemnt", "English" ]
categories: ["Environment","Dev environment"]
toc: true
---
# Background
As I had rebuild my PC recently, I need to reset my dev-environment on that machine, and therefore write a blog to jot down my configuraion of nvim. 

This blog will be focusing on setting up the basic environment and keybinding. The next blog will be focus on setting up LSP/ syntax/ source code related features.

//TODO: Add Photo of nvim set up 

# Command which help during set up 
 ```vimscript
 :map <C-H> -- Command to check what key does Ctrl-H map to in Normal mode
 :map! <C-H> -- Command to check what key does Ctrl-H map to in Insert mode
 ```

# After configuration
## Command that I map to
- F5 : Open NvimTree (file explorer)
- F6 : Open UndoTree (All previous changes)
- F4 : markdown preview , use q to quit
- C-Q/C-E : previous/next buffer (looks like tab in vs code)
- <SPACE>ff/fg/fc/fd : 4 commands of telescope
- A-HJKL : navigate between windows (NvimTree count as a window)

## Some Setting
Auto-Session

Eventhough I used the Auto-Session plugin and MiniSession for Mini.nvim (comes along with the MiniStarter), I did not enable auto create new session, it only save the session if the session exited already. 

:SessionSave to save the Session

# Methodology? Behind every setting
Try to reduce the disturbance caused by GUI/ Message pop up/ use of mouse to keyboard. At the same time try to keep things as simple as possible. Most set up/ configuration are some how perfect but at the same time too bulky or with a lot of extra features probably you do not even realize there is a features like that.

# Important Setting
There is a simple configuration which can squeeze a lot of time for you in the future. Which is reducint the *Key Repeat TIme* as much as possible.

//TODO: Add photo in Ubuntu/Window/Mac

# IDE
To be honest, in most of the time I just need a text editor. Someone would like an IDE, pressing "A fancy collection of button or keys" then some code will magically spawn. I dont against this, just not my style.

I did tried JetBrain family, They are quite nice, especially the IntelliJ and Clion. With some extension like IdeaVim, There are quite a large fans base in their products as they have strong features. 

I still remember a quote that my friends once told me "Learn IntelliJ Before Java"

I personally prefer something more extensible and customizable. Vscode/ nvim. Vscode have quite a lot of plugin and they exist in every platform as it is built with electron Js. I got it installed on all of my machine, and now I am using nvim with few plugin/ setting that I will share in the following. 

I tried spacemacs/ spacevim/ lazyvim. Basically vim/ emacs with a lot of configuration given, but I found these quite bulky. And Eventhough it is beginner friendly as you dont need to use any time to set up your own configuration. As a beginner, you usually do not know how to fine tune your own vim/emacs. If in this case, why dont u go to intelliJ product with the idea Vim extension. 

# Vim 
## neo-vim plugin/setting
There is one very importent plugin that I think everyone should install.
Which is a file tree plugin.

I have also set up some features in my init.vim

- Hybrid line number display
- Using ctrl + hjkl in navigation during insert mode 

# Terminal
I am not really a Windows fans but I need to use it in my work. Funny enough I could access all website e.g reddit, instagram, facebook, youtube in the network. But it has block windows update which leads to not being able to install WSL.

In the current company, there are not any needs to run program locally, just simply ssh to the server and runs build. 

I am using [Windows terminal]() in Windows + powershell,

I use + zsh in Linux and mac

# Coding Time timer 
I use Wakatime Calculate the time I use to code.

# Map key

Windows powershell
oh my posh
posh git?

neovim
share profile

vimplug

# LSP


# Things I am still learning/ I wish to implement 
## Use [i3-wm - i3 Window Manger]() as window manager
I did try to use eaf - emacs application framework before, which there are pdf viewer, browser, even music listener live within eaf, so basically you could use emacs as your "Operating System" some how. However, I just feel it will be easier for me to use

## Jump navigation
I wish to set up a jump navigation to view source code of the library, such as jumping to source code of STL/JDK when I use some function such as std::unordered_map in C++ or Date1.compareTo(Date2) in Java.
