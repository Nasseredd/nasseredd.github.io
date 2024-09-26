---
title: "Basics (Operations and Variables)"
permalink: /teaching/python/practical_1/
author_profile: true
---

## First steps

### Exercise 1 <span style="color:#F0B815;">★</span>

Write a program that prints the sentence `'Hello, World!'`.
<details>
    <summary>Solution</summary>
    <pre>
        <code>
            print("Hello, World!")
        </code>
    </pre>
</details>

<hr style="border: 1px solid #afada8;">

### Exercise 2 <span style="color:#F0B815;">★</span>

Write a program that prints the number `42`.

<details>
  <summary>Solution</summary>

  <pre><code>
    print(42)
  </code></pre>
</details>

### Exercise 3 <span style="color:#F0B815;">★</span>

Write a program that prints the string `'42'`.

<details>
  <summary>Solution</summary>

  <pre><code>
    print("42")
  </code></pre>
</details>


---

## Basic Operations

### Exercise 4 <span style="color:#F0B815;">★</span>

Write a Python program that adds two numbers.

<details>
  <summary>Solution</summary>

  <pre><code>
5 + 3
  </code></pre>
</details>

### Exercise 5 <span style="color:#F0B815;">★</span>

Write a Python program that subtracts one number from another.

<details>
  <summary>Solution</summary>

  <pre><code>
10 - 2
  </code></pre>
</details>

### Exercise 6 <span style="color:#F0B815;">★</span>

Write a Python program that multiplies two numbers.

<details>
  <summary>Solution</summary>

  <pre><code>
5 * 7
  </code></pre>
</details>

### Exercise 7 <span style="color:#F0B815;">★</span>

Write a Python program that divides one number by another (floating-point division).

<details>
  <summary>Solution</summary>

  <pre><code>
8/4
  </code></pre>
</details>

### Exercise 8 <span style="color:#F0B815;">★</span>

Write a program that calculates the cube of the number 7.

<details>
  <summary>Solution</summary>

  <pre><code>
7**3
  </code></pre>
</details>

### Exercise 9 <span style="color:#F0B815;">★</span>

You are planting a garden, and each plant needs 3 feet of space in every direction. If you have a square garden with sides of length 8 feet, how many square feet of space do you have for planting? Write a program to calculate the area of the square garden using an exponent.

💡 Hint: $Area = side\;length^2$

<details>
  <summary>Solution</summary>

  <pre><code>
8**2
  </code></pre>
</details>

### Exercise 10 <span style="color:#F0B815;">★</span>

Write a program that performs floor division between 15 and 4.

💡 The **floor division** is the integer part of the quotient. For instance, let 7/2 = 3.5. The quotient is 3.5, and the integer part of the quotient is 3.

<details>
  <summary>Solution</summary>

  <pre><code>
15//4
  </code></pre>
</details>

### Exercise 11 <span style="color:#F0B815;">★</span>

Write a program that computes the remainder of the division between 15 and 4.

💡 The **remainder** is the part left over after dividing one number by another when the division does not result in an integer.

<details>
  <summary>Solution</summary>

  <pre><code>
15%4
  </code></pre>
</details>

### Exercise 12 <span style="color:#F0B815;">★★</span>

You have 98 eggs. Write a program that calculates how many dozens (12 eggs) you have and how many eggs remain. Print each result of each operation on a separate line.

<details>
  <summary>Solution</summary>

  <pre><code>
