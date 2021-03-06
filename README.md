# bash-git-version-updater

A simple bash script to update the version of a git repository.

## 0.) Requirements

You need bash with version 4 at least, because it supports associative arrays and other stuff (https://www.admon.org/scripts/new-features-in-bash-4-0/):

```bash
user$ bash --version
GNU bash, Version 4.4.12(1)-release (x86_64-pc-linux-gnu)
Copyright (C) 2016 Free Software Foundation, Inc.
...
```

If you have a version lower than the version 4 (for example on mac):

```bash
user$ bash --version
GNU bash, version 3.2.57(1)-release (x86_64-apple-darwin17)
Copyright (C) 2007 Free Software Foundation, Inc.
```

You have to update your bash version first.

### 0.1) Update bash on mac to version 4

```bash
user$ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
user$ brew update && brew install bash
```

Add the new shell to the list of allowed shells:

```
user$ sudo bash -c 'echo /usr/local/bin/bash >> /etc/shells'
```

Change the shell:

```
user$ chsh -s /usr/local/bin/bash
```

Check the used shell locations:

```
user$ which -a bash
/usr/local/bin/bash
/bin/bash
```

Reopen your terminal and check again:

```bash
user$ bash --version
GNU bash, Version 4.4.19(1)-release (x86_64-apple-darwin17.3.0)
Copyright (C) 2016 Free Software Foundation, Inc.
...
```

Looks good. Now you are ready to use this library on your mac as well.

## 1.) First usage

### 1.1) Global installation

Maybe you need administration rights:

```
user$ cd /opt
user$ sudo install -d -o $(whoami) -m 775 bash-git-version-updater && cd bash-git-version-updater
user$ git clone https://github.com/bjoern-hempel/bash-git-version-updater.git .
user$ sudo bin/install
```

### 1.2) Local installation

In that case you don't need administration rights.

```
user$ cd /your/directory
user$ git checkout git@github.com:bjoern-hempel/bash-git-version-updater.git .
user$ bin/update-library
```

### 1.3 Update version of given git project

```
user$ cd /path/to/git/project
```

Global installation:

```
user$ bash-git-version-updater
```

Local installation:

```
user$ /your/directory/bin/bash-git-version-updater
```

## 2.) Version rules

### 2.1) set new version

Possible version that will be parsed:

* case1: no version available
* case2: v[major].[minor].[revision] (-[commit-number]-[revision-hash])
* case3: [major].[minor].[revision] (-[commit-number]-[revision-hash])

The version of the given repository will be set to:

* case1: v0.0.1 or v0.1.0 or v1.0.0 
* case2: v[major+1].[minor+1].[revision+1]
* case3: [major+1].[minor+1].[revision+1]

### 2.2) show version

#### No version available

```
user$ git describe
fatal: No names found, cannot describe anything.
```

#### Already set version

```
user$ git describe
v0.0.5-2-gf2d1127
```

or

```
user$ git describe
v0.0.6
```
