# LunarVim 
[back to main index](../README.md)

## General
* leader key is `<SPACE>`
* navigation between windows `<Ctrl + h/j/k/l>`
* navigation between buffers
    * previous buffer `<Leader + b, b>`
    * next buffer `<Leader + b, n>`
    * jump to buffer `<Leader + b, j>`
* to go to specific line:
  * `<line_number>G`
  * `:<line_number>`

## Editing
* `<x>` deletes a character
* `<dd>` deletes a line
* `<p>` to put deleted text after cursor
* `<P>` to put deleted text before cursor
* `<i`> to insert before cursor
* `<a>` to append after cursor
* `<A>` to append at the end of new line
* `<o>` to open new line at the bottom
* `<O>` to open new line at top

## Replace
* `<r<char>` to replace single character
* `<R>` to replace multiple characters

## Operators
* `d` - delete
* `c` - change
* `y` - yank(copy)

## Motions
* `w` - until start of next word
* `e` - end of current word
* `0` - start of line
* `$` - end of line
* `gg` - first line
* `G` - last line

## Change command syntax

operator [number] motion

## Changes
* `<u>` to undo last changes
* `<U>` to fix entire line
* `<Ctrl + r>` to redo changes
* `:q!` to discard changes and quit
* `:wq` to save and quit

## Windows
* `<Ctrl + w, s>` - to split windows horizontally
* `<Ctrl + w, v>` - to split windows vertically horizontally
* `<Ctrl + h/j/k/k>` - to move between the windows 
* `<Ctrl + w, c>` - to close the window

## Searching
* searching for a word in a file:
  * `/` to search forward
  * `?` to search backward
  * `<n>` go to next finding
  * `<N>` go to previous finding
* `<%>` go to matching parenthesis


## Jumplists
* jumplist is stored per each window
  * `<Ctrl + o>` - to go back
  * `<Ctrl + i>` - to go forward

## Substitutions 
* to substitute use
  * `:s/<what>/<to_what>/` single substitution
  * `:s/<what>/<to_what>/g` global substitution
  * `:N,Ms/<what>/<to_what>` substitution from line N to M

## Visual mode
  * `<v>` to enter visual mode

## Misc
* to make language server like clangd work remember to set `CMAKE_EXPORT_COMPILE_COMMANDS`
* `<Ctrl + g>` to display status of file
* `<Ctrl + \>` to toggle terminal
* `:!<command>` to run any shell command
* `:r <file/pipe/command results>` - retrieve text and put it on cursor
