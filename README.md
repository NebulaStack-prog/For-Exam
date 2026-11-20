# For-Exam

<img src="https://github.com/NebulaStack-prog/For-Exam/blob/main/ForExam.png" width="200" height="230">

## 1. Number Systems

This section contains a general-purpose algorithm for converting a non-negative decimal integer into a number system with a specified base.

### Implementation

```python
def num_sys(n, base):
    digits = '0123456789ABCDEF'

    if n == 0:
        return '0'

    result = ''
    while n > 0:
        result = digits[n % base] + result
        n //= base

    return result
```

### Supported Bases

The function supports bases from `2` to `16`, including:

* **Base 2** – Binary
* **Base 3** – Ternary
* **Base 4** – Quaternary
* **Base 8** – Octal
* **Base 10** – Decimal
* **Base 16** – Hexadecimal

### Examples

```python
print(num_sys(10, 2))    # 1010
print(num_sys(10, 3))    # 101
print(num_sys(10, 4))    # 22
print(num_sys(10, 8))    # 12
print(num_sys(255, 16))  # FF
```

### How It Works

1. The remainder of `n` divided by `base` determines the last digit of the converted number.
2. Integer division by `base` removes the digit that has already been processed.
3. Each new digit is added to the beginning of the result string.
4. The process continues until `n` becomes zero.

The algorithm extracts digits from right to left and builds the final representation in the correct order.

### Complexity

* **Time complexity:** `O(log_base(n))` iterations for `n > 0`. Building the string through repeated concatenation may require additional time.
* **Space complexity:** `O(log_base(n))` for storing the result.

**Note:** The function returns a string to support hexadecimal digits such as `A`–`F`. It is designed for non-negative integers and bases from `2` to `16`.

## 2. Binary Search

Binary search is an efficient algorithm for finding an element in a sorted array. It works by repeatedly dividing the search interval in half.

### Implementation

```python
def binary_search(arr, target):
    left, right = 0, len(arr) - 1

    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1

    return -1  # Element not found
```

### Examples

```python
data = [1, 3, 5, 7, 9, 11, 13]
print(binary_search(data, 7))   # 3
print(binary_search(data, 4))   # -1
```

### How It Works

1. Compare the target with the middle element.
2. If they are equal, return the index.
3. If the target is smaller, search the left half.
4. If the target is larger, search the right half.
5. Repeat until the element is found or the interval is empty.

### Complexity

* Time complexity: O(log n)
* Space complexity: O(1) (iterative version)

**Note:** The array must be sorted beforehand.

## 3. Recursion and lru_cache

Recursion is a technique where a function calls itself to solve smaller subproblems. In Python, recursion can be slow due to repeated calculations. The functools.lru_cache decorator solves this by storing (caching) the results of function calls.

### Implementation

```python
from functools import lru_cache

@lru_cache(maxsize=None)
def fib(n):
    if n <= 1:
        return n
    return fib(n - 1) + fib(n - 2)
```

### Examples

```python
print(fib(10))   # 55
print(fib(50))   # 12586269025 (works instantly)
```

### How It Works

1. lru_cache memorizes the arguments and the returned value.
2. When the function is called again with the same arguments, the cached result is returned immediately.
3. This reduces the time complexity from exponential to linear.

### Complexity

* Time complexity: O(n) for the Fibonacci example.
* Space complexity: O(n) for the cache.

**Note:** Use lru_cache only for pure functions (functions that return the same result for the same input and have no side effects).

## 4. itertools – Combinations and Permutations

The itertools module provides fast, memory-efficient tools for creating iterators for combinatorial tasks.

### Common Functions

* product() – Cartesian product (with repetition).
* permutations() – Ordered arrangements without repetition.
* combinations() – Unordered selections without repetition.
* combinations_with_replacement() – Unordered selections with repetition.

### Implementation

```python
from itertools import product, permutations, combinations

# Cartesian product: 'ABC' repeated 2 times
a = product('ABC', repeat=2)

# Permutations of length 2 from 'ABC'
b = permutations('ABC', 2)

# Combinations of length 2 from 'ABC'
c = combinations('ABC', 2)
```

### Examples

```python
print(list(product('AB', repeat=2)))
# [('A', 'A'), ('A', 'B'), ('B', 'A'), ('B', 'B')]

print(list(permutations('ABC', 2)))
# [('A', 'B'), ('A', 'C'), ('B', 'A'), ('B', 'C'), ('C', 'A'), ('C', 'B')]

print(list(combinations('ABC', 2)))
# [('A', 'B'), ('A', 'C'), ('B', 'C')]
```

### How It Works

1. The functions return iterators, not lists. This saves memory.
2. Convert to a list with list() if you need to print or access elements multiple times.
3. Elements are returned as tuples.

Note: product performs the Cartesian product, meaning order matters and elements can repeat.

## 5. Converting Recursion to an Array (Dynamic Programming)

Recursion can be rewritten as an iterative loop using an array (usually called dp — dynamic programming). This approach is often faster and avoids recursion depth limits.

### Example: 
Fibonacci Numbers

### Recursive version:

```python
def fib_rec(n):
    if n <= 1:
        return n
    return fib_rec(n - 1) + fib_rec(n - 2)
```

### Iterative version with an array:

```python
def fib_iter(n):
    if n <= 1:
        return n
    dp = [0] * (n + 1)
    dp[0] = 0
    dp[1] = 1
    for i in range(2, n + 1):
        dp[i] = dp[i - 1] + dp[i - 2]
    return dp[n]
```

### How It Works

