---
title: Design Pattern in Python
date: 2021-03-07
---

# Some of the 'GoF' design patterns disappear in Python
note: if a module imports more than 3 major modules. see if it can be refactored.
## 'program to interfaces, not implementation'
Java or C++ fixes the type of output naturally(eg. if File format, then WebSocket format will not be a valid output). So have to write an interface that fakes to be any types.
## ```if/elif/else``` should be used only when these branches serve different goals. If found different branch serve the same goal but just different execution, look for a common interface.
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
Still exists and useful to organize the code.
### Adapter
Still useful. Override methods with unified methods names
### Bridge
Still useful. Seperate a business layer out of the lower level so that lower level only stores data, business layer operates
### Composite
Still useful. Has a child object which is the basic element or the object like itself recursively. Store children objects as list, dict or just the object itself.

### Facade
Still useful. Builder creates a complex object. Facade operates a complex object. Simple example is ```find()```method of a object that lets us do not have to write iteration to search the whole data.
### Flyweight
still useful
### Proxy
Performed by ```__getattr__()``` in Python
### Decorator
same as decorators in python

## 11 behavioral patterns
They are big solutions for big probelms and some of the patterns turn up into libraries. But still useful in python. They can be collapsed into callbacks or data structures that hold functions.
### Interperter
Python itself is interpreted
### Iterator
is built-in in Python. implement ```yield``` in ```__iter__``` method
### Mediator
still useful
### Memento
### Observer
still useful. esp in GUI and DOMs
### State
