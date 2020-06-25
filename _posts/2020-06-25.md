---
title: thread, python thread and multi-threading
---

### What is a thread

### _thread module, the low-level module

_thread module provides lower level of threading implementation.  

```python
import _thread
def func(i, exit_signal):
  lock.acquire()
  #body
  lock.release()
  exit_signals[i] = True
  
exit_signals = [False]*5 
lock = _thread.allocate_lock()
for i in range(5):
    thread = _thread.start_new_thread(func, (i,exit_signal))
while False in exit_signal: pass # signals the program to terminate
```

It is not OOP and thread spawn, lock and the time to terminate the program need to be manually acquired. 
Based on _thread module, the new threading module is a higher level module with more features convienent to use.  

a common pattern for the basic use of threading module is:

```python
threads = []
for _ in range(5): # spawn and start new thread
    thread = threading.Thread(target=callable, args=())#target also called action, which can also specifically defined in Thread.run method
    thread.start() 
    threads.append(thread)
    
for each in threads: # wait all the threads to finish
    each.join()
```

### threading with queue module

We could use acquire lock to control the workflow of multiple threads. But a nicer way to manage the flow is by using queue module.
Multi-thread design usually is based on 'producer' and 'consumer' pattern, the basic structure is like:
```python
import threading, queue
q = queue.Queue()
def producer():
    #body
    q.put()#put data in
def consumer():
    while True:
        #body
        try:
            q.get()#get data out
        except queue.Empty:
            pass
def main():          
    for _ in range(n_producers):
        threading.Thread(producer).start()
    for _ i in range(n_consumers):
        threading.Thread(consumer).start()
```