1. Create an array dp of size n + 1.
2. Set the base cases (dp[0], dp[1]).
3. Fill the array iteratively using the recurrence relation.
4. Return the final answer from dp[n].

### Complexity

* Time complexity: O(n)
* Space complexity: O(n) (can be optimized to O(1) by storing only the last two values)

**Note:** This technique is called dynamic programming and is widely used in competitive programming and exams.

## 6. Stone Pile Game (Game Theory)

A classic game theory problem where two players take turns modifying two piles of stones. The goal is to determine for which starting positions the first player wins or loses.

### Problem Statement (brief)

* Two piles: (x, y).
* A move: increase the smaller pile by 1, by 2, or double the smaller pile.
* The game ends when the total number of stones x + y >= 69 (or another threshold).
* Petya moves first, Vanya moves second.

### Implementation

```python
def f(x, y, pos):
    # Petya's winning strategy (pos = 0, 2)
    if pos == 4:
        return x + y >= 69
    if pos == 2 and x + y >= 69:
        return True
    if (pos == 1 or pos == 3) and x + y >= 69:
        return False

    if pos == 0 or pos == 2:
        return (f(x + 1, y, pos + 1) and
                f(x, y + 1, pos + 1) and
                f(x * 2, y, pos + 1) and
                f(x, y * 3, pos + 1))
    if pos == 1 or pos == 3:
        return (f(x + 1, y, pos + 1) or
                f(x, y + 1, pos + 1) or
                f(x * 2, y, pos + 1) or
                f(x, y * 3, pos + 1))


def g(x, y, pos):
    # Vanya guarantees a win on the first move
    if pos == 2:
        return x + y >= 69
    if pos == 1 and x + y >= 69:
        return False

    if pos == 0:
        return (g(x + 1, y, pos + 1) and
                g(x, y + 1, pos + 1) and
                g(x * 2, y, pos + 1) and
                g(x, y * 3, pos + 1))
    if pos == 1:
        return (g(x + 1, y, pos + 1) or
                g(x, y + 1, pos + 1) or
                g(x * 2, y, pos + 1) or
                g(x, y * 3, pos + 1))


for S in range(1, 59):
    if (g(10, S, 0) == False) and (f(10, S, 0) == True):
        print(S)
```

### How It Works

1. pos tracks the move number:
   * pos = 0 – Petya's first move.
   * pos = 1 – Vanya's first move.
   * pos = 2 – Petya's second move.
   * pos = 3 – Vanya's second move.
   * pos = 4 – Petya's third move.
2. f() determines if Petya can win.
3. g() determines if Vanya can win.
4. and is used when the player wants all moves to lead to a win.
5. or is used when the player needs at least one winning move.
6. The loop finds the value of S that satisfies the condition.

**Note:** The threshold 69 and multipliers x * 2, y * 3 depend on the specific problem statement.

## 7. Logical Operations and Simplification

Logical expressions can be written using only V (OR), Λ (AND), and ¬ (NOT).

### Commutativity:

* a ∧ b = b ∧ a
* a ∨ b = b ∨ a

### Associativity:

* (a ∧ b) ∧ c = a ∧ (b ∧ c)
* (a ∨ b) ∨ c = a ∨ (b ∨ c)

### Distributivity:

* a ∧ (b ∨ c) = (a ∧ b) ∨ (a ∧ c)
* a ∨ (b ∧ c) = (a ∨ b) ∧ (a ∨ c)

### Idempotence:

* a ∧ a = a
* a ∨ a = a

### Law of Excluded Middle:

* ¬a ∨ a = 1
* ¬a ∧ a = 0

### Constants:

* a ∧ 0 = 0
* a ∧ 1 = a
* a ∨ 0 = a
* a ∨ 1 = 1
* a → 1 = 1
* a → 0 = ¬a
* 0 → a = 1
* 1 → a = a
* a ≡ 0 = ¬a
* a ≡ 1 = a

### Absorption:

* (a ∨ b) ∧ a = a
* (a ∧ b) ∨ a = a

### De Morgan's Laws:

* ¬(a ∧ b) = ¬a ∨ ¬b
* ¬(a ∨ b) = ¬a ∧ ¬b

### Implication:

* a → b = ¬a ∨ b

### Equivalence:

* a ≡ b = (a → b) ∧ (b → a) = (¬a ∨ b) ∧ (a ∨ ¬b)

### Examples

```python
# Check De Morgan's law
a, b = True, False
print(not (a and b) == (not a or not b))   # True

# Check implication
print((not a) or b)   # True
```

**Note:** These laws are used to simplify logical expressions in tasks like the Unified State Exam (EGE) in Informatics.

## 8. Kadane's Algorithm (Maximum Subarray Sum)

Kadane's algorithm finds the maximum sum of a contiguous subarray in O(n) time.

### Implementation

```python
def kadane(a):
    best = a[0]
    c = a[0]
    for x in a[1:]:
        c = max(x, c + x)
        best = max(best, c)
    return best
```

### Examples

```python
print(kadane([-2, 1, -3, 4, -1, 2, 1, -5, 4]))   # 6 (subarray [4, -1, 2, 1])
print(kadane([1, 2, 3, 4]))                      # 10
```

### How It Works

1. c stores the maximum sum ending at the current position.
2. best stores the maximum sum found so far.
3. For each element, choose between starting a new subarray (x) or extending the previous one (c + x).
4. Update best if c is larger.

### Complexity

* Time complexity: O(n)
* Space complexity: O(1)

**Note:** The algorithm works for both positive and negative numbers, but the array must not be empty.

© NESTIMS
