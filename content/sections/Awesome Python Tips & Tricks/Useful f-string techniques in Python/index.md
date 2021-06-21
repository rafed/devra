---
title: Useful f-string Techniques in Python
date: 2021-06-20
tags: [programming, python]
image: python.png
---

Python f-strings are super useful for formatting strings. Before python 3.6 _str.format()_ were used. But f-strings makes string manipulation much more easier and effective.

#### 0. The simplest way to use f-strings

```python
name = "John"
print("Hello {name}")
# >> "Hello John"
```

#### 1. Equals debugging

```python
num = 5
print("value is {num}")    # value is 5
print("value is {num=}")   # value is num=5
print("value is {num%2=}") # value is num%2=1
```

#### 2. Formatting

```python
num_float = 12.34
now = datetime.datetime.utcnow()
print(f"{now=:%Y-%m-%d}")
print(f"{num_float:.2f}")
```

#### 3. Padding

```python
x = 'test'
print(f"{x:>10}")   # "      test"
print(f"{x:*<8}")   # "test****"
print(f"{x:=^8}")   # "==test=="

# For dynamic padding length
x, n = 'test', 10
print(f"{x:~^{n}}") # '~~~test~~~'
```

#### 4. Base conversion

```python
a = 42
print(f"{a:c}")    # ascii => '*'
print(f"{a:x}")    # hex => '2a'
print(f"{a:X}")    # HEX => '2A'
print(f"{a:o}")    # octal => '52'

print(f"{a:b}")    # binary => '101010'
print(f"{a:010b}") # combined with padding => '0000101010'
```




