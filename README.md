# GNU screen configuration

This README documents the settings in `.screenrc`.

## Settings

### Shell
```
defshell -bash
```
Sets the default shell used by screen to `bash`.

### Messages and screens
```
startup_message off
altscreen on
```
- `startup_message off` disables screen's startup banner.
- `altscreen on` enables the alternate screen, so full-screen applications
  (such as full-screen TUIs) do not clutter the scrollback buffer.

### Colors
```
attrcolor b ".I"
term term-256color
truecolor on
```
- `attrcolor b ".I"` assigns colors to bold attributes (`.I` is italic, which
  screen maps to bold), so styled text is colored as expected.
- `term term-256color` enables the 256-color terminal.
- `truecolor on` enables truecolor (24-bit) color output.

### Scrollback and clearing
```
defbce on
defscrollback 30000
```
- `defbce on` clears the background with the current background color when a
  window is cleared.
- `defscrollback 30000` caches 30000 lines of scrollback history.

### Terminal capabilities
```
termcapinfo xterm* ti@:te@
```
`termcapinfo` lets you modify terminal capabilities for matching terminals.

- `xterm*` matches all xterm-family terminals.
- `ti@` and `te@` delete the `ti` (terminal init) and `te` (terminal exit)
  capabilities. The `@` action removes the capability entirely.

Screen normally uses `ti`/`te` to save and restore the terminal title when a
session starts and stops. Deleting them means screen never changes the terminal
title, which avoids conflicts with other programs (such as tmux or shell
prompts) that manage the title themselves.

### Status line
```
hardstatus alwayslastline
hardstatus string '%{= Kd} %{= Kd}%-w%{= Kr}[%{= KW}%n %t%{= Kr}]%{= Kd}%+w %-= %{KG}'
```
- `hardstatus alwayslastline` always displays the hard status line on the last
  line of the terminal.
- `hardstatus string ...` defines a tabbed, colored hard status line showing the
  session name (`%n`) and tab title (`%t`).