print(98//12)
print(98%12)
  </code></pre>
</details>

### Exercise 13 <span style="color:#F0B815;">★★</span>

You have 145 candies to distribute equally among 8 children. Write a program that calculates and prints how many candies each child gets and how many are left over. Print the result of each operation on a separate line.

<details>
  <summary>Solution</summary>

  <pre><code>
print(145//8)
print(145%8)
  </code></pre>
</details>

### Exercise 14 <span style="color:#F0B815;">★★</span>

Write a program that computes and prints the tens place and ones place of the number `57` using `//` and `%`.

💡 The **tens** place of a number represents how many full sets of ten are in the number (e.g., Tens place of 63 is 6). The **ones** place represents the leftover units after accounting for the tens (e.g., Ones place of 63 is 3).

<details>
  <summary>Solution</summary>

  <pre><code>
print(57//10)
print(57%10)
  </code></pre>
</details>

### Exercise 15 <span style="color:#F0B815;">★★★</span>

Write a program that computes the tens place of the number `657` using `//` and `%`.

💡 The tens place of `657` is `5`.

<details>
  <summary>Solution</summary>

  <pre><code>
(657%100)//10
  </code></pre>
</details>

### Exercise 16 <span style="color:#F0B815;">★★★</span>

Bonus: Write a program that calculates the sum of the digits in the number `357` using `//` and `%`.

💡 3+5+7 = 15

<details>
  <summary>Solution</summary>

  <pre><code>
(357//100) + ((357%100)//10) + (357%10)
  </code></pre>
</details>


---

## Variables and Types (Int, Float, String, Bool)

### Exercise 1 <span style="color:#F0B815;">★</span>

Write a program to declare the following variables:
- `age` with the value `25`
- `price` with the value `19.99`
- `name` with the value `Alice`
- `is_raining` with the value `False`

Each variable on a separate line.

<details>
  <summary>Solution</summary>

  <pre><code>
age = 25
price = 19.99
name = "Alice"  # or 'Alice'
is_raining = False
  </code></pre>
</details>

### Exercise 2 <span style="color:#F0B815;">★</span>

Declare two integers `a` equal to 10 and `b` equal to 20. Then, print their sum and their product. Each operation on a separate line.

<details>
  <summary>Solution</summary>

  <pre><code>
a = 10
b = 20
print(a + b)
print(a * b)
  </code></pre>
</details>

### Exercise 3 <span style="color:#F0B815;">★</span>

Copy the following code and write a program that prints the type of each variable. 
💡 Use the `type()` function!

<pre><code>age = 25
price = 19.99
name = "Alice"  # or 'Alice'
is_raining = False
</code></pre>

<details> <summary>Solution</summary> <pre><code> print(type(age)) # Output: <class 'int'> print(type(price)) # Output: <class 'float'> print(type(name)) # Output: <class 'str'> print(type(is_raining)) # Output: <class 'bool'> </code></pre> </details>

### Exercise 4 <span style="color:#F0B815;">★</span>

Write a program that checks if 7 is greater than 5, assigns the result to a variable named result, and prints the result as a boolean. What is the result? 💡 Hint: you don’t need to use conditions (if/elif/else)!

<details> <summary>Solution</summary> <pre><code> result = 7 > 5 print(result) </code></pre> </details>

### Exercise 5 <span style="color:#F0B815;">★</span>

Write a program that checks if 11 is lower than 7, assigns the result to a variable named result, and prints the result as a boolean. What is the result? 💡 Hint: you don’t need to use conditions (if/elif/else)!

<details> <summary>Solution</summary> <pre><code> result = 11 < 7 print(result) </code></pre> </details>

### Exercise 6 <span style="color:#F0B815;">★</span>

Declare a variable num equal to 10, convert it to a float (assign it to a new variable), and then print the result. 💡 Read about "casting" (or "conversion").

<details> <summary>Solution</summary> <pre><code> num = 10 num_float = float(num) print(num_float) </code></pre> </details>

### Exercise 7 <span style="color:#F0B815;">★</span>

Write a program that:

Declares three variables x, y, and z equal respectively to 10, 11, and 12.
Computes the average and assigns the result to a variable named average.
Prints the average of the three variables.
<details> <summary>Solution</summary> <pre><code> x = 10 y = 11 z = 12 average = (x + y + z) / 3 print(average) </code></pre> </details>

### Exercise 8 <span style="color:#F0B815;">★</span>

Write a program that computes the simple interest as follows:

Declare three variables principal, rate, and time equal respectively to 1000, 5.0, and 3.
Compute the simple interest and assign the result to a variable named interest.
Print the simple interest.
💡 Use this formula: $Interest = \frac{P \times R \times T}{100}$

<details> <summary>Solution</summary> <pre><code> principal = 1000 rate = 5.0 time = 3 interest = (principal * rate * time) / 100 print(interest) </code></pre> </details>

### Exercise 9 <span style="color:#F0B815;">★★</span>

Declare a float variable radius equal to 5.0 and a float variable pi equal to 3.14. Then, compute the area of a circle using the formula $\pi r^2$. Finally, print the area.

<details> <summary>Solution</summary> <pre><code> radius = 5.0 pi = 3.14 area = pi * (radius ** 2) print(area) </code></pre> </details>

### Exercise 10 <span style="color:#F0B815;">★★</span>

Write a program to calculate the compound interest. Declare variables:

principal = 1500
rate = 4.3
time = 6
n = 4 (compounds per year)
Use the formula: $A = P \left( 1 + \frac{R}{100n} \right)^{nt}$

Assign the result to the variable amount and print it.

<details> <summary>Solution</summary> <pre><code> principal = 1500 rate = 4.3 time = 6 n = 4 amount = principal * (1 + (rate / (100 * n))) ** (n * time) print(amount) </code></pre> </details>

### Exercise 11 <span style="color:#F0B815;">★★</span>

Write a program that declares an integer x equal to 10 and prints True if x is equal to 5 * 2, False if it’s not. 💡 You don’t need conditions (if/elif/else).

<details> <summary>Solution</summary> <pre><code> x = 10 print(x == 5 * 2) </code></pre> </details>

### Exercise 12 <span style="color:#F0B815;">★★★</span>

Bonus: Write a program that declares an integer n equal to 15 and prints True if it's even, False if it's odd. 💡 You don’t need conditions (if/elif/else).

<details> 
    <summary>Solution</summary> <pre><code> n = 15 print(n % 2 == 0) </code></pre> </details> ```
This format includes the stars and collapsible solution sections for each exercise as requested!