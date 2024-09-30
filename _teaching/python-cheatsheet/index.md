---
title: "🚀 Python CheatSheet"
permalink: /teaching/python-cheatsheet/
author_profile: true
---

Here's the cheat sheet formatted in Markdown code snippets:

## First Start
- **print()**: Outputs text to the console.
  ```python
  print("Hello, World!")
  ```

## Operations and Variables
- **Operations**: 
  - `+` (addition): `2 + 3` results in `5`
  - `-` (subtraction): `5 - 2` results in `3`
  - `*` (multiplication): `4 * 3` results in `12`
  - `/` (division): `10 / 2` results in `5.0`
  - `**` (exponentiation): `2 ** 3` results in `8`
  - `//` (floor division): `7 // 2` results in `3`
  - `%` (modulus): `10 % 3` results in `1`
  
- **Variable Assignment**: Assigns a value to a variable.
  ```python
  x = 10
  ```

- **Variable Types**: 
  - `int`: `x = 5`
  - `float`: `y = 5.0`
  - `str`: `name = "Alice"`
  - `bool`: `is_active = True`
  
- **type()**: Returns the type of a variable.
  ```python
  type(x)  # Returns <class 'int'>
  ```

- **Comparison Operators**: 
  - `==`: Equal
  - `>`: Greater than
  - `<`: Less than
  - `>=`: Greater than or equal to
  - `<=`: Less than or equal to
  ```python
  x == 10  # True
  ```

## Input and Casting
- **input()**: Gets user input.
  ```python
  name = input("Enter your name: ")
  ```

- **Casting**: Converts between types.
  ```python
  num_str = "10"
  num_int = int(num_str)  # Converts to int
  ```

## Strings
- **lower()**: Converts to lowercase.
  ```python
  "HELLO".lower()  # 'hello'
  ```

- **len()**: Returns length of string.
  ```python
  len("Python")  # 6
  ```

- **capitalize()**: Capitalizes the first letter.
  ```python
  "hello".capitalize()  # 'Hello'
  ```

- **upper()**: Converts to uppercase.
  ```python
  "hello".upper()  # 'HELLO'
  ```

- **title()**: Capitalizes the first letter of each word.
  ```python
  "hello world".title()  # 'Hello World'
  ```

- **strip()**: Removes leading/trailing whitespace.
  ```python
  "  hello  ".strip()  # 'hello'
  ```

- **replace()**: Replaces a substring.
  ```python
  "Hello World".replace("World", "Python")  # 'Hello Python'
  ```

- **count()**: Counts occurrences of a substring.
  ```python
  "banana".count("a")  # 3
  ```

- **isalpha()**: Checks if all characters are alphabetic.
  ```python
  "Hello".isalpha()  # True
  ```

- **isdigit()**: Checks if all characters are digits.
  ```python
  "123".isdigit()  # True
  ```

- **isalnum()**: Checks if all characters are alphanumeric.
  ```python
  "Hello123".isalnum()  # True
  ```

- **in**: Checks if a substring exists in a string.
  ```python
  "Hello" in "Hello World"  # True
  ```

- **Concatenation**:
  - Using `+`: 
  ```python
  "Hello" + " World"  # 'Hello World'
  ```
  - Using `,`: 
  ```python
  print("Hello", "World")  # 'Hello World'
  ```
  - **f-string**: 
  ```python
  name = "Alice"
  f"Hello, {name}!"  # 'Hello, Alice!'
  ```

- **String Slicing**:
  ```python
  text = "Hello"
  text[1:4]  # 'ell'
  ```

## Control Flow
- **if/else**:
  ```python
  if x > 10:
      print("Greater")
  else:
      print("Not greater")
  ```

- **if/elif/else**:
  ```python
  if x > 10:
      print("Greater")
  elif x == 10:
      print("Equal")
  else:
      print("Less")
  ```

## Loops
- **for loop**:
  ```python
  for i in range(5):
      print(i)  # 0 to 4
  ```

- **while loop**:
  ```python
  count = 0
  while count < 5:
      print(count)
      count += 1  # 0 to 4
  ```

## Lists
- **Creation**:
  ```python
  my_list = [1, 2, 3]
  ```

- **len()**: 
  ```python
  len(my_list)  # 3
  ```

- **Slicing**:
  ```python
  my_list[0:2]  # [1, 2]
  ```

- **remove()**: 
  ```python
  my_list.remove(2)  # [1, 3]
  ```

- **pop()**: 
  ```python
  my_list.pop()  # Removes and returns the last item (3)
  ```

- **clear()**: 
  ```python
  my_list.clear()  # []
  ```

- **append()**: 
  ```python
  my_list.append(4)  # [4]
  ```

- **extend()**: 
  ```python
  my_list.extend([5, 6])  # [4, 5, 6]
  ```

- **List Comprehension**:
  ```python
  squares = [x**2 for x in range(5)]  # [0, 1, 4, 9, 16]
  ```

## File I/O
- **open**: Opens a file.
  ```python
  file = open('file.txt', 'r')  # Opens for reading
  ```

- **close**: Closes a file.
  ```python
  file.close()
  ```

- **open with 'with'**:
  ```python
  with open('file.txt', 'r') as file:
      content = file.read()
  ```

- **read()**: Reads the entire file.
  ```python
  content = file.read()
  ```

- **readline()**: Reads one line.
  ```python
  line = file.readline()
  ```

- **readlines()**: Reads all lines into a list.
  ```python
  lines = file.readlines()
  ```
```

You can copy and paste this Markdown code into any Markdown-compatible editor or viewer to see the formatted output. Let me know if you need any more assistance!