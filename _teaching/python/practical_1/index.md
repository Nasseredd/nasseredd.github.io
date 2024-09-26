---
title: "Basics (Operations and Variables)"
permalink: /teaching/python/practical_1/
author_profile: true
---

# First steps

### Exercise 1 ★

Write a program that prints the sentence `'Hello, World!'`.

<details>
  <summary>Solution</summary>

  <pre><code>
print("Hello, World!")
  </code></pre>
</details>

### Exercise 2 ★

Write a program that prints the number `42`.

<details>
  <summary>Solution</summary>

  <pre><code>
print(42)
  </code></pre>
</details>

### Exercise 3 ★

Write a program that prints the string `'42'`.

<details>
  <summary>Solution</summary>

  <pre><code>
print("42")
  </code></pre>
</details>

# Basic Operations

---

### Exercise 4 ★

Write a Python program that adds two numbers.

<details>
  <summary>Solution</summary>

  <pre><code>
5 + 3
  </code></pre>
</details>

### Exercise 5 ★

Write a Python program that subtracts one number from another.

<details>
  <summary>Solution</summary>

  <pre><code>
10 - 2
  </code></pre>
</details>

### Exercise 6 ★

Write a Python program that multiplies two numbers.

<details>
  <summary>Solution</summary>

  <pre><code>
5 * 7
  </code></pre>
</details>

### Exercise 7 ★

Write a Python program that divides one number by another (floating-point division).

<details>
  <summary>Solution</summary>

  <pre><code>
8/4
  </code></pre>
</details>

### Exercise 8 ★

Write a program that calculates the cube of the number 7.

<details>
  <summary>Solution</summary>

  <pre><code>
7**3
  </code></pre>
</details>

### Exercise 9 ★

You are planting a garden, and each plant needs 3 feet of space in every direction. If you have a square garden with sides of length 8 feet, how many square feet of space do you have for planting? Write a program to calculate the area of the square garden using an exponent.

💡 Hint: $Area = side\;length^2$

<details>
  <summary>Solution</summary>

  <pre><code>
8**2
  </code></pre>
</details>

### Exercise 10 ★

Write a program that performs floor division between 15 and 4.

💡 The **floor division** is the integer part of the quotient. For instance, let 7/2 = 3.5. The quotient is 3.5, and the integer part of the quotient is 3.

<details>
  <summary>Solution</summary>

  <pre><code>
15//4
  </code></pre>
</details>

### Exercise 11 ★

Write a program that computes the remainder of the division between 15 and 4.

💡 The **remainder** is the part left over after dividing one number by another when the division does not result in an integer.

<details>
  <summary>Solution</summary>

  <pre><code>
15%4
  </code></pre>
</details>

### Exercise 12 ★★

You have 98 eggs. Write a program that calculates how many dozens (12 eggs) you have and how many eggs remain. Print each result of each operation on a separate line.

<details>
  <summary>Solution</summary>

  <pre><code>
print(98//12)
print(98%12)
  </code></pre>
</details>

### Exercise 13 ★★

You have 145 candies to distribute equally among 8 children. Write a program that calculates and prints how many candies each child gets and how many are left over. Print the result of each operation on a separate line.

<details>
  <summary>Solution</summary>

  <pre><code>
print(145//8)
print(145%8)
  </code></pre>
</details>

### Exercise 14 ★★

Write a program that computes and prints the tens place and ones place of the number `57` using `//` and `%`.

💡 The **tens** place of a number represents how many full sets of ten are in the number (e.g., Tens place of 63 is 6). The **ones** place represents the leftover units after accounting for the tens (e.g., Ones place of 63 is 3).

<details>
  <summary>Solution</summary>

  <pre><code>
print(57//10)
print(57%10)
  </code></pre>
</details>

### Exercise 15 ★★★

Write a program that computes the tens place of the number `657` using `//` and `%`.

💡 The tens place of `657` is `5`.

<details>
  <summary>Solution</summary>

  <pre><code>
(657%100)//10
  </code></pre>
</details>

### Exercise 16 ★★★

Bonus: Write a program that calculates the sum of the digits in the number `357` using `//` and `%`.

💡 3+5+7 = 15

<details>
  <summary>Solution</summary>

  <pre><code>
(357//100) + ((357%100)//10) + (357%10)
  </code></pre>
</details>
