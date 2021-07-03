---
title: Things You're doing wrong in Python
date: 2021-07-03
tags: [programming, python]
image: python.png
---

Avoid these things in Python to write better code and make better software. <!--more-->

## 1. Not using _if \_\_name\_\_ == '\_\_main\_\_'_

Let's say, you have written a very useful function and tested it by running the file.

```python
import time

def timer():
    for i in range(100):
        print(i)
        time.sleep(1)

timer()
```

Apparently, nothing seems wrong. However, since this function is so useful, you start importing it into other projects. This importing will cause problems because, with each import, the timer is going to start executing. 

To block the file from executing code, we should use _if \_\_name\_\_ == '\_\_main\_\_'_.

```python
import time

def timer():
    for i in range(100):
        print(i)
        time.sleep(1)

if __name__ == '__main__':
    timer()
```

Now we can run the file individually and also import our timer in other py files without side effects.

## 2. Using bare excepts

Let's say we want to handle errors.

```python
while:
    try:
        doing_something()
    except:
        print("Oops! Something went wrong.)
```

When you run this code, you cannot stop it using a KeyboardInterrupt (<kbd>ctrl</kbd> + <kbd>c</kbd>) because the except block handles this interrupt and the loop continues. 

If you mention the type of exception then this can be avoided.

```python
while:
    try:
        doing_something()
    except Exception:
        print("Oops! Something went wrong.)
```

KeyboardInterrupt is not handled by the Exception class. So now you can stop the program using <kbd>ctrl</kbd> + <kbd>c</kbd>.

## 3. Not Using Sets instead of Lists

Let's say we want to check the membership of a value in a group. The following dummy code simulates searching 100 names in a long list of names.

```python
# names.txt contains a million names
with open('names.txt') as f:
    names = f.readlines()

def search_in_names():
    ret = []
    for i in range(100):
        ret.append(str(i) in names)
    return ret

search_in_names()
# Execution time: 2s
```

The problem here is that searching in lists is slow. It can be made faster using a list.

```python
# names.txt contain a million names
with open('names.txt') as f:
    names = set(f.readlines())

def search_in_names():
    ret = []
    for i in range(100):
        ret.append(str(i) in names)
    return ret

search_in_names()
# Execution time: <0.1s
```

There you go! Now you're a little bit better and a little bit wiser in Python.

## 4. Using len() to check empty list

A python newbie may check the emptiness of a list with the following

```python
if len(names) > 0:
    print(names)
```

This can be done better. The len() function is not required. The following will work as well.

```python
if names:
    print(names)
```

## 5. Evaluating Multiple Conditions

If you're coming from another programming language, you might be using multiple conditions the following way.

```python
if 1 < a and a < 4:
    # do something
```

But you can do better.

```python
if 1 < a < 4:
    # do something 
```

#### 5.1 Bonus for multiple conditions!

For multiple conditions inside _if_ statements you can use the following tricks.

Instead of

```python
if b == "Mon" or b == "Wed" or b == "Fri" or b == "Sun":
    # do something
```

Do

```python
if b in "Mon Wed Fri Sun".split():
    # do something 
```

And, instead of 

```python
if a < 10 and b > 5 and c == 4:
    # do something

if a < 10 or b > 5 or c == 4:
    # do something
```

Do

```python
if all([a < 10, b > 5, c == 4]):
    # do something

if any([a < 10, b > 5, c == 4]):
    # do something
```