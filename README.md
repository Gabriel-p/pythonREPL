pythonREPL
==========

A [`Sublime Text`](https://www.sublimetext.com/) package for running Python REPLs.

This is a **heavily** stripped-down version of the [SublimeREPL](https://github.com/wuub/SublimeREPL) package, tested
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