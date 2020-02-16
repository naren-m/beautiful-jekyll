---
layout: post
title: Fibonacci Sequence
subtitle: Fibonacci Sequence
published: true
---

{% include mathjax.html %}

# Fibonacci Sequence

- [Fibonacci Sequence](#fibonacci-sequence)
	- [Some properties of Fibonacci numbers](#some-properties-of-fibonacci-numbers)
		- [Golden ratio (φ)](#golden-ratio-%cf%86)
		- [Every nth number if multiple of fib(n)](#every-nth-number-if-multiple-of-fibn)
		- [Exact divisibility of fib(n)](#exact-divisibility-of-fibn)
	- [Finding Nth term of a Fibonacci sequence](#finding-nth-term-of-a-fibonacci-sequence)
		- [Using golden ratio](#using-golden-ratio)
		- [Power of matrix {{1, 1}, {1, 0}}](#power-of-matrix-1-1-1-0)

Fibonacci sequence is a series of numbers, where each number is the sum of previous 2 numbers.

Ex: 0, 1, 1, 2, 3, 5, 8, 13, 21, 34 …

## Some properties of Fibonacci numbers

### Golden ratio (φ)

The ratio of the fibonacci numbers are close to the golden ratio. `φ = 1.618…`

```math
3/2  = 1.5
5/3  = 1.666
8/5  = 1.6
13/8 = 1.625
...
233/144 = 1.618055...
377/233 = 1.618025...
```

### Every nth number if multiple of fib(n)

|n=     |0  |1  |2  |3  |4  |5  |6  |7  |8  |9  |10 |11 |
|—|-|-|-|-|-|-|-|-|-|-|-|-|
|fib(n) |0  |1  |1  |2  |3  |5  |8  |13 |21 |34 |55 |89 |

- 3rd fibonacci number is 2 and every 3rd number is a multiple of 2
- 4th fibonacci number is 3 and every 4th number is a multiple of 3
- 5th fibonacci number is 5 and every 5th number is a multiple of 5

### Exact divisibility of fib(n)

Two fibonacci numbers are exactly divisible if and only of their indices are exactly divisible

$$
\frac {fib(n)} {fib(m)} = 0
\text{ If and only if }
\frac{n}{m} == 0
$$

## Finding Nth term of a Fibonacci sequence

### Using golden ratio

Phi(φ), golden ratio is a special number.

$$
φ = \frac{(1+ \sqrt{5})}{2} = 1.618034….
$$

Few more equalities for golden ratio,


We can calculate nth term of a fibonacci sequence using a formula,

$$
fib(n) =  \frac{( φ^n - (1-φ)^n)}{\sqrt{5}} \\
fib(6) = (1.61803^6 -  ( -0.61803) ^6) /√5 = 8.000000000000002≃ 8
$$

### Power of matrix {{1, 1}, {1, 0}}

Multiplying the matrix {{1, 1}, {1, 0}} n times my itself, will result in a matrix, whose (0, 1) or (1, 0) element would be the nth fibonacci number.

Base rule of Fibonacci numbers is $f(n) = f(n-1) + f(n-2)$
```
| f(n)   |   =  | f(n-1) + f(n-2) |
| f(n-1) |      | f(n-1) |
```

Above could be represented as,

```
| f(n)   |   =   | 1  1 |  X  | f(n-1) |
| f(n-1) |       | 1  0 |     | f(n-2) |
```

if we represent the matrix as below,

```
F(n) = | f(n)   |
	   | f(n-1) |
```

then the above can be represented as $F(n) = C *  F(n-1)$

And now with recurrence, we can see how we can find the nth fibonacci number by matrix multiplication.

```math
Base case, n = 1
F(1)  = C * F(0)
F(2)  = C * F(1) = C * ( C * F(0)) = C^2 * F(0)
F(3)  = C * F(2) = C^2 * ( C * F(0)) = C^3 * F(0)
. . .
F(n)  = C^n * F(0)
```
$$
\left| \begin{array}{cc} f_{11} & F_{12} \\ x_{21} & x_{22} \end{array} \right|
$$
Formula:

```math
| f(n+1) |   =   | 1  1 |  ^ n
| f(n)   |       | 1  0 |
```
