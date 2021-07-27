---
layout: post
title: 'Quick Guide: How to add aliases in Z shell?'
published: false
---

# Step 1

## Open up your terminal

# Step 2

## Edit the .bash_profile file using vim

```zsh
$ vim .bash_profile
```

# Step 3

## Add your alias to the file

```vim
alias linux_ssh='gcloud beta compute ssh --zone "australia-southeast2-a" "linux-ansible-playground"  --project "rugged-future-316207"'
```

Once you are done adding, ensure to save and quit by pressing the ESC key followed by :wq and ENTER.

# Step 4

## Check the alias works

```zsh
$ source .bash_profile
$ linux_ssh
```

# Step 5

## Add .bash_profile to .zshrc file

```zsh
$ vim .zshrc
```

```vim
source ~/.bash_profile
```

# Step 6

## Close and re-open the terminal

Test that your alias works without referencing the .bash_profile file.