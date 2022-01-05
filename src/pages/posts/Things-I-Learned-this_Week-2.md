---
setup: |
  import Layout from '../../layouts/BlogPost.astro'
title: Things I Learned this Week 2
publishDate: 31 Dec 2021
name: Zac Yellowhorse
description: Since its in between holidays and most people are off / taking vacation I did not do much work related tasks. I did however take the time to get learn more Kubernetes and make my command like look cooler. 

---

- [Intro](#intor)
- [oh-my-zsh plugins](#oh-my-zsh-plugins)
- [Powerlevel10K](#powerlevel10k)

## Intro
Since its in between holidays and most people are off / taking vacation I did not do much work related tasks. I did however take the time to get learn more Kubernetes and make my command like look cooler. 

## oh-my-zsh plugins 
While this isn't really something new I learned but I recently enabled the [aws plugin](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/aws) in on in my ~/.zshrc. 

Basically this plugin will display your aws profile you are set to use when running aws commands, here is how it looks in my terminal: 
![[Pasted image 20211229133319.png]]

This is helpful to me because I have been running Terraform manually recently and its helpful to see what profile I am using at the moment and be able to switch profiles easily with `asp <profile>`. 

The other one I found useful is the [kubectl](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/kubectl) and [kubectx](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/kubectx). Kubectl provides some handy aliases to kubeclt so you dont have to type it all out all the time and kubectx shows your context in the terminal similar to the aws plugin. Here is how kubectx looks like in my terminal: 
![[Pasted image 20211230142217.png]]

This is also helpful so that I can easily see what context is set to without having to run `kubectl config current-context`.

To add these to your ZSH you need to add `aws` and `kubectl` to the list of plugins in the .zshrc file. It will look like this

```bash
plugins=(
	git
	zsh-autosuggestions
	aws
	kubectl
)
```

To get the kubernetes context to show up you need to add `RPS1='$(kubectx_prompt_info)'` anywhere in your .zshrc file. 

## Powerlevel10K
Powerlevel10k is what I use to make my command line look cool, you can find the repo [here](https://github.com/romkatv/powerlevel10k). You can read the README to get more info but for me it was running these two lines to clone the repo and add it to my .zshrc file
```bash
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ~/powerlevel10k
echo 'source ~/powerlevel10k/powerlevel10k.zsh-theme' >>~/.zshrc
```
once that was done I reloaded my zsh with `exec zsh` and it came up with a wizard to configure how I want it to look. You follow the prompts and select what you like and thats it. It will require you to have a font installed that can display the emojis or unicode characters if you don't already have it setup. 

Both the powerlevel10k settings and the oh-my-zsh plugins are in my .dotfile repo found [here](https://github.com/zyellowhorse/.dotfiles) if you would like to see my setup exactly. 
