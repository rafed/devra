---
title: "A better dictionary in python"
date: 2021-04-23
tags: [programming, python]
image: dictionary.jpg
---

A Python dictionary is a very useful data structure that stores key value pairs. A python dictionary is declared like the following

```python
_dict = {}
```

Although this dictionary does its job well, we can do something better and I'm gonna show you how.

But first, consider the following statements for a problem.
1. We have a list of numbers
1. We want to count the occurrence of each number

Pythonistas would solve it using a dictionary like the following snippet

```python {hl_lines=["5-6"]}
nums = [1, 2, 2, 3, 3, 3]
counter = {}

for num in nums:
    if num not in counter:
        counter[num] = 0
    
    counter[num] += 1

print(counter)
```

Notice that, in the highlighted section, we had to check whether the value does not exist in the dictionary yet. Without this check, we would get an error if we we tried to increment.

We can write a better code than the above snippet.

By using **defaultdict** we can omit to check whether a key already exists in a dictionary.

```python
from collections import defaultdict

nums = [1, 2, 2, 3, 3, 3]
counter = defaultdict(lambda: 0)

for num in nums:
    counter[num] += 1

print(counter)
```

defaultdict takes one argument, which is, the function that returns the default value. In the above case, we passed a lambda function that returns 0 when an item is not found.

Now, instead of writing extra code to check whether an element exists, we can let the dictionaries handle it themselves and do their thing!
