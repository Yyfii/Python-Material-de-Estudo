## Python Code Quality - Best Practices

- `Low-quality code`: It has the minimal required characteristics to be functional.
- `High-quality code`: It has all the necessary characteristics that make it work reliably, efficiently, and effectively, while also being straightforward to maintain.

_Low-Quality Code at the very least needs to meet the following basic criteria:_

- **It does what it’s supposed to do**. If the code doesn’t meet its requirements, then it isn’t quality code. You build software to perform a task. If it fails to do so, then it can’t be considered quality code.

- **It doesn’t contain critical errors**. If the code has issues and errors or causes you problems, then you probably wouldn’t call it quality code. If it’s too low-quality and becomes unusable, then if falls below even basic quality standards and you may stop using it altogether.

_Key characteristics that define high-quality code:_

- **Functionality**: Works as expected and fulfills its intended purpose.
- **Readability**: Is easy for humans to understand.
- **Documentation**: Clearly explains its purpose and usage.
- **Standards Compliance**: Adheres to conventions and guidelines, such as PEP 8.
- **Reusability**: Can be used in different contexts without modification.
- **Maintainability**: Allows for modifications and extensions without introducing bugs.
- **Robustness**: Handles errors and unexpected inputs effectively.
- **Testability**: Can be easily verified for correctness.
- **Efficiency**: Optimizes time and resource usage.
- **Scalability**: Handles increased data loads or complexity without degradation.
- **Security**: Protects against vulnerabilities and malicious inputs.

#### Functionality

It needs to do what it´s supposed to do.

🔴 **Low-quality code**:

```py
def add_numbers(a,b):
return a + b

print(add_numbers(2, 3))

## If you mix some argument types, then the function will crash

print(add_numbers(2, "3"))

## Python will come up with an error because you passing a number and a string. Now, it´s time for a higher-quality implementation.
```

🟢 **Higher-quality code**

```py
## higher-quality code

def add_numbers(a: int | float, b: int | float) -> float:
    a, b = float(a), float(b)
    return a + b

print(add_numbers(2, 3))
print(add_numbers(2, "a"))

## Now it converts the input arguments into float numbers. This way the function will be more resilient. Of course, this implementation isn´t perfect, but it´s better than the first one.
```

#### Readability

🔴 **Low-quality code**:

```py
## Low-quality code

def ca(w, h):
    return w * h
print(ca(12, 20))

## this function works, it takes two numbers and multiplies them, but you can tell what this function is for?
```

🟢 **Higher-quality code**

```py
## higher-quality code

def calculate_rectangle_area(width: float, height: float) -> float:
    return width * height

print(calculate_rectangle_area(12, 20))

## Now, when you read the function´s name, you immediately know what the function is about because the argument names provide additional context.
```

#### Documentation

🔴 **Low-quality code**:

```py
## Low-quality code

def multiply(a, b):
    return a * b

print(multiply(2, 3))

## This function provides no explanation of parameters or return values. If you dig into the code, then you can tell what the function does, but it would be nice to have some more context. That’s where documentation comes in. The improved version below uses docstrings and type hints as ways to document the code.
```

🟢 **Higher-quality code**

```py
## higher-quality code

def multiply(a: float, b: float) -> float:
    """
    Multipy two numbers.

    Args:
        a (float): First number.
        b (float): Second number.
    Returns:
        float: Product of a and b.
    """
    return a * b
print(multiply(2, 3))
```

#### Compliance

Following PEP 8 guidelines.

🔴 **Low-quality code**:

```py
## Low-quality code

def multiply(a, b):
    return a * b

print(multiply(2, 3))

## This function provides no explanation of parameters or return values. If you dig into the code, then you can tell what the function does, but it would be nice to have some more context. That’s where documentation comes in. The improved version below uses docstrings and type hints as ways to document the code.
```

🟢 **Higher-quality code**

