## Invoking the Interpreter

Interpreter options:
  - `python -c` for execute command
  - `python -m` for execute module
  - `python -i file.py` for execute interactive mode
      (interactive mode after running the script)

## Argument Passing
sys.argv - list with arguments (filenames, flags, commands/modules)

## Source Code Encoding
Default: utf-8

To declare an encoding other than the default one, a special comment line
should be added as the first line of the file (but after shebang).
The syntax is as follows:
```
#!/usr/bin/env python3
# -*- coding: encoding -*-
```
