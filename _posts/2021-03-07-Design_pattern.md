---
title: Design Pattern in Python
date: 2021-03-07
---

# Some of the 'GoF' design patterns disapper in Python
note: if a module imports more than 3 major modules. see if it can be refactored.
## 'program to interfaces, not implementation'
Java or C++ fixes the type of output naturally(eg. if File format, then WebSocket format will not be a valid output). So have to write an interface that fakes to be any types.

## 5 creational patterns
### Factory method, Abstract Factory and Singleton patterns is trivial in Python since a function in Python could possibly return any type of class.   
Singleton pattern in fact is a alternate to global variable in other languages. But Python modules can not intercept global variables. So Python's singletons is just function which looks like:
```python
# If singleton class not set, set it. If set, return it
_singleton = None
def get_singleton(cls=MyClass):
    global _singleton
    if not _singleton:
        _singletone = cls()
    return _singleton
```
### Prototype
replaced by the copy module
### Builder
Still have to be implemented by syntax

## 7 structural patterns
### Adapter
Still useful. Override methods with unified methods names
### Bridge
Still useful. Seperate a business layer out of the lower level so that lower level only stores data, business layer operates
### Composite
Still useful. Has a child object which is the basic element or the object like itself recursively. Store children objects as list, dict or just the object itself.
