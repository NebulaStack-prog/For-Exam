# For-Exam

<img src="https://github.com/NebulaStack-prog/Fir-Exam/blob/main/ForExam.png" width="200" height="230">

## Number Systems

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

* **Base 2** — Binary
* **Base 3** — Ternary
* **Base 4** — Quaternary
* **Base 8** — Octal
* **Base 10** — Decimal
* **Base 16** — Hexadecimal

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

