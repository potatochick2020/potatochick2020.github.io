---
layout: post
title: "Nvim: common action/movement"
tags: [ "Development","Environemnt", "English", "Notes" ]
categories: ["Environment","Dev environment","Software","Ide"]
toc: true
---

# Background
After some set up of vim I want to mark down some common action that I used within my Nvim.

# Actions
## Delete
### Command to delete all lines include string "potatochick2020"
```vim
:g/potatochick2020/d
```

### Command to delete all lines not include string "potatochick2020"
```vim
:g!/potatochick2020/d
```
> The logic behind bellow delete command is delete until cursor , so `$` in normal mode mean move cursor to end of line, `d$` mean delete until end of line 
{: .prompt-info }
### Delete until end of line in normal mode
```vim
d$
```

### Delete until start of line in normal mode
### Delete until end of Document
```vim
dG
```

### Delete until start of Document
```vim
dgg
```

## Motion 
### go to line x , e.g. 1
```vim
:1
```

### Hop.nvim
Basically I could go to anywhere of my screen with few click, I type `:HopChar1` for demonstration purpose. In my use case, I had map it to <Leader>-J , which my leader key is space key.

![hop.nvim-demo](/assets/img/dev-environment/software/nvim/hopnvim-demo.gif)

with Hop.nvim, I could do to perform delete until destination. 
```vim
d
:HopChar1
first char for search
second char for jump
```