```py
## higher-quality code

def multiply(a: float, b: float) -> float:
    """
    Multipy two numbers.

    Args:
        a (float): First number.
        b (float): Second number.
    Returns:
        float: Product of a and b.
    """
    return a * b
print(multiply(2, 3))
```

#### Reusability

Reusable code reduces repetition, which improves maintability and has strong impact on productivity.

🔴 **Low-quality code**:

```py
## Low-quality code

def greet_alice():
    return "Hello, Alice!"
print(greet_alice())

## This function only works when we need to greet alice, which is preety restrictive.
```

🟢 **Higher-quality code**

```py
## higher-quality code

def greet(name: str) -> str:
    return f"Hello {name}!"

print(greet("Alice"))
print(greet("Ana"))
print(greet("Maria"))

## Although quite basic, this function is more generic and useful than the previous version. It takes a person’s name as an argument and builds a greeting message using an f-string.
```

#### Maintainability

Maintainability is all about writing code that you or other people can quickly understand, update, extend, and fix. Avoiding repetitive code and code with multiple responsibilities are key principles to achieving this quality characteristic.

🔴 **Low-quality code**:

```py
## Low-quality code

def process(numbers):
    cleaned = [number for number in numbers if number >= 0]
    return sum(cleaned)

print(process([1, 2, 3, -1, -2, -3]))
## First, it cleans the input data by filtering out negative numbers. Then, it calculates the total and returns it to the caller.
```

🟢 **Higher-quality code**

```py
## higher-quality code

def clean_data(numbers: list[int]) -> list[int]:
    return [number for number in numbers if number >= 0]

def calculate_total (numbers: list[int]) -> int:
    return sum(numbers)

cleanead = clean_data([1, 2, 3, -1, -2, -3])
print(calculate_total(cleanead))

## This time, you have a function that cleans the data and a second function that calculates the total. Each function has a single responsibility, so they’re more maintainable and easier to understand.
```

#### Robustness

Robust code is capable of handling errors gracefully, preventing crashes and unexpected behaviors and results.

🔴 **Low-quality code**:

```py
## Low-quality code

def divide_numbers(a, b):
    return a / b
print(divide_numbers(4, 2))
print(divide_numbers(4, 0))

## This function divides two numbers, as expected. However, when the divisor is 0, the code breaks with a ZeroDivisionError exception. To fix the issue, you need to properly handle the exception.
```

🟢 **Higher-quality code**

```py
## higher-quality code

def divide_numbers(a: float, b: float) -> float | None:
    try:
        return a / b
    except ZeroDivisionError:
        print("Error: can´t divide by zero")

print(divide_numbers(4, 2))
print(divide_numbers(4, 0))

## Now, your function handles the exception, preventing a code crash. Instead, you print an informative error message to the user.
```

#### Testability

You can say that a piece of code is testable when it allows you to quickly write and run automated tests that check the code’s correctness.

🔴 **Low-quality code**:

```py
## Low-quality code

## This function is hard to test because it uses the built-in print() function of returning a concrete result. The code operates through a side effect, making it more challenging to test. Here´s the test that takes advantage of pytest:

import pytest

def greet(name):
    print(f"Hello, {name}!")

def test_greet(capsys):
    greet("Alice")
    captured = capsys.readouterr()
    assert captured.out.strip() == "Hello, Alice!"

## This test case works. However, it´s hard to write because it demands a relatively advanced knowledge of the pytest library.You can replace the call to print() with a return statement to improve the testability of greet() and simplify the test.
```

🟢 **Higher-quality code**

```py
## higher-quality code

def greet(name: str) -> str:
    return f"Hello, {name}!"

def test_greet():
    assert greet("Alice") == "Hello, Alice!"

## Now, the function returns the greeting message. This makes the test case quicker to write and requires less knowledge of pytest. It´s also more efficient and quick to run, so this version of greet() is more testable.
```

#### Efficiency

