---
title: Passwordless SSH connection to a Cluster
date: 2018-10-04 15:10:09
tags: [Research Daily, CAML]
categories: Research Daily
---

I am using the cluster [GRAHAM](https://docs.computecanada.ca/wiki/Graham) for our simulation, and it uses SSH (Secure Shell) to connect to the remote servers. It is found annoying to type the password everytime you try to log in or copy files from the server. Herewith several simple commands, we could domake the password-less connection (for MacOS only).

<!--more-->
1. `cd ~/.ssh/`, enter the folder where the ssh keys are kept.
2. `ssh-keygen -t rsa`, create a new ssh key pair. You would be asked to 
   `Enter file in which to save the key:` and I use `graham` here.
3. `ssh-add -K graham`, add the ssh private key to the ssh-agent to store the passphrase the keychain.
4. `cat graham.pub >> authorized_keys`, write the public key into the file authorized_keys.
5. `ssh-copy-id -i graham.pub USER@graham.computecanada.ca`, `ssh-copy-id` is to use locally available keys to authorize logins on a remote machine. The authorized_keys is copied to the cluster.

**Done!**

PS: add `alias graham='ssh -y USER@graham.comoputecanada.ca'` into `~./bash_profile` for convenience

### Userful links
- [SSH Key](https://www.ssh.com/ssh/key/)
- [SSH Files](https://www.msri.org/realvideo/ln/msri/usered/ssh/bernstein/1/7.html)
- [Github Help](https://help.github.com/articles/connecting-to-github-with-ssh/)


