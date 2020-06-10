---
title: "Using VimWiki and git to manage notes"
date: 2020-06-10T10:37:05+02:00
tags:
  - vim
  - git
draft: false
---

This post explains how I manage my notes with VimWiki and a git repository.

# VimWiki Installation

The only requirement on the system that you want to use VimWiki on is that vim is installed. For VimWiki to work, the following code must be added to your vimrc. First, the following settings must be added to you `.vimrc` file so VimWiki will work properly.

```vim
set nocompatible
filetype plugin on
syntax on
```

Now you must install the VimWiki vim plugin, in this example I use Vim Plug. More information about Vim Plug can be found [here](https://github.com/junegunn/vim-plug).

```vim
call plug#begin('~/.vim/plugged')
  Plug 'vimwiki/vimwiki'
call plug#end()
```

To install the specified plugins, run the following vim command: `:PlugInstall`

After the installation of the required plugin, VimWiki can be configured. The only configuration that I am using is the location of the VimWiki files. To set the path, add the following configuration to your `.vimrc`.

```vim
let g:vimwiki_list = [{
  \ 'path': '~/vimwiki/',
  \ }]
``` 

I use the VimWiki syntax. With the VimWiki syntax, it is possible to use the build-in HTML converter. If you want to use Markdown for your VimWiki files, add te following code to your `.vimrc`.

```vim
let g:vimwiki_list = [{
  \ 'path': '~/vimwiki/',
  \ 'syntax': 'markdown',
  \ 'ext': '.md'
  \ }]
```

To see my `.vimrc` file, you can check my GitHub repository [maartenbeeckmans/dotfiles](https://github.com/maartenbeeckmans/dotfiles].

For convenience, I have added an alias to my `.zshrc` to open my VimWiki index.

```bash
alias vimwiki="vim -c VimwikiIndex"
```

# Setting up Git repository

To manage VimWiki in a git repository. First create an empty git repository on GitHub or Gitlab. When te repository is created, go to your VimWiki folder and run the following commands:

```bash
git init
git add .
git commit -m "initial commit"
git remote add origin git@github.com:<git username>/<repo name>.git
git push -u origin master
```

# VimWiki syntax overview

```wiki
= Header1 =
== Header2 ==
=== Header3 ===


*bold* -- bold text
_italic_ -- italic text

[[wiki link]] -- wiki link
[[wiki link|description]] -- wiki link with description

* bullet list item
  - bullet list item
```

> For more syntax elements, see `:h vimwiki-syntax`

# Using VimWiki

To launch VimWiki run the command `vimwiki` (if you did set the alias).

Write your notes in the vimwiki syntax as described above.

To create a link, press `<Enter>` when on a word, to return to the parent document, press `<Backspace>`.

For creating the HTML documents, run the vim command `:VimwikiAll2HTML`.

To see all the key bindings and commands, see the vim help pages (`:h vimwiki-mappings` and `:h vimwiki-commands`).

More information about VimWiki can be found [here](https://github.com/vimwiki/vimwiki)
