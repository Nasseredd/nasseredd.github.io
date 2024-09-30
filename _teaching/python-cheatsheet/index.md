---
title: "🚀 Python CheatSheet"
permalink: /teaching/python-cheatsheet/
author_profile: true
---

Here's the cheat sheet formatted in Markdown code snippets:

## First Start
- **print()**: Outputs text to the console.
    <pre><code>  print("Hi Nasser!")</code></pre>

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
    <pre><code>  x = 10</code></pre>


- **Variable Types**: 
  - `int`: `x = 5`
  - `float`: `y = 5.0`
  - `str`: `name = "Alice"`
  - `bool`: `is_active = True`
  
- **type()**: Returns the type of a variable.
    <pre><code>  type(x)  # Returns <class 'int'></code></pre>

- **Comparison Operators**: 
  - `==`: Equal
  - `>`: Greater than
  - `<`: Less than
  - `>=`: Greater than or equal to
  - `<=`: Less than or equal to
    <pre><code>  x == 10  # True</code></pre>

## Input and Casting
- **input()**: Gets user input.
    <pre><code>  name = input("Enter your name: ")</code></pre>

- **Casting**: Converts between types.
    <pre><code>  num_str = "10"
    num_int = int(num_str)  # Converts to int</code></pre>

## Strings
- **lower()**: Converts to lowercase.
    <pre><code>  "HELLO".lower()  # 'hello'</code></pre>

- **len()**: Returns length of string.
    <pre><code>  len("Python")  # 6</code></pre>

- **capitalize()**: Capitalizes the first letter.
    <pre><code>  "hello".capitalize()  # 'Hello'</code></pre>

- **upper()**: Converts to uppercase.
    <pre><code>  "hello".upper()  # 'HELLO'</code></pre>

- **title()**: Capitalizes the first letter of each word.
    <pre><code>  "hello world".title()  # 'Hello World'</code></pre>

- **strip()**: Removes leading/trailing whitespace.
    <pre><code>  "  hello  ".strip()  # 'hello'</code></pre>

- **replace()**: Replaces a substring.
    <pre><code>  "Hello World".replace("World", "Python")  # 'Hello Python'</code></pre>

- **count()**: Counts occurrences of a substring.
    <pre><code>  "banana".count("a")  # 3</code></pre>

- **isalpha()**: Checks if all characters are alphabetic.
    <pre><code>  "Hello".isalpha()  # True</code></pre>

- **isdigit()**: Checks if all characters are digits.
    <pre><code>  "123".isdigit()  # True</code></pre>

- **isalnum()**: Checks if all characters are alphanumeric.
    <pre><code>  "Hello123".isalnum()  # True</code></pre>

- **in**: Checks if a substring exists in a string.
    <pre><code>  "Hello" in "Hello World"  # True</code></pre>

- **Concatenation**:
  - Using `+`: 
    <pre><code>  "Hello" + " World"  # 'Hello World'</code></pre>
  - Using `,`: 
    <pre><code>  print("Hello", "World")  # 'Hello World'</code></pre>
  - **f-string**: 
    <pre><code>  name = "Alice"
    f"Hello, {name}!"  # 'Hello, Alice!'</code></pre>

- **String Slicing**:
    General syntax: ```string[start:end:step]```
    <pre><code>  text = "Hello"
    text[1:4]  # 'ell'</code></pre>

## Control Flow
- **if/else**:
    <pre><code>  if x > 10:
        print("Greater")
    else:
        print("Not greater")</code></pre>

- **if/elif/else**:
    <pre><code>  if x > 10:
        print("Greater")
    elif x == 10:
        print("Equal")
    else:
        print("Less")</code></pre>

## Loops
- **for loop**:
    <pre><code>  for i in range(5):
        print(i)  # 0 to 4</code></pre>

- **while loop**:
    <pre><code>  count = 0
    while count < 5:
        print(count)
        count += 1  # 0 to 4</code></pre>

## Lists
- **Creation**:
    <pre><code>  my_list = [1, 2, 3]</code></pre>

- **len()**: 
    <pre><code>  len(my_list)  # 3</code></pre>

- **Slicing**:
    <pre><code>  my_list[0:2]  # [1, 2]</code></pre>

- **remove()**: 
    <pre><code>  my_list.remove(2)  # [1, 3]</code></pre>

