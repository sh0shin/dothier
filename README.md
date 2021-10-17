# dothier

Keep all your dotfiles in one or multiple git repositories and deploy them with
one simple command.

[![GitHub Release](https://img.shields.io/github/v/release/sh0shin/dothier)](https://github.com/sh0shin/dothier/releases)
[![GitHub License](https://img.shields.io/github/license/sh0shin/dothier)](https://github.com/sh0shin/dothier/blob/master/LICENSE)

## Installation

The only supported package manger for now is [homebrew](https://brew.sh).

```sh
brew tap sh0shin/tap
brew install sh0shin/tap/dothier
```

Or simply clone the git repository, it's just a bash script 8)

```sh
git clone https://github.com/sh0shin/dothier.git
install -m 0555 dothier/dothier /usr/local/bin
```

## Usage

```sh
dothier v0.2.8 ( https://sh0shin.org/dothier )
Usage: dothier [-CLRghnqrstv] [-f file] [-d dir] [-H home] [-k file]
Options:
  -C      : Disable colorized output
  -H home : Home directory (default: $HOME)
  -L      : Enable dead symlink search mode
  -R      : Enable remove/delete mode
  -c conf : Use config file (default: $HOME/.config/dothier)
  -d dir  : Use directory for recursive mode (default: $HOME/.dotfiles)
  -f file : Use dothier file (default: .hier)
  -g      : Enable git pull
  -h      : Show this help
  -k file : Use git-crypt key file
  -n      : Dry-run
  -q      : Be quiet
  -r      : Enable recursive mode
  -s      : Short message mode
  -t      : Enable tmutil (macOS only)
  -u      : Set umask (default: 0022)
  -v      : Enable verbose mode
```

* `dothier` config file (see: [dothier.config-sample](dothier.config-sample))

### Dotfiles repository

```sh
mkdir ~/.dotfiles
cd ~/.dotfiles
git init
git remote add origin <repo.url>

# Move your dotfiles here
# .profile
# .vimrc
# ...

# Define your dotfiles in a .hier file
```

* `.hier` file (see: [hier.sample](hier.sample))
* `.hiergit` file (see: [hiergit.sample](hiergit.sample))

### Deploy your dotfiles

```sh
dothier -f ~/.dotfiles/.hier
```

Or use the `-r` recursive option to deploy from `~/.dotfiles`,
all found `.hier` files will be used.

```sh
dothier -r
```
