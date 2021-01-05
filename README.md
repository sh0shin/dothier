# dothier
Manage dotfiles hierarchy.  
Keep all your dotfiles in a git repository and deploy them with one simple
command `dothier`...

[![GitHub Release](https://img.shields.io/github/v/release/sh0shin/dothier)](https://github.com/sh0shin/dothier/releases)
[![GitHub License](https://img.shields.io/github/license/sh0shin/dothier)](https://github.com/sh0shin/dothier/raw/master/LICENSE)

## Installation
The only supported package manger for now is [homebrew](https://brew.sh)
```sh
brew tap sh0shin/tap
brew install sh0shin/tap/dothier
```

Or simply clone the git repository, it's just a bash script 8)
```sh
git clone https://github.com/sh0shin/dothier.git
cp dothier/dothier /usr/local/bin
chmod 0755 /usr/local/bin/dothier
```

## Usage
```
dothier v0.1.1 ( https://sh0shin.org/dothier )
Usage: dothier [-Dhrv] [-f file] [-d dir] [-H home]
Options:
  -D      : Enable verbose debug output
  -g      : Enable git pull (default: false)
  -h      : Show this help
  -r      : Enable recursive mode (default: false)
  -v      : Verbose output (default: false)
  -f file : The .hier file to use (default: .hier)
  -d dir  : Use directory for recursive mode (default: /your-homedir/.dotfiles)
  -H home : Home directory (default: /your-homedir)
```

### The `.hier` file
```sh
# (dot).hier

# the local repository directory itself (~/.dotfiles)
#                             type  mode
.                             ldir  0700

# local files within the repository directory
#                             type  mode
.editorconfig                 lfile 0640
.gitignore                    lfile 0640
LICENSE                       lfile 0640
README.md                     lfile 0640
dothier                       lfile 0750

# dotfiles collection (not shipped ;)
#                             type  mode  link
# link ~/.dotfiles/.profile to ~/.profile
.profile                      file  0600  yes  # link default: no

# linking the .profile file
#                             type  mode  source
# link ~/.dotfiles/.profile to ~/.bash_profile
.bash_profile                 link  0600  .profile
# link ~/.profile to ~/.bashrc
.bashrc                       link  0600  ~/.profile

# more dotfiles (mode will be enforced)
#                             type  mode  link
# link ~/.dotfiles/.gnupg to ~/.gnupg
.gnupg                        dir   0700  yes
# creates ~/.ssh (no link)
.ssh                          dir   0700
# link ~/.dotfiles/.ssh/id_ed25519 to ~/.ssh/id_ed25519
.ssh/id_ed25519               file  0600  yes
# link ~/.dotfiles/.ssh/id_ed25519.pub to ~/.ssh/id_ed25519.pub
.ssh/id_ed25519.pub           file  0644  yes
# link ~/.dotfiles/.vimrc -> ~/.vimrc
.vimrc                        file  0640  yes
# just rests within the ~/.dotfiles (mode will be enforced)
.screenrc                     file  0640
# more...
```

### Deploy your dotfiles hierachy
```sh
dothier -f ~/.dotfiles/.hier
```
