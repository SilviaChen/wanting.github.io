---
layout: post
title:  "Setup VIM with Python in Ubuntu 18.04"
categories: Software Technical Note
---

I referred some blogger articles to setup my vim for python, and this is just a note recording my steps:

&nbsp;&nbsp;&nbsp;

## 1. Prepare

#### Install vim
```
# apt-get install vim-scripts
# apt-get install vim-addon-manager
```

#### Install ctags

```
# apt-get install exuberant-ctags
```

#### Install taglist

```angular2html
# vim-addons install taglist
```

#### Install pydiction (in /usr/share/vim):

> Download pydiction from this page:https://www.vim.org/scripts/script.php?script_id=850

```angular2html
# wget https://www.vim.org/scripts/download_script.php?src_id=21842
# unzip download_script.php\?src_id\=21842
```

then you will get 'pydiction' directory

#### Configure vimrc(1/2)
> The '~/.vimrc' is a new file, not a default, you can refer other cofiguratiion to customize your vim:
 
```angular2html
# cp /usr/share/vim/vim80/vimrc_example.vim ~/.vimrc
# vim ~/.vimrc
```

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;

## 2. Python IDE

#### Configure ~/.vimrc(2/2)
> '~/.vim/after/ftplugin 'and '~/.vim/tools/pydiction/' are not default

```angular2html
#cp /usr/share/vim/pydiction/after/ftplugin/python_pydiction.vim ~/.vim/after/ftplugin
#cp /usr/share/vim/pydiction/complete-dict ~/.vim/tools/pydiction/complete-dict
```

#### Configure ~/.vimrc(2/2)
> The '~/.vimrc' is a new file, not a default, you can refer other configuration to customize your vim:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;

## DONE

![layout](/assets/images/ubuntu18_04.png)

