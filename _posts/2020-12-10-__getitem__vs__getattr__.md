---
date: 2020-12-10
title: Python class __getitem__ vs __getattr__
---

When came to get attribute in a real project yesterday, I got confused. What is the difference between __getitem__ and __getattr__, __setitem__ and __setattr__?

##  ```__getitem__``` and ```__setitem__```, called containers. Get and set data.
### example
```python
class Indexer:
    data = [5, 6, 7]
    def __getitem__(self, index):
        return self.data[index]
    def __setitem__(self, index, value):
        return self.data[index] = value
    def __delitem__(self, index):
        del self.data[index]

>>> x = Indexer() 
>>> x[0]   #See, this makes direct index on class object, rather than x.data[0] possible.
5
```
### Notice ```__getitem__``` not only fetch data by index, it also makes iteration possible(of course other methods like __next__ etc also initiates iterations)

## ```__getattr__``` and ```__setattr__```, called attribute reference. Get and set attributes
```python
class Indexer:
    ...
    def __getattr__(self, name):
        return self.__dict__[name]
        
    def __getattribute__(self, name):
        return object.__getattribute__(self, name)
        #return self__dict__[name] #this also causes loop!
        
    def __setattr__(self, name, value):
        self.__dict__[name] = value
        #object.__setattr__(self, name, value) #this also avoids loops
        #self.name = value #causes recursive loop!
```

## properties. Get and set a perticular attribute
### there are two ways to use properties for attr getter and setter
#### without descriptor
```python
class X:
    def getX(self): ...
    def setX(self): ...
    def delx(self): ...
    name = property(getx, setx, delx, 'name property doc string')
```
#### with descriptor
```python
class X:
    @property
    def name(self): ...
    @name.getter
    def name(self): ...
    @name.setter
    def name(self): ...
    @name.deleter
    def name(self): ...
```
Notice: Descriptor is another class. They just intercept the methods in the descriptor class INSTANCE

