# dothier
Keep all your dotfiles in one or multiple git repositories and deploy them with
one simple command.

[![GitHub Release](https://img.shields.io/github/v/release/sh0shin/dothier)](https://github.com/sh0shin/dothier/releases)
[![GitHub License](https://img.shields.io/github/license/sh0shin/dothier)](https://github.com/sh0shin/dothier/blob/master/LICENSE)

## Notes
**v0.2.0+ is using different `.hier` properties!**
 * `ltype` is now `rtype` to represent repository type.
   - `ldir` -> `rdir`
   - `lfile` -> `rfile`
   - `lgit` -> `rgit`

 * `.gitsrc` files are now treated as `rfile`.
   - `pull` & `depth` properties were moved to the `.gitsrc` file itself.

 * Some options changed, see: [Usage](#usage).

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
```
dothier v0.2.0 ( https://sh0shin.org/dothier )
Usage: dothier [-CRghnrstv] [-f file] [-d dir] [-H home]
Options:
  -C      : Disable colorized output
  -H home : Home directory (default: $HOME)
  -R      : Enable remove/delete mode
  -d dir  : Use directory for recursive mode (default: $HOME/.dotfiles)
  -f file : Use dothier file (default: .hier)
  -g      : Enable git pull
  -h      : Show this help
  -n      : Dry-run
  -r      : Enable recursive mode
  -s      : Short message mode
  -t      : Enable tmutil (macOS only)
  -v      : Enable verbose mode
```

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

### `.hier` file
```sh
# (dot).hier
#! <path>                     <type>  <[@]mode> [link (yes|no)|link-source]
# the repository directory itself (~/.dotfiles)
.                             rdir    0700

# files within the repository
.editorconfig                 rfile   0640
.gitignore                    rfile   0640
LICENSE                       rfile   0640
README.md                     rfile   0640
dothier                       rfile   0750

# dotfiles collection (not shipped ;)
# link ~/.dotfiles/.profile to ~/.profile
.profile                      file    0600      yes  # link default: no

# linking the .profile file
# link ~/.dotfiles/.profile to ~/.bash_profile
.bash_profile                 link    0600      .profile

# link ~/.profile to ~/.bashrc
.bashrc                       link    0600      ~/.profile

# more dotfiles (mode will be enforced)
# link ~/.dotfiles/.gnupg to ~/.gnupg
.gnupg                        dir     0700      yes

# creates ~/.ssh (no link)
.ssh                          dir     0700

# link ~/.dotfiles/.ssh/id_ed25519 to ~/.ssh/id_ed25519
.ssh/id_ed25519               file    0600      yes

# link ~/.dotfiles/.ssh/id_ed25519.pub to ~/.ssh/id_ed25519.pub
.ssh/id_ed25519.pub           file    0644      yes

# link ~/.dotfiles/.vimrc -> ~/.vimrc
.vimrc                        file    0640      yes

# just rests within the ~/.dotfiles (mode will be enforced)
.screenrc                     file    0640

# macos directory which will be excluded from time machine backups (@mode)
.macos                        dir     @0700

# more...

# git repositories
# clone/pull git repositories to/from ~/.dotfiles/<name>
.gitsrc                       rgit    0600

# clone/pull git repositories to/from ~/<name>
.gitsrc                       git     0600
```

### `.gitsrc` file
```sh
#! <git-repository-url>                 [destination]     [[@]mode] [pull]  [depth]

# clone the repository as name dothier
# mode is set from umask, pull defaults to yes, depth to 1
https://github.com/sh0shin/dothier.git

# clone the repository as name dothier-git-src (mode: 0750)
# macos users can use @0750 to exclude from time machine backups
https://github.com/sh0shin/dothier.git  dothier-git-src   0750
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
