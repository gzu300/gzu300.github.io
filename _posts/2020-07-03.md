---
title: Interpreter
---

'Interpreter' is heard everywhere when programming python. For example, they always mention about Interpreters for CPython and Pypy... But unfortunately it has been carefully studied so it coufuses me all the time. Now let's make it clear.

When we say 'I program in python', we usually refer to the syntax of python code. Python itself should actually be called python interpreter. It is a layer of software logic between our code and computer. It essentially reads the program we wrote and execute it. It's just interpreters can be implemented, like different flavors, by C, Java or now python itself.

So how does python interpreter execute the program? The below steps even though now explicitly stated, it should be C-flavored python, Cpython.  
1. __Byte Code compilation__. Byte code is a low level that can be run faster by computer. python interpreter will first compile the script into byte code, which is .pyc file provided the interepreter has the write access. So for large program .pyc files speed up the execution.  
2. __Python Virtual Machine__. It is the runtime engine of python that actually runs the program. The PVM still needs to interpret the byte code then goes to chip. So it's slower than C and C++.

Cpython is the classic implementation of python. There are also Jpython and Ironpython. Now there is Pypy. For Cpython, Jpython and Ironpython, the execution is similar. compile and execute. But the newer interpreter Pypy is different. It has the Just-in-time compiler which compiles the code while running the script. So it's much faster than the others. To notice that pypy only accepts pure python modules so modules with c exetensions will not work or need work around.
