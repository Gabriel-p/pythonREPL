pythonREPL
==========

A [`Sublime Text`](https://www.sublimetext.com/) package for running Python REPLs.

This is a **heavily** stripped-down version of the [`SublimeREPL`](https://github.com/wuub/SublimeREPL) package, tested
only for running Python on Linux. The original `SublimeREPL` is no longer maintained
(it was last updated in 2016), and recent builds of `Sublime Text` have started to
break it.

Set key bindings to run either a Python REPL with the currently open file or an
interactive REPL without any file. E.g.:

```
// Runs currently open file in REPL
{
    "keys": [
        "f5"
    ],
    "command": "run_python_repl"
},
// Runs interactive REPL without any file
{
    "keys": [
        "f4"
    ],
    "command": "run_python_repl",
    "args": {
        "interactive": true
    }
}
```

## How the Python interpreter is chosen

Every time a REPL is opened, `resolve_python()` decides which Python
interpreter to launch, in this order:

1. **Manual override — `python_venv_path` setting.** If this setting is a
   non-empty string, pythonREPL treats it as the path to a virtual
   environment directory and appends `bin/python` to it. If the resulting
   path exists and is executable, it is used immediately and takes
   precedence over everything else. If it's set but the resulting file is
   missing or not executable, an error message is shown and pythonREPL
   falls back to the automatic search below.
2. **Automatic search — nearest `.venv`.** If `python_venv_path` is empty
   (or invalid), `get_venv_python()` starts at the directory of the current
   file and walks upward through parent directories looking for a
   `.venv/bin/python` executable. The first one found (closest to the file)
   is used.
3. **Fallback — Sublime Text's own interpreter.** If no file is open, or no
   `.venv/bin/python` is found anywhere up the directory tree, pythonREPL
   falls back to `sys.executable` (the Python interpreter running Sublime
   Text's plugin host), or `python3` if that isn't available.

The REPL banner shows both the resolved interpreter path and which of these
sources it came from (`python_venv_path setting` or `auto-detected`), so you
can always confirm what will be used.

### Setting a manual environment

To force pythonREPL to always use a specific virtual environment regardless
of the current file's location, set `python_venv_path` in your
`pythonREPL.sublime-settings` file to the path of that environment's root
directory (the folder containing `bin/python`):

```jsonc
{
	"python_venv_path": "/home/username/myproject/.venv"
}
```

Leave it as an empty string (`""`) to disable the override and use the
automatic `.venv` search described above.
