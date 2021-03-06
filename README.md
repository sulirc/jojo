# JOJO

> Convenient command line path shuttle tool

## Design Goal
Every searching will locate register file and find the alias key. Each alias key must begin with symbol `@`. One path may have multiple alias key. Data will be saved in a file which exist in system root path. 
```
@npm
/Users/sulirc/.nvm/versions/node/v14.16.1/bin/npm

@desk:@des:@d
/Users/sulirc/Desktop

@rock
/Users/sulirc/spaceship/workspace/rock_proj
```

## Command

### jojo jump
 jump target path by alias:
```bash
jojo-jump @desk
# or short command
j @desk
```

In essence: The rust program can only affect its own environment, not your shell. Therefore we need to implement command by wrapping `jojo expand` in bash function:

```bash
jojo_jump() {
  cd $(jojo expand "$1")
}
j() {
  jojo_jump $1
}
```

Refer to the bash function above. we can create more handy bash function.

```bash
# open your project with your editor quickly
jojo_code() {
  code $(jojo expand "$1")
}
# open folder quickly
jojo_open() {
  open $(jojo expand "$1")
}
```

### jojo register
Register new alias key:
```bash
jojo register @desk /Users/user/Desktop/
# or you can use relative path, command below is same as above (as long as if you are on desktop currently)
jojo register @desk .
# and short command below
jojo r @desk .
```

### jojo name
Update registered alias key to new name:
```bash
jojo name @foo @bar
# short command
jojo n @foo @bar
```

### jojo unregister
Unregister an alias key:
```bash
jojo unregister @desk
# short command
jojo R @desk
```

### jojo list 
List all alias keys:
```bash
jojo list
# short command
jojo l
```

### jojo expand
Expand alias key. Therefore redirect path string to stdout.
```bash
jojo expand @desk
# short command
jojo e @desk
```

### jojo clean
Clean all alias keys(Caution: can not redo):
```bash
jojo clean
```
