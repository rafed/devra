---
title: "Tips & Tricks to Make Python Faster!"
date: 2021-02-26
tags: [programming, python]
image: python.png
---

Python is known for being slow in terms of execution speed. However, you can try out the following tricks to make your code faster.

Ways to improve:

1. Identify slow functions and improve them
1. Use a cache
1. Use numba
1. Use generators
1. Other tips

## 1. Identify slow functions and improve them

The first rule of optimization is to not do it. It's best to finish implementing business logic and then finding out bottlenecks in the code.

We do this with a technique called profiling.

Let's say we want to profile the following code (in _code.py_).

```python
def fib(x):
    if x==0: return 0
    if x==1: return 1
    return fib(x-1) + fib(x-2)

def loop(x):
    total = 0
    for i in range(x):
        total += i
    return total

print(fib(20))
print(loop(9999999))
```

Instead of manually figuring out functions that could be bottlenecks, lets run the profiler to automatically do it for us. In the terminal, run-

```bash
$ python3 -m cProfile -s time code.py
```

and the output should be something like this-

```text
         21897 function calls (7 primitive calls) in 0.603 seconds

   Ordered by: internal time

   ncalls  tottime  percall  cumtime  percall filename:lineno(function)
        1    0.597    0.597    0.597    0.597 code.py:6(loop)
  21891/1    0.006    0.000    0.006    0.006 code.py:1(fib)
        1    0.000    0.000    0.603    0.603 code.py:1(<module>)
        2    0.000    0.000    0.000    0.000 {built-in method builtins.print}
        1    0.000    0.000    0.603    0.603 {built-in method builtins.exec}
        1    0.000    0.000    0.000    0.000 {method 'disable' of '_lsprof.Profiler' objects}
```

Notice the **ncalls** and **tottime** values. **ncalls** shows the number of times a function has been called and **tottime** shows the total time of execution of a function. By observing these values of all the functions in your code you can start thinking about which functions need to be optimized. For example, the _loop_ function took 0.595s to run and it was called 1 time. The _fib_ function took much lesser time to run (0.006s) but it was called 21891 times. It may need to be improved as it is a function that is being called numerous times.


## 2. Use a Cache

It is possible to cache the return values of heavily used functions.

```python
import functools
import time

# caching up to 10 different results
@functools.lru_cache(maxsize=10)
def foo(x):
    time.sleep(2) ## Simulates heavy computation
    return x+1

foo(5)
foo(5)
```

The foo function simulates a time consuming operation. The first time it is called, the function will take 2 seconds to execute. However, when it is called the second time with the same argument, the result will be returned immediately as the first result was cached.

Note: the function must be a pure function to make it cacheable. That is, for the same arguments passed, it must always return the same value. Caching on non pure functions will show erratic behavior.

## 3. Use Numba

Numba is a library that makes Python fast. To use it, install llvm and numba-

```bash
$ sudo apt-get install llvm
$ pip3 install numba
```

Extensive computation without numba.

```python
# time taken: 6.508s
def computeSum(size):
    sum = 0
    for i in range(size):
        sum += i
    return sum

s = 10000
for _ in range(s):
    sum = computeSum(s)
```

Same code using numba.

```python
## time taken: 1.049s
import numba

@numba.jit
def computeSum(size):
    sum = 0
    for i in range(size):
        sum += i
    return sum

s = 10000
for _ in range(s):
    sum = computeSum(s)
```

Numba can take your python code almost as close to the performance of C.

## 4. Use Generators

The following list comprehension is not memory efficient as it consumes a big chunk of memory.

```python
sum([num**2 for num in range(1000000)])
```

Converting the above to a generator expression-

```python
sum((num**2 for num in range(1000000)))
```

The sum can now be computed without building the entire list and holding it in memory.

## 5. Other Tips

#### a. Use built-in data types

Built-in data types are faster in comparison with custom-made data types (such as linked lists, trees, etc). This is because the internal data structures are implemented in C.

#### b. Optimizing string operations

Performing string operations inside a loop can be expensive using functions like _.format()_ or _% (modulus)_. F-strings can provide faster string operations and they are also more readable.

```python
name = "Rafed"
print(f"My name is {name}")
```

#### c. Use local variables instead of global variables

Accessing local variables is faster than accessing global variables.

#### d. Reduce dot operations

Accessing attributes using dot operations can reduce performance. 

This is slower-

```python
import math

for i in range(10):
    print(math.sqrt(i))
```

This is faster

```python
from math import sqrt

for i in range(10):
    print(sqrt(i))
```

#### e. For over While

_For_ loops are much faster than _while_ loops.


## Conclusion

Now go out there and write faster python code. Impress your friends with your improved code speed and slam the haters who say python is slow. 