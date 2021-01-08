# dothier
Keep all your dotfiles in one or multiple git repositories and deploy them with
one simple command.

[![GitHub Release](https://img.shields.io/github/v/release/sh0shin/dothier)](https://github.com/sh0shin/dothier/releases)
[![GitHub License](https://img.shields.io/github/license/sh0shin/dothier)](https://github.com/sh0shin/dothier/blob/master/LICENSE)

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
  -d dir  : Use directory for recursive mode (default: ~/.dotfiles)
  -H home : Home directory (default: ~/)
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

# git repositories
#                             type  pull  depth
# clone/pull git repositories to/from ~/.dotfiles/<name>
.lgitsrc                      lgit  yes # depth default: 1
# clone/pull git repositories to/from ~/<name>
.gitsrc                       git   yes   1
```

### The `.(l)gitsrc` file
```sh
# git repository url                      name (optional)
# destination path is defined in .hier
# clone the repository as name dothier
https://github.com/sh0shin/dothier.git
# clone the repository as name dothier-git-src
https://github.com/sh0shin/dothier.git    dothier-git-src
```

### Deploy your dotfiles
```sh
dothier -f ~/.dotfiles/.hier
```
Or use the `-r` recursive option to deploy from `~/.dotfiles`, per default all
found `.hier` files will be used.
```sh
dothier -r
```
