---
setup: |
  import Layout from '../../layouts/BlogPost.astro'
title: How I manage my dotfiles
publishDate: 21 Dec 2021
name: Zac Yellowhorse
description: I have been using neovim for about 6 months and I want to be able to version control my configurations...

---
- [Intro](#intro)
- [Getting started](#getting-started)
- [Copy files](#copy-files)
- [Stow files](#stow-files)

## Intro
I have been using neovim for about 6 months and I want to be able to version control my configurations in case I ever need to move to another machine. I have been looking into how others tackle this and I have landed on using `stow`. Stow is an program that takes an input directory and creates symlinks to the equivalent location in the target directory. This way you can have all of your config files living in one location but have you system still be able to find those files where it expects them to be.

One thing you need to keep in mind when using stow is that it expects the input directory to be similar to the target directory so it knows where to create symlinks

## Getting started
First I needed to install stow because it was not already installed.

```bash
sudo apt update && sudo apt upgrade
sudo apt install stow
```

I needed to create the base directory (stow directory) where I was going to place my files which I called .dotfiles, located in my home directory.

```bash
mkdir ~/.dotfiles
```

## Copy files
Now I am going to create a nvim directory inside the .dotfiles directory so I can keep all my neovim config settings in one place.  In side my newly created folder I want to create a similar folder structure to how I want the files symlinked when stowed so I will also create a .config directory inside nvim. Now I will copy my nvim folder to the .config directory. 

```bash
mkdir ~/.dotfiles/nvim
mkdir ~/.dotfiles/nvim/.config
cp ~/.config/nvim ~/.dotfiles/nvim/.config
```

At the end I will have a directory that structure that looks like this:
```bash
└── home
    ├── .config
    │   └── nvim
    └── .dotfiles
        └── nvim
            └── .config
                └── nvim
```

## Stow files
To run stow you call stow and pass it a directory as a parameter. Stow will then assume your target directory is the parent directory; so one level up. Again stow looks in the directory that you passed in and attempts to create symlinks based upon the directory structure.  

I'm going to test stow now that its copied to my .dotfiles directory. First I rename my original nvim config to nvim-old in case it does not work I still have it sitting there. 

```bash
mv ~/.config/nvim ~/.config/nvim-old
```

Here is what my directory structure looks like before running stow:

```bash
└── home
    ├── .config
    │   └── nvim-old
    └── .dotfiles
        └── nvim
            └── .config
                └── nvim
```

Now I go to my .dotfiles directory and run stow

```bash
cd ~/.dotfiles

stow nvim
```

Here is what my directory structure looks like after running stow:

```bash
└── home
    ├── .config
    │   ├── nvim-old
    │   └── nvim (symlink pointing to ~/.dotfiles/nvim/.config/nvim)
    └── .dotfiles
        └── nvim
            └── .config
                └── nvim
```

Now that I have verified that its working as I want and as intended I feel confident in deleting the nvim-old directory. I'm going to initialize a new get repository in my .dotfiles directory and push it up to Github found [here](https://github.com/zyellowhorse/.dotfiles)
