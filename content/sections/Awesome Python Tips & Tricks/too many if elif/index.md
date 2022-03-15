---
title: "Reduce Too Many if-elif in Python"
date: 2022-03-14
tags: [programming, python]
image: featured.png
---

```if-elif``` statements are one of the used features of Python. However, they can become hard to read when the number of ```elif``` statements increase. Let's consider the following code for a game:

```python
# Assume run(), stop(), shoot(), guard() methods are defined

command = input()

if command == "run"
    run()
elif command == "stop"
    stop()
elif command == "shoot"
    shoot()
elif command == "guard"
    guard()
...
...
...
```

There are multiple actions that our protagonist can do. Additionally, the game devs are planning to add more actions for the protagonist. Soon this action list will become big and hard to read.

We can simplify these conditionals using a dictionary. Here's how:

```python
command_dict = {
    "run": run,
    "stop": stop,
    "shoot": shoot,
    "guard": guard,
}

command = input()
command_dict[command]
```

The code is now shortened by a great deal. It is also more readable and easier to modify now.

If the functions need to receive paramaters then modify the above code to

```python
command_dict = {
    "run": run,
    "stop": stop,
    "shoot": shoot,
    "guard": guard,
}

command = input()
x = input()
command_dict[command](x)
```

And that's it! You now have a more readable and maintainable ```if-elif``` system in your code.