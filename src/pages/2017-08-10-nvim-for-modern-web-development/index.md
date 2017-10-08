---
title: "NeoVim: vi for modern web development"
date: "2017-08-10T22:12:03.284Z"
path: "/neo-vim-for-modern-web-development/"
---

I had been programming for only a few months when I started using vim as my main editor.

Over the past year I transitioned to working on an all-javascript stack. The js runtime tends to be far less friendly towards the developer. Whereas ruby will present a useful `NoMethodError`, even trying to guess at method might have been intended, javascript will simply pass over misspelt function invocations, to cryptically bomb out later. This means that, to be productive, the modern javascript developer needs the kind of linting and autocorrect support from their IDE that vim doesn't give out the box.

I first tried installing [syntastic](https://github.com/vim-syntastic/syntastic) with the js plugin. While this works well in itself, it runs up against vim's lack of support for async jobs.  This meant that the whole vim process would lock up for 1 ~ 2 seconds while syntastic ran on file-save. This is a fundamental shortcoming of vim that's difficult to get around with plugins, that the creator vim had repeatedly refused to merge [patches](https://groups.google.com/forum/#!msg/vim_dev/-4pqDJfHCsM/LkYNCpZjQ70J) for.

At this point, after wasting an embarrassing amount of time on trivial bugs that would easily have been caught by a mature IDE, I started considering alternatives such as Visual Studio Code.

Fortunately, just in time, I discovered [Neovim](https://neovim.io/) and it was like falling in love with vim all over again. Neovim was forked off of vim specifically to provide support for async jobs. With the help of the [ALE](https://github.com/w0rp/ale) plugin, this means I can have a process running eslint in the background, alerting on linting failures and even autofixing on save! 

Here are the nvim-specific highlights of my current .vimrc:

```vimscript
Plug 'w0rp/ale'
" another plugin that targets nvim for autocompletion.
Plug 'roxma/nvim-completion-manager'

" ALE SETTINGS...

" ===== AUTOCOMPLETE ======
" maps tab to cycle through menu
inoremap <expr> <Tab> pumvisible() ? "\<C-n>" : "\<Tab>"
inoremap <expr> <S-Tab> pumvisible() ? "\<C-p>" : "\<S-Tab>"

" ale sign gutter always displays
let g:ale_sign_column_always = 1

" bufferline displays filename relative to current directory
let g:bufferline_fname_mod = ':.'

" sets eslint as default fixer for javascript files
let g:ale_fixers = {
\   'javascript': ['eslint'],
\}

" runs :ALEFix on save
let g:ale_fix_on_save = 1
```

In short, if you haven't yet switched I recommend you do so immediately.
