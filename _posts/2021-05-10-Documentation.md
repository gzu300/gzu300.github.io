---
title: documentations
date: 2021-05-10
---

## Refer to PEP 257 for detailed description on how to document.
## Summarized conventions:
### A blank line after docstrings.
### For Script. E.g. the commond-line tools like samstools.
- When script is invoked with missing or incorrect arguments.
- Can several pages long. Such a docstring should document the script's function and command line syntax, environment variables, and files.
- should be sufficient for a new user to use the command properly, as well as a complete quick reference to all options and arguments for the sophisticated user
### For Module. 
- list the classes, functions, etc.
- one line summary for each of them
### For Class.
- summary of its behaviour.
- public methods and instance variables.
### For Func and Method.
- summary of its behaviour.
- arguments and returned values, side effects.
### For Subclass.
- summary of its difference to parent class.
- use 'override' to indicate methods that are totally replaced
- use 'extend' to indicate methods still calls the superclass
