---
title: "Powerful Python One Liners"
date: 2021-02-20
tags: [programming, python]
image: python.png
---

Why write more code when you can write less? Become a Python Ninja with the below one-liners. <!--more-->

#### 1. Swapping variables

```python
a, b = b, a
```

#### 2. Assigning multiple values

```python
a, b, c = 10, 20, 30
```

#### 3. Create a list

```python
## Instead of this
nums = []
for i in range(10):
    nums.append(i)
```

```python
## DO THIS
nums = [i for i in range(10)]
```
#### 4. Take subset of a list

```python
nums = [1, 2, 3, 4, 5, 6]
b = [num for num in nums if num%2 == 0]
```

#### 5. Shorten if/else (with ternary operator)

```python
## Instead of this
if age<20:
    print("Young")
else:
    print("Old")
```

```python
## DO THIS
print("Young") if age<20 else print("Old")
```

#### 6. Reverse a string/list

```python
>>> s = "GMO"
>>> s[::-1]
"OMG"
```

#### 7. Check palindrome

```python
>>> s = "madam"
>>> s == s[::-1]
True
```

#### 8. Take input in one line

```python
## Instead of this
a = input()
b = input()
c = input()
```

```python
## DO THIS
a, b, c = input().split(' ')
```

```python
## If type casting is needed then, (from string to int)-
a, b, c = [int(x) for x in input().split(' ')]
```

#### 9. Read a file

```python
f = [line for line in open("filename")]
```

#### 10. Generate groups

```python
>>> groups = [(a, b) for a in ['a', 'b'] for b in [1, 2, 3]] 
>>> groups
[(a, 1), (a, 2), (a, 3), (b, 1), (b, 2), (b, 3)]
```

#### 11. Generator expression

```python
nums = [x for x in range(10)]

## Instead of this
def number_generator(list):
    for item in list:
        yield item

>>> g = number_generator(nums)
>>> next(g)
0
```

```python
## DO THIS
>>> nums = [x for x in range(10)]
>>> g = (n for n in nums)
>>> next(g)
0
```

## Conclusion

One-liners look cool and it does make code smaller. However, it might not be the best idea to always use them. One-liners can make code hard to read. Additionally, they might not always be the most memory efficient. If your code needs to be more readable/maintainable, avoid complex one-liners in favor of longer but readable code.