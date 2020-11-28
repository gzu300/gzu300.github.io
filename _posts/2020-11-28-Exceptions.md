---
title:  Exceptions
date:  2020-11-28
---

## Exceptions are objects

```Exception``` is the super class for user-defined exceptions. It's meant for non-system-exit errors. ```BaseException``` is just a frame for exceptions. We shouldn't directly use it.

## workflows for try/exception/else/finally

```python
try:
    func() #This function might raise error
except MyError1:
    ... #Error1 is catched here
except MyError2 as error2:
    ... #for error2
except (MyError3, MyError4) as error3_4:
    ... # catch multiple errors
else:
    ... # when no errors are raised in try block
finally:
    ... # Always execute this 'clean up' process before else or except clause
```
1. nested exceptions = ```except (eror1, error2...)```
2. exception clause always exits at the last ```except```
3. finally clause always go through all ```finally``` till the first
## Exceptions are not only for error
### try/finally can be used for workflow that needs 'clean up'

1. I/O ```file.close()```
2. Server curser ```commit``` or ```roll back```
3. Multi-threads ```threading.Lock()```

### try/else clauses for workflows that return only meaningful results

```python
def search():
    if succeed:
        return item
    else:
        raise MyError()
try:
    item = search()
except MyError():
    do_something_else()
else:
    process(item)
```

### general try/except for programs meant to run forever, like server.

## Inherit same type of exception. So same parent exception can intercept them all.

### Intercept all w/o changing code
```python
class Error1(ValueError): pass
class Error2(ValueError): pass

try:
    func() # raise Error1 or Error2
Except ValueError:
    print('error caught')
```

### Use sys.exc_info() for specific error
