# Setup a Git server

This guide will show you how to setup your own Git server.

## Conventions

 - `localbox` - The client machine or dev machine
 - `git-server` - The Git server machine
 
## Connectivity test

```bash
# Obtain the IP for the `git-server`
git-server> ifconfig

# Test the connectivity
localbox> ping 192.168.1.65
```

## Setup SSH access

### Install SSH server

```bash
git-server> sudo apt-get install openssh-server
```

## Create Git user

```bash
# Add new user
git-server>  sudo adduser git

# Test newly created user
git-server>  su - git
```

### Test logging in using SSH

```bash
localbox> ssh git@git-server


# Exit SSH session
git@git-server> exit
```


## Setup SSH keys for passwordless login

### Create a new SSH key

```bash
localbox> ssh-keygen

# Share your public key with the Git server admin
localbox> scp ~/.ssh/your_new_key.pub git@git-server:/home/git
```

### Add authorized keys

```bash
# Optional - only create directory if it doesn't exist
git@git-server> mkdir ~/.ssh

# Optional - only create file if it doesn't exist
git@git-server> touch ~/.ssh/authorized_keys


git@git-server> cat your_new_key.pub  >> ~/.ssh/authorized_keys 
```

## Test Git commands

```bash
localbox> git clone git@git-server:/home/git/proj1.git
```
