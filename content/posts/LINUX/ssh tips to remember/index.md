---
title: SSH Tips to Remember
date: 2021-04-18
tags: [terminal, linux]
image: ssh.png
---

SSH, short for Secure Shell, is a protocol and a tool for secure network communications. It is widely used for connecting to remote servers for executing commands and transferring files between computers.

In this post I'll share tips on how I use SSH for various tasks in my day to day work and how it helps me to get jobs done in remote servers.

## Basic SSH

To connect to a remote server and use its terminal, execute

```bash
$ ssh the_user@domain.com 
# or with IP
$ ssh the_user@10.100.1.10
# or if ssh is served on different port
$ ssh the_user@10.100.1.10 -p 2222
```

After executing, you'll be asked for password, enter it and boom! You are now connected.

## Passwordless SSH

For passwordless SSH we need to create a private and public key pair in the client PC. To do that, execute

```bash
$ ssh-keygen -t rsa
Enter file in which to save the key (/home/john/.ssh/id_rsa): #Enter a path or keep default
Enter passphrase (empty for no passphrase): # Keep empty
Enter same passphrase again: # Keep empty
```

This will create a public and a private pair key in your mentioned path. Copy the contents of the file ending in **.pub** to **.ssh/authorized_keys**.

Alternatively, you could run the following to automatically do that.

```bash
$ ssh-copy-id -i file.pub user@192.168.1.110
```

Now if you try SSHing to the remote server, no password will be required!

## Copy files between machines

To copy files between PCs we will use a program called **scp**. It stands for _secure copy_.

To copy from localhost to remote server, execute

```bash
$ scp path/to/file user@192.168.1.110:path/to/save
```

To copy from remote server to localhost, just switch the source and destination of the previous command. Execute

```bash
$ scp user@192.168.1.110:path/to/copy path/to/save
```

## Synchronize folders between machines

To synchronize folders between PCs we will use **rsync**.

To sync folder on remote host with files from localhost, execute

```bash
$ rsync --archive --compress --partial --progress path/to/folder/ user@remote.com:path/to/folder/
```

To sync folder on local host with files from remote host, execute

```bash
$ rsync --archive --compress --partial --progress user@remote.com:path/to/folder/ path/to/folder/
```
## File transfer with FTP

Sometimes it makes more sense to login to a machine, see what files are present there and then download them. This can be done through **sftp**,, which stands for _secure file transfer protocol_.

To use sftp, run

```bash
$ sftp user@remote.com
```

After logging in, you'll get an interactive shell for traversing paths, uploading and downloading files.

```bash
sftp> pwd       # See current working directory on remote
sftp> lpwd      # See current working directory on local

sftp> ls        # List files on current remote directory
sftp> lls       # List files on current local directory

sftp> get remoteFile         # Get remote file
sftp> get remoteFile name    # Get remote file with custom name
sftp> get -r remoteDirectory # Get remote directory

sftp> put localFile
sftp> put -r localDirectory
```

## Configure local SSH for easier access

Sometimes it is troublesome to write the full __user@host.com__. It's especially troublesome when there is not domain configured and you need to enter with an IP like __user@92.168.1.110__.

We can configure the ssh client to make things easier.

Open **~/.ssh/config**. If the file doesn't exist, create it. 

In the file configure your hosts like the following

```conf
Host office
    HostName domain.com # or IP
    User john # the user name
    IdentityFile ~/.ssh/key.pub
```

Now if you can SSH like this

```bash
$ ssh office
$ scp office:~/Desktop/file.txt ~/Desktop/file.txt
$ sftp office
```

Boom! Now you can connect more easily to remote PCs!