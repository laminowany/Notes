# gdb
[back to main index](../README.md)

## Common
- `start` - puts **tbreak** on main() and runs the program
- `r/run`
- `k/killc`
- `bt/backtrace`
- `l/list` - list source file
- `<Ctrl + P/N>` - previous/next command

## Frames
- `bt/backtrace` - show frames
- `frame #N` - switch to frame **#N**
- `up` - go frame up
- `down` - go frame down

## TUI (Text User Interface)
- `<Ctrl + X, A>` to enter/exit TUI, or:
  - `tui enable`
  - `tui disable`
- `<Ctrl + L>` - repaint the screen
- layouts:
  - `layout asm`
  - `layout regs`
  - `layout split`
  - `layout src`
    - `layout prev/next`
- `<Ctrk + X, 2>` - cycle through layouts
- `<Ctrl + X, O>` - change active wingow

## info
- `info args`
- `info locals`
- `info r` - registers
- `info threads`
  - `thread #N` - switch to thread nr **#N**
