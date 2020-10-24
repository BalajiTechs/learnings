1. ctrl+P to search for all options.
3. ctrl+` to open terminal
2. Enable git-bash as default terminal 
1. First type "Ctrl+Shift+P" to open the command search and type/select "Open User Settings". 
2. If this display a settings search page you will need to hit the ”{}” at the top right to get to the raw JSON. 
3. Merge the following settings ensuring to use paths that match where you installed the "bash.exe" and "git.exe" binaries:
    {
        "terminal.integrated.shell.windows": "C:\\apps\\Git\\bin\\bash.exe",
        "terminal.integrated.env.windows": {
        "CHERE_INVOKING": "1"
        },
        "files.autoSave": "afterDelay"
    }