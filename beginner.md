# Beginner level - [Python udemy course](https://www.udemy.com/course/100-days-of-code/)

## Taking input

Use the `input(prompt)` function to take input. It will display prompt and wait for input, afer which the input function will be replaced by what is inputted

```
print("hello there " + input("enter your name")) // will wait for input and print hey there input
```

Use the `len(variableName or data)` to get the length of a string, int, etc

**Printing multiple lines of string** To create strings that span multiple lines, triple single quotes ''' or triple double quotes """ are used to enclose the string.

## Type conversions

Convert to a string using the `str()` function. Similarly use `int()` or `float()` to convert.

You check the type of an object/data using `type` function. example, `print(type(entityName))`

## Mathematical operations

**Exponents** use `**` to denote a number as an exponent. For example, `print(2**3)` would print 2^3 that is 8

### Rounding numbers

```
print(round(8 / 3))   // answer 3
print(round(8 / 3, 2))    // answer 2.67
```

The additional 2 will round 8 / 3 to two places afer the decimal

_TODO insert link here after finishing rounding properly_

**Floor division** Use double lashes to do a floor division. The float is automatically rounded off to an integer and returns an integer data type `print(8 // 3)` will print 2

## F strings

Automatically converts data into string and concatenates with the rest of the string. Needs an f before the string

```
score = 0
isWinnning = True
print(f"your score is {score} and you winning boolean is {isWinnign}")
```

## Lower() and count()

`lower()` function will make a string lowercase. The `count()` function will return the count of the string or substring passed to it from a list.

```
name = "Atharva"
lower = name.lower() // will become "atharva"
count = name.count("a") // will return 3
```

`lower()` is part of [python string methods](https://www.w3schools.com/python/python_ref_string.asp) and `count()` is a part of python list methods
