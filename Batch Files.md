# Get info from current file location

Using the special variable `%~0` you can get the full path for the current file.

```
@echo off
set "DIR=%~0"

echo %DIR%
pause
```
*This prints the file directory*

Depending what you place between the '%~' and the '0' you can take specific parts of the full path. 

Take your pick from:

```
d -- drive
p -- path
n -- file name
x -- extension
f -- full path
```

E.g., from inside c:\tmp\foo.bat, `%~nx0` gives you "foo.bat", whilst `%~dpnx0` gives "c:\tmp\foo.bat". Note the pieces are always assembled in canonical order, so if you get cute and try `%~xnpd0`, you _still_ get "c:\tmp\foo.bat"