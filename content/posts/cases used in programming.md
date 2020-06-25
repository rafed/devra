---
title: Cases used in programming
date: 2020-06-24
tags: [Programming, Software engineering]
---
You've probably heard about following camel cases when naming functions and variables. There are more types of cases out there. In this post, we will discover other cases followed in naming conventions and where they are commonly used.

The cases are:
1. camelCase
1. PascalCase
1. snake_case
1. kebab-case
1. MACRO_CASE

## 1. camelCase

Rules:
- Must start with a lower case alphabet
- All subsequent words must start with a capital letter

Examples: count, findBiggestNumber, add1DayToWeek

Commonly used in:
- Naming variables in **Java, JavaScript**
- Internal variables and methods in **Go**

## 2. PascalCase

Also known as Capital case.

Rules:
- Must start with a capital letter
- All subsequent words must start with a capital letter

Examples: Count, FindBiggestNumber, Add1DayToWeek

Commonly used in:
- Naming namespaces and methods in **C#**
- Public variables and methods in **Go**

## 3. snake_case

Rules:
- All variables should be lower case
- subsequent words should be separated by underscores (_)

Examples: count, find_biggest_number, add_1_day_to_week

Commonly used in:
- Naming variables and functions in **python**
- Naming **files**
- Keys of **JSON** strings: {'first_name': 'John"}


## 4. kebab-case

It's called kebab case because the hyphens are like a skewer going through kebabs.

Rules:
- All variables should be lower case
- Subsequent words should be separated by hyphens (-)

Examples: nav-bar, date-component

Commonly used in:
- **CSS/SCSS**
- **Vue** components

## 5. MACRO_CASE

Rules:
- All variables should be upper case
- Subsequent words should be separated by underscores

Examples: MAX_ITERS, MIN_COUNT

Commonly used in:
- Naming constants in most programming languages
- Naming preprocessors in **C/C++**

## 6. Bonus: 1337 K453 (Leet case)

This is not usually found in programming. It is mostly used by hackers to look cool. You might find it being used a lot in print statements of CLI applications.

Examples: 
- H4X0Rm4N (hackerman)
- r007ed (rooted)
- Checkout [1337.me](https://1337.me/) to turn any phrase to leet code.