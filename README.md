# virename
Batch rename files using your editor. The script is pretty short and simple - I encourage you to look at it yourself to see what it does in detail.

## Usage

### Rename all files in current directory
```sh
virename
```

### Rename all PNG's using shell globbing
```sh
virename *.png
```

### Rename all but PNG's, reading the list of files to rename from stdin (notice the `-`)
```sh
find -not -name "*.png" | virename -
```

### Change the default editor
```sh
EDITOR=nvim virename
```

### Change the default mv command
- Create all leading destination directories if they don't exist by using `install -D`
```sh
MV='install -D' virename
```
- Integrate with git using `git mv`
```
git ls-files -m | MV='git mv -v' virename -
```

## Inspiration
I was obviously inspired by [vimv](https://github.com/thameera/vimv). Thing is - it does some questionable things (evals, using `ls` output, repeatedly echo-appending to the same file and such). I could've opened a couple of PR's to fix all theese things, but that would be me basically rewriting the whole script - why not just do exactly that here? And add a couple of features while I'm at it - support for reading the filenames from stdin, and customizable mv command. The latter allowed me to remove `git mv` and `mkdir -p` integrations from the script itself, but still make them (and much more) possible :)
