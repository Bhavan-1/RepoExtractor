![](https://raw.githubusercontent.com/TimothyYe/skm/master/snapshots/skm.png)

[![Release][3]][4] [![MIT licensed][5]][6] [![Build Status][1]][2] [![Go Report Card][7]][8] [![GoCover.io][11]][12] [![GoDoc][9]][10]

[1]: https://travis-ci.org/TimothyYe/skm.svg?branch=master
[2]: https://travis-ci.org/TimothyYe/skm
[3]: http://github-release-version.herokuapp.com/github/timothyye/skm/release.svg?style=flat
[4]: https://github.com/timothyye/skm/releases/latest
[5]: https://img.shields.io/dub/l/vibe-d.svg
[6]: LICENSE
[7]: https://goreportcard.com/badge/github.com/timothyye/skm
[8]: https://goreportcard.com/report/github.com/timothyye/skm
[9]: https://godoc.org/github.com/TimothyYe/skm?status.svg
[10]: https://godoc.org/github.com/TimothyYe/skm
[11]: https://img.shields.io/badge/gocover.io-81.8%25-green.svg
[12]: https://gocover.io/github.com/timothyye/skm

SKM is a simple and powerful SSH Keys Manager. It helps you to manage your multiple SSH keys easily!

![](https://github.com/TimothyYe/skm/blob/master/snapshots/demo.gif?raw=true)

## Features

* Create, List, Delete your SSH key(s)
* Manage all your SSH keys by alias names
* Choose and set a default SSH key
* Display public key via alias name
* Copy default SSH key to a remote host
* Rename SSH key alias name
* Backup and restore all your SSH keys
* Prompt UI for SSH key selection

## Installation

#### Homebrew

```bash
brew tap timothyye/tap
brew install timothyye/tap/skm
```

#### Using Go

```bash
go get github.com/TimothyYe/skm/cmd/skm
```

#### Manual Installation

Download it from [releases](https://github.com/TimothyYe/skm/releases) and extact it to /usr/bin or your PATH directory.

## Usage
```bash
% skm

SKM V0.5.2
https://github.com/TimothyYe/skm

NAME:
   SKM - Manage your multiple SSH keys easily

USAGE:
   skm [global options] command [command options] [arguments...]

VERSION:
   0.5.2

COMMANDS:
     init, i      Initialize SSH keys store for the first time usage.
     create, c    Create a new SSH key.
     ls, l        List all the available SSH keys.
     use, u       Set specific SSH key as default by its alias name.
     delete, d    Delete specific SSH key by alias name.
     rename, rn   Rename SSH key alias name to a new one.
     copy, cp     Copy current SSH public key to a remote host.
     display, dp  Display the current SSH public key or specific SSH public key by alias name.
     backup, b    Backup all SSH keys to an archive file.
     restore, r   Restore SSH keys from an existing archive file.
     help, h      Shows a list of commands or help for one command.

GLOBAL OPTIONS:
   --help, -h     show help
   --version, -v  print the version
```

### For the first time use

You should initialize the SSH key store for the first time use:

```bash
% skm init

✔ SSH key store initialized!
```

So, where are my SSH keys?
SKM will create SSH key store at ```$HOME/.skm``` and put all the SSH keys in it.

__NOTE:__ If you already have id_rsa & id_rsa.pub key pairs in ```$HOME/.ssh```, SKM will move them to ```$HOME/.skm/default```

### Create a new SSH key
__NOTE:__ Currently __ONLY__ RSA and ED25519 keys are supported!

```bash
skm create prod -C "abc@abc.com"

Generating public/private rsa key pair.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /Users/timothy/.skm/prod/id_rsa.
Your public key has been saved in /Users/timothy/.skm/prod/id_rsa.pub.
...
✔ SSH key [prod] created!
```

### List SSH keys
```bash
% skm ls

✔ Found 3 SSH key(s)!

->      default
        dev
        prod
```
### Set default SSH key
```bash
% skm use dev
Now using SSH key: dev
```

### Prompt UI for key selection

You can just type ```skm use```, then a prompt UI will help you to choose the right SSH key:

![](https://github.com/TimothyYe/skm/blob/master/snapshots/prompt.gif?raw=true)

### Display public key

```bash
% skm display
```

Or display specific SSH public key by alias name:

```bash
% skm display prod
```

### Delete a SSH key

```bash
% skm delete prod

Please confirm to delete SSH key [prod] [y/n]: y
✔ SSH key [prod] deleted!
```
### Copy SSH public key to a remote host

```bash
% skm cp timothy@example.com

/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/Users/timothy/.skm/default/id_rsa.pub"
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
timothy@example.com's password:

Number of key(s) added:        1

Now try logging into the machine, with:   "ssh 'timothy@example.com'"
and check to make sure that only the key(s) you wanted were added.

✔  Current SSH key already copied to remote host
```

### Rename a SSH key with a new alias name

```bash
% skm rn test tmp
✔  SSH key [test] renamed to [tmp]
```

### Backup SSH keys

Backup all your SSH keys to $HOME directory by default.

```bash
% skm backup

a .
a ./test
a ./default
a ./dev
a ./dev/id_rsa
a ./dev/id_rsa.pub
a ./default/id_rsa
a ./default/id_rsa.pub
a ./test/id_rsa
a ./test/id_rsa.pub

✔  All SSH keys backup to: /Users/timothy/skm-20171016170707.tar
```

### Restore SSH keys

```bash
% skm restore ~/skm-20171016172828.tar.gz                                                                                           
x ./
x ./test/
x ./default/
x ./dev/
x ./dev/id_rsa
x ./dev/id_rsa.pub
x ./default/._id_rsa
x ./default/id_rsa
x ./default/._id_rsa.pub
x ./default/id_rsa.pub
x ./test/id_rsa
x ./test/id_rsa.pub

✔  All SSH keys restored to /Users/timothy/.skm
```

### Hook mechanism

Edit and place a executable file named ```hook``` at the specified key directory, for example:

```bash
~/.skm/prod/hook
```

This hook file can be both an executable binary file or an executable script file.

SKM will call this hook file after switching default SSH key to it, you can do some stuff in this hook file. 

For example, if you want to use different git username & email after you switch to use a different SSH key, you can create one hook file, and put shell commands in it:

```bash
#!/bin/bash
git config --global user.name "YourNewName"
git config --global user.email "YourNewEmail@example.com"
```

Then make this hook file executable:

```bash
chmod +x hook
```

SKM will call this hook file and change git global settings for you!

## Licence

[MIT License](https://github.com/TimothyYe/skm/blob/master/LICENSE)
