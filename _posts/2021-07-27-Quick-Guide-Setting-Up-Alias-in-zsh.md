---
layout: post
title: 'Quick Guide: How to add aliases in Z shell?'
published: true
---

In this quick guide, I show you how to add aliases in Z shell. This is particularly useful when you want to shorten a command that you frequently use.

For example, I set this up on my local machine so that I could easily SSH into my remote VMs. This means that I can type a single word in the terminal, instead of typing out the entire SSH command each time I want to log in remotely.

# Step 0

## Open up your terminal

# Step 1

## Check your directory

When you open up your terminal, you should automatically be in your home directory. Check this by using the command shown below. You should get an output similar to: **/Users/{your username}**.

```zsh
$ pwd
```

If you are not in your home directory, you can use the following command to navigate there.

```zsh
$ cd ~
```

# Step 2

## Open the .bash_profile file using vim

Once you're in your home directory, open the .bash_profile file using the following command.

```zsh
$ vim .bash_profile
```

# Step 3

## Add your alias to the file

Press the 'I' key to insert into the file. Use the arrow keys to navigate to a new line where you will be adding your alias.

Follow the syntax shown below to add your alias; replacing ${ALIAS_NAME} and ${COMMAND} with your choice.

```vim
alias ${ALIAS_NAME} = '${COMMAND}'
```
For example, in my case, I have added the command below to be able to easily access my Linux instance on GCP. Remember to insert your command inside the single quotation marks, as shown below.

```vim
alias linux_ssh='gcloud beta compute ssh --zone "australia-southeast2-a" "linux-playground" --project "rugged-future-316207"'
```

Once you have added your alias, ensure to save and exit by pressing the ESC key followed by ':wq' and ENTER.

# Step 4

## Check that the alias works

For now, we'll have to manually notify our machine to look in the .bash_profile file for our aliased command. 
```zsh
$ source .bash_profile
```
Next, we can check our alias works by calling it with the same name we entered earlier. You can check your alias' name by using the 'alias' command. Replace ${ALIAS_NAME} with your alias' name.

```zsh
$ alias
$ ${ALIAS_NAME}
```

# Step 5

## Add .bash_profile to the .zshrc file

The shell commands contained in the .zhrc file is run every time Z shell is invoked. By adding the previous command to this file, we can tell Z shell to look in .bash_profile for our newly added alias. This means we don't have to manually reference the .bash_profile file each time we want to use our alias.

Open up the .zshrc file using the vim editor.

```zsh
$ vim .zshrc
```

Whilst in this editor, press 'I' and use the arrow keys to navigate to a new line. Enter the following command and press ESC followed by ':wq' and ENTER.

```vim
source ~/.bash_profile
```

# Step 6

## Close and re-open the terminal

Exit out of the terminal and re-open it. Test your alias works without referencing the .bash_profile file manually.

# That's It!

I hope this quick guide helped you to get a new alias set up. Keep in mind that you don't have to use .bash_profile and can instead create a new file to house your aliases.

If you have any questions, feel free to let me know!

# Contact

You can find me at any of the following places!

- Website: [https://thanesh.io/](https://thanesh.io/)
- Email: [thanesh.pannirselvam@gmail.com](mailto:thanesh.pannirselvam@gmail.com)
- LinkedIn: [linkedin.com/in/thanesh-pannirselvam](https://linkedin.com/in/thanesh-pannirselvam)