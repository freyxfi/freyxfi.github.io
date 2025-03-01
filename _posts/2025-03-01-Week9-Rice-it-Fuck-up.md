---
title: "Week #9 Rice it Fuck up"
date: 2025-03-01 19:24:00 +0800
categories: [Ricing]
tags: [vim, Programming]
image:
  path: https://i.pinimg.com/originals/13/66/a2/1366a245bb4f728bc59cafac97b5aa0a.gif
---

# Another Note

I failed and then I started again as I know this is a part of life, not the ending.  
Btw, in this blog, I will show how I riced up my Vim from the ordinary to the nerdy cool one. As other blogs were all about what I am doing, this will be about giving something to the community. Despite web security or Active Directory, can we talk about computers for once?

# What Happened Last Week?

- I spent most of the time trying to understand logic bugs.
- Still struggling to understand logic bugs.
- Need to create a mind map.
- Stopped showing off to the wild.
- Keeping in the work.
- I have a lot of company work.
- Recently joined some cool communities and thinking about helping them.
- My daily streak got broken as I got injured + fever.

But now the fun begins!  

# Rice up your Vim

## **What is Vim Ricing?**

Ricing refers to customizing a system or tool to improve its visual aesthetics and user experience. For Vim, this involves adding plugins, themes, fonts, and configuration tweaks to make it both powerful and beautiful. While Vim is known for being fast and minimalist, you can rice it up without sacrificing performance.

![vim](https://pbs.twimg.com/media/Gk9RhYJWQAA5snb?format=jpg&name=medium)

## **Basic Vim Configurations**

### **Syntax Highlighting**
```vim
syntax on
```
- **Why?** Enables syntax highlighting for better readability by coloring code according to its type (keywords, strings, comments).

### **Line Numbers**
```vim
set number
set relativenumber
```
- **Why?** Shows both absolute and relative line numbers, making it easier to navigate the code.

### **Cursor Line Highlighting**
```vim
set cursorline
```
- **Why?** Highlights the current line your cursor is on, which helps you stay focused in larger files.

## **Installing Plugins with Vim-Plug**

### **Installing Vim-Plug**
First, install Vim-Plug using the following command:
```bash
curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
       https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```

### **Using Vim-Plug in `.vimrc`**
```vim
call plug#begin('~/.vim/plugged')
Plug 'morhetz/gruvbox'
Plug 'vim-airline/vim-airline'
Plug 'vim-airline/vim-airline-themes'
Plug 'preservim/nerdtree'
Plug 'ryanoasis/vim-devicons'
Plug 'tiagofumo/vim-nerdtree-syntax-highlight'
call plug#end()
```
To install the plugins, open Vim and run `:PlugInstall`.

## **Setting Up a Colorscheme**

### **Adding Gruvbox to `.vimrc`**
```vim
set background=dark
colorscheme gruvbox
```
- **Why?** Gruvbox provides a dark, contrast-rich colorscheme that’s easy on the eyes and well-loved by developers.

## **Adding a Modern Status Line (Vim-Airline)**

### **Vim-Airline in `.vimrc`**
```vim
let g:airline_theme='gruvbox'
let g:airline_powerline_fonts=1
```
- **Why?** This status line is more informative, shows the current mode, file type, cursor position, and integrates well with Gruvbox.

## **File Management with NERDTree**

### **NERDTree Setup**
In your `.vimrc`, add:
```vim
map <C-n> :NERDTreeToggle<CR>
```
- **Why?** Allows you to toggle NERDTree with `Ctrl + n`, providing a convenient way to manage files directly inside Vim.

## **Enabling Icons with Nerd Fonts**

### **Install Nerd Fonts**
```bash
cd ~/.local/share/fonts
wget https://github.com/ryanoasis/nerd-fonts/releases/latest/download/Hack.zip
unzip Hack.zip -d HackNerdFont
fc-cache -fv
```
- **Why?** Nerd Fonts provide special symbols and icons that enhance the visual aspect of NERDTree.

After installing, set your terminal font to **Hack Nerd Font** (or another Nerd Font of your choice) in your terminal preferences.

## **Performance Tweaks**

### **Smooth Scrolling and Redraw**
```vim
set scrolloff=8
set sidescrolloff=8
set lazyredraw
set ttyfast
set updatetime=100
```
- **What it does?** Ensures smoother scrolling and reduces any potential screen redraw lags when moving around in files.

## **Conclusion**

Ricing Vim is not just about making it look beautiful — it’s about creating a productive and pleasant environment to work in. By leveraging plugins, colorschemes, and performance tweaks, you can turn a simple text editor into a fully customized powerhouse.

Take your time, experiment with different themes and plugins, and find what works best for your workflow.

## **What’s Next?**
In future blogs, I'll dive into more advanced Vim customizations, including key mappings, plugin development, and integrating Vim with version control systems like Git.

