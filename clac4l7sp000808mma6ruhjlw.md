---
title: "Create SSH keys to access GitHub via SSH"
datePublished: Fri Nov 11 2022 06:36:11 GMT+0000 (Coordinated Universal Time)
cuid: clac4l7sp000808mma6ruhjlw
slug: create-ssh-keys-to-access-github-via-ssh
canonical: https://arunava.tech/blog/creat-ssh-key-to-access-github-via-ssh
tags: ubuntu, linux, github, ssh

---

Dont need if you use github desktop ~

I do this all the time whenever I break my Arch install (ye I have my backups in timeshift, dont teach me now) or I do another distro hop, so thought why not I just put these in my easy website to easy access these commands, instead of typing them always :p

1. Open terminal and cd into ssh folder (mkdir ~/.ssh if it doesnt exist there )
    

```bash
cd ~/.ssh
```

1. Update with your GitHub Email Address
    

```bash
ssh-keygen -t rsa -b 4096 -C "arnvgh@gmail.com"
```

Ignore passphrase (by press Enter key without input any characters) if you want to create a non-passphrase ssh key

![Screenshot from 2022-11-11 11-47-34.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1668147634907/SS1hVWVU-.png align="center")

3\. Run ssh agent

```bash
eval $(ssh-agent -s)
```

1. Add the key has been just generated to ssh agent you can simply run (if you are folllowing my guide)
    

```bash
ssh-add
```

else

```bash
ssh-add "/home/username/.ssh/ssh_file_name"
```

1. Copy the SSH Key by
    

```bash
ls
cat id_rsa.pub
```

(Dont copy mine, I have changed it alr :p)

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1668147974099/UpwaGk2d0.png align="center")

**Finally,**

Add the publickey to github account (go to "Setting" then select "SSH and GPG keys")

here ~ https://github.com/settings/keys

Happy Coding 🐼