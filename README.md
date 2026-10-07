# .screenrc Configuration

A custom GNU Screen configuration file featuring 256-color/truecolor support, an extended scrollback buffer, and a tabbed colored status line.

## Overview

This `.screenrc` enhances the default GNU Screen experience with:

- **Bash as the default shell**
- **No startup message** for a cleaner session start
- **Alternate screen support** (proper handling of full-screen apps like `vim`, `less`, etc.)
- **Bold color rendering**
- **Background color erase (BCE)**
- **256-color and truecolor terminal support**
- **30,000 lines of scrollback**
- **Faster terminal passthrough** for xterm-style terminals
- **A tabbed, colored hardstatus line** at the bottom of the screen

## Installation

Copy the configuration into your home directory as `.screenrc`:

   ```bash
   cp .screenrc ~/.screenrc
   ```

## Configuration Breakdown

### Shell & Startup

```screen
defshell -bash
startup_message off
altscreen on
```

- `defshell -bash` — Uses `bash` as the default shell for new windows.
- `startup_message off` — Suppresses the copyright/startup splash screen.
- `altscreen on` — Enables the alternate screen buffer so full-screen apps restore your previous terminal contents on exit.

### Color & Rendering

```screen
attrcolor b ".I"
defbce on
term screen-256color
truecolor on
```

- `attrcolor b ".I"` — Allows bold colors to render correctly.
- `defbce on` — Erases the background using the current background color (avoids ugly artifacts).
- `term screen-256color` — Tells Screen to report itself as a 256-color terminal.
- `truecolor on` — Enables 24-bit truecolor support (requires a compatible terminal).

### Scrollback & Terminal Handling

```screen
defscrollback 30000
termcapinfo xterm* ti@:te@
```

- `defscrollback 30000` — Caches 30,000 lines of scrollback history per window.
- `termcapinfo xterm* ti@:te@` — Disables the terminal init/restore strings for xterm-like terminals, which prevents flickering and improves compatibility with modern terminal emulators.

### Hardstatus Line

```screen
hardstatus alwayslastline
hardstatus string '%{= Kd} %{= Kd}%-w%{= Kr}[%{= KW}%n %t%{= Kr}]%{= Kd}%+w %-= %{KG}'
```

- `hardstatus alwayslastline` — Keeps the status line permanently visible at the bottom.
- The status string renders open windows as tabs:
  - Inactive windows appear in **black on dark** (Kd).
  - The **current window** is highlighted in **red** (Kr) with a bracketed label showing its number (`%n`) and title (`%t`) in **white** (KW).
  - A trailing green (KG) segment anchors the right side.

## Requirements

- **GNU Screen** (tested with recent versions supporting `truecolor`)
- A **truecolor-capable terminal emulator** (e.g., Alacritty, Kitty, WezTerm, iTerm2, or a recent GNOME Terminal / Konsole) for `truecolor on` to be effective
- **Bash** available on your `PATH` (only if you keep the `defshell -bash` line — change or remove it if you prefer a different shell)

## Notes

- If your terminal doesn't support truecolor, you can remove or comment out `truecolor on` — Screen will still use 256 colors.
- The `termcapinfo xterm*` line is tailored to xterm-compatible terminals. If you use a different terminal family, you may need to adjust the pattern.
- Colors are defined using Screen's `%{= XY}` syntax, where `X` is the attribute (e.g., `K` for black background) and `Y` is the foreground color.

## License

This configuration is provided as-is. Feel free to modify it to suit your workflow.
