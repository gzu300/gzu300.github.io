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
### Factory
The mechanics of Factory Method are:\
Client depends on one concrete implementation of an **interface**. Which concrete implementation to be used is returned and decided by **creator component**. Of course, every concrete implementation should be implemented, as methods or functions.
So elements are:
- client
- creator
- concrete implementations
Here is the example of refactoring a class into factory pattern
```python
#we may endup here for the first versions
class SongSerializer(object):
    def serialize(self, song, format):
        if format == 'JSON':
            song_info = {
                'id': song.song_id,
                'title': song.title,
                'artist': song.artist
            }
            return json.dumps(song_info)
        if format == 'XML':
            song_info = et.Element('song', attrib={'id': song.song_id})
            title = et.SubElement(song_info, 'title')
            title.text = song.title
            artist = et.SubElement(song_info, 'artist')
            artist.text = song.artist
            return et.tostring(song_info, encoding='unicode')
        else:
            raise ValueError(format)

# refactor            
# step 1: move implements to interfaces            
class SongSerializer1(object):
    def serialize(self, song, format): #now this is the client code
        if format == 'JSON': return self._serialize_to_jons(song) #these are the interfaces
        if format == 'XML': return self._serialize_to_xml(song)
        else: raise ValueError(format)
            
    def _serialize_to_jons(self, song): #these are the concrete implementations
        payload = {
                'id': song.song_id,
                'title': song.title,
                'artist': song.artist
            }
        return json.dumps(payload)
    def _serialize_to_xml(self, song):
        song_info = et.Element('song', attrib={'id': song.song_id})
        title = et.SubElement(song_info, 'title')
        title.text = song.title
        artist = et.SubElement(song_info, 'artist')
        artist.text = song.artist
        return et.tostring(song_info, encoding='unicode')
#step 3: With common interface, we could send 'format' as a parameter to control the which concrete implementation to use.
#this is the central idea of Factory pattern.
class SongSerializer2(SongSerializer1): #methods interfaces interited are  product component
    def serialize(self, song, format): #this is the application code. i.e. client component
        serializer = self._get_serializer(format)
        return serializer(song)
    def _get_serializer(self, format):# this is the                        creator component
        serializers = {
            'JSON': self._serialize_to_jons,
            'XML': self._serialize_to_xml
        }
        serializer = serializers.get(format)
        if not serializer:
            raise ValueError(format)
        return serializer
    
#step 3: When methods are not using 'self', seperate them into functions.
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