Is the execution speed and memory consumption. Depending on your project, you may find other features that could be considered for evaluating efficiency, including disk usage, network latency, energy consumption, and many others.

Following PEP 8 guidelines.

🔴 **Low-quality code**:

```py
## Low-quality code

# The following code computes the fibonacci sequence of a series of numbers using a recursive algorithm:
from time import perf_counter

def fibonacci_of(n):
    if n in {0, 1}:
        return n
    return fibonacci_of(n - 1) + fibonacci_of(n -2)

start = perf_counter()
[fibonacci_of(n) for n in range(35)] # Generate 35 Fibonacci numbers
end = perf_counter()

print(f"Execution time: {end - start:.2f} seconds")

## if you run this scrit from your command line, "Execution time: 1.96 seconds", the execution time is almost two seconds.
```

🟢 **Higher-quality code**

```py
## higher-quality code

from time import perf_counter

cache = {0 : 0, 1: 1} # dictionary to store calculated results.
def fibonacci_of(n):
    if n in cache: # if the result is already in the cache, return it directly.
        return cache[n]
    # if not, the it calculates recursively and stores in cache
    cache[n] = fibonacci_of(n - 1) + fibonacci_of(n -2)
    return cache[n]

start = perf_counter()
[fibonacci_of(n) for n in range(35)] # calculates fibonacci from 0 to 35
end = perf_counter()

print(f"Execution time: {end - start:.2f} seconds")

## This implementation optimizes the Fibonacci computation using caching. Now, run this improved code from the command line. You´ve improved the code´s efficiency by boosting performance.
## So, what´s the diference?
# The diference, is because this one, uses `Memoization(cache), it record the results already calculated in memory cache`, while the low-quality code (uses pure recusiveness), recalculates the same values repeatedly, making it relatively slower.
```

#### Scalability

Following PEP 8 guidelines.

🔴 **Low-quality code**:

```py
## Low-quality code

def multiply(a, b):
    return a * b

print(multiply(2, 3))

## This function provides no explanation of parameters or return values. If you dig into the code, then you can tell what the function does, but it would be nice to have some more context. That’s where documentation comes in. The improved version below uses docstrings and type hints as ways to document the code.
```

🟢 **Higher-quality code**

```py
## higher-quality code

def multiply(a: float, b: float) -> float:
    """
    Multipy two numbers.

    Args:
        a (float): First number.
        b (float): Second number.
    Returns:
        float: Product of a and b.
    """
    return a * b
print(multiply(2, 3))
```

#### Compliance

Following PEP 8 guidelines.

🔴 **Low-quality code**:

```py
## Low-quality code

def multiply(a, b):
    return a * b

print(multiply(2, 3))

## This function provides no explanation of parameters or return values. If you dig into the code, then you can tell what the function does, but it would be nice to have some more context. That’s where documentation comes in. The improved version below uses docstrings and type hints as ways to document the code.
```

🟢 **Higher-quality code**

```py
## higher-quality code

def multiply(a: float, b: float) -> float:
    """
    Multipy two numbers.

    Args:
        a (float): First number.
        b (float): Second number.
    Returns:
        float: Product of a and b.
    """
    return a * b
print(multiply(2, 3))
```

#### Compliance

Following PEP 8 guidelines.

🔴 **Low-quality code**:

```py
## Low-quality code

def multiply(a, b):
    return a * b

print(multiply(2, 3))

## This function provides no explanation of parameters or return values. If you dig into the code, then you can tell what the function does, but it would be nice to have some more context. That’s where documentation comes in. The improved version below uses docstrings and type hints as ways to document the code.
```

🟢 **Higher-quality code**

```py
## higher-quality code

def multiply(a: float, b: float) -> float:
    """
    Multipy two numbers.

    Args:
        a (float): First number.
        b (float): Second number.
    Returns:
        float: Product of a and b.
    """
    return a * b
print(multiply(2, 3))
```

### Referencias

- 🗂️[Real Python](https://realpython.com/python-code-quality/)