- **pop()**: 
    <pre><code>  my_list.pop()  # Removes and returns the last item (3)</code></pre>

- **clear()**: 
    <pre><code>  my_list.clear()  # []</code></pre>

- **append()**: 
    <pre><code>  my_list.append(4)  # [4]</code></pre>

- **extend()**: 
    <pre><code>  my_list.extend([5, 6])  # [4, 5, 6]</code></pre>

- **List Comprehension**:
    <pre><code>  squares = [x**2 for x in range(5)]  # [0, 1, 4, 9, 16]</code></pre>

## File I/O
- **open**: Opens a file.
    <pre><code>  file = open('file.txt', 'r')  # Opens for reading</code></pre>

- **close**: Closes a file.
    <pre><code>  file.close()</code></pre>

- **open with 'with'**:
    <pre><code>  with open('file.txt', 'r') as file:
        content = file.read()</code></pre>

- **read()**: Reads the entire file.
    <pre><code>  content = file.read()</code></pre>

- **readline()**: Reads one line.
    <pre><code>  line = file.readline()</code></pre>

- **readlines()**: Reads all lines into a list.
    <pre><code>  lines = file.readlines()</code></pre>

## Dictionaries
- **Create a Dictionary**:
    <pre><code>  my_dict = {
        "name": "Alice",
        "age": 30,
        "city": "New York"
    }</code></pre>

- **Access a Value in a Dictionary**:
    <pre><code>  age = my_dict["age"]  # 30</code></pre>

- **pop(key)**: Removes the specified key and returns its value.
    <pre><code>  city = my_dict.pop("city")  # 'New York'</code></pre>

- **items()**: Returns a view object containing the key-value pairs.
    <pre><code>  items = my_dict.items()  # dict_items([('name', 'Alice'), ('age', 30)])</code></pre>

- **keys()**: Returns a view object containing the dictionary's keys.
    <pre><code>  keys = my_dict.keys()  # dict_keys(['name', 'age'])</code></pre>

- **values()**: Returns a view object containing the dictionary's values.
    <pre><code>  values = my_dict.values()  # dict_values(['Alice', 30])</code></pre>

- **update()**: Updates the dictionary with elements from another dictionary or from an iterable of key-value pairs.
    <pre><code>  my_dict.update({"age": 31, "country": "USA"})</code></pre>


## Functions
- **Create a Function**:
    <pre><code>  def greet(name):
        return f"Hello, {name}!"</code></pre>

- **Call the Function**:
    <pre><code>  message = greet("Alice")  # 'Hello, Alice!'</code></pre>

- **Function with No Arguments**:
    <pre><code>  def say_hello():
        print("Hello, World!")
  
  say_hello()  # Outputs: Hello, World!</code></pre>

- **Function with a Flexible Number of Arguments (`*args`)**:
    <pre><code>  def add_numbers(*args):
        return sum(args)

  result = add_numbers(1, 2, 3, 4)  # 10</code></pre>

- **Function with Keyword Arguments (`**kwargs`)**:
    <pre><code>  def print_info(**kwargs):
        for key, value in kwargs.items():
            print(f"{key}: {value}")

  print_info(name="Alice", age=30)  
  # Outputs:
  # name: Alice
  # age: 30</code></pre>

- **Function with Default Arguments**:
    <pre><code>  def greet(name="Guest"):
        return f"Hello, {name}!"

  message1 = greet("Alice")  # 'Hello, Alice!'
  message2 = greet()          # 'Hello, Guest!'</code></pre>

- **Function Returning Multiple Values**:
    <pre><code>  def get_user_info():
        return "Alice", 30

    name, age = get_user_info()  # name = 'Alice', age = 30</code></pre>

- **Lambda Function**: A small anonymous function.
    <pre><code>  square = lambda x: x ** 2
    result = square(5)  # 25</code></pre>

- **Function Documentation**: Use docstrings to document the function.
    <pre><code>  def multiply(x, y):
        """Multiply two numbers and return the result."""
        return x * y

    print(multiply.__doc__)  # 'Multiply two numbers and return the result.'</code></pre>

- **Higher-Order Functions**: Functions that take other functions as arguments.
    <pre><code>  def apply_function(func, value):
        return func(value)

    result = apply_function(square, 10)  # 100</code></pre>