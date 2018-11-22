# Linux

## Exec Python File without calling python

```python
#!/usr/bin/python2.7
import sys ...
```

And then give X permission

```bash
chmod +x x.py
```

## Env

```bash
env
env | grep \$USER
```

### Add Env

```bash
export PATH=$PATH:/newEnv/
```

## Vim

### Open side by side

```bash
vim -O file1.c file2.c
```

* Ctrl+W + →←  to Switch between views

### Commands

| Command    | Desc |
|------------|------|
| Esc/ Ctrl+C| Switch Modes
| i          | InsertMode
| A          | Append at end of line
| o          | i + NewLine Below Cursor
| u          | Undo
| dd         | delete line
| shift+o    | i + NewLine Above Cursor
| :w filename| Save File
| :sav       | Save As
| :q!        | force exit
| :e         | Open
| :sp        | Split Open
| :tabe      | Open in new Tab
| :browse e      | Open with FileExplorer
| :sh        | fg, Like Ctrl+Z
| :!(any bash cmd) | To execute Bash Cmd in Vim
| :syntax on | Syntax Highlighter
| :set syntax=perl | Set Syntax Lang
| :set number| Enable Line Number
| :set tabstop=4 shiftwidth=4 softtabstop=4 | Set default TAB width
| 10w        | skip forward 10 words
| 10dd       | delete 10 lines
| * # g* g#  | find word under cursor (forwards/backwards)
| %         | match brackets {}[]\(\)
| :set ignorecase | Search ignorecase
| /wordRegex| Search word from top to bottom