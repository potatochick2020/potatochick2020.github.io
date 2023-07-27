---
layout: post
title: "Notes on my dev environment set up, try to mark down everything I did to set up my dev environemt"
tags: [ "Development","Environemnt", "English", "Notes" ]
categories: ["Environment","Dev environment","Software","Ide"]
toc: true
---

# Background
Setting up my nvim config recently, and decide to jot down some notes related. Not gonna mentioned every thing from hjkl navigation, but more like what mistake I made, and how to make stuff easier.

# Potential Issues
## Get the most update version
The version in debian-based apt repository (The version you installed with sudo apt-get install) is v0.6.1 which as at 2023 July, the most update version is v0.9.1 for stable release.

## Case Sensitive File System
Windows and Mac are Case - Insensitive file system by default, and Linux are Case - Sensitive, it might leads to some issues

## Search where will be your path 
In nvim normal mode type `:help vimrc-intro`

It state the 2 default file path
- ~/.config/nvim/init.vim         (Unix and OSX) 
- ~/AppData/Local/nvim/init.vim   (Windows) 
# Live an easier life
## Put everything on git

use `git clone <your configuration> ~/.config/nvim ` , this will help a lot if you own multiple dev set up. 
 
## markdown a dependency list if needed
e.g. [Telescope.nvim](https://github.com/nvim-telescope/telescope.nvim) need [ripgrep0(https://github.com/BurntSushi/ripgrep) as a dependencies, to use [Packer.nvim](https://github.com/wbthomason/packer.nvim) to manage the package, you need to install it first.

## Keep a good file structure in .../nvim

I try to seperate each plugin to its own file, so when I messed something up by installing new plugin, I could quickly remove it and fix my setting.

![init.vim](/assets/img/dev-environment/software/nvim/Initvim.PNG)
