# dothier

Manage dotfiles hierarchy.

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

## Supported types

 * `dir` - Directory
 * `ldir` - Local directory
 * `file` - File
 * `lfile` - Local file
 * `link` - (Sym)link
 * `git` - Git
 * `lgit` - Local git
