# Beginner level - [Python udemy course](https://www.udemy.com/course/100-days-of-code/)

You can import any python file that you write in the project folder as a module using `import file-name or module-name`

## Taking input

Use the `input(prompt)` function to take input. It will display prompt and wait for input, afer which the input function will be replaced by what is inputted

```
print("hello there " + input("enter your name")) // will wait for input and print hey there input
```

**Printing multiple lines of string** To create strings that span multiple lines, triple single quotes ''' or triple double quotes """ are used to enclose the string.

### Taking multiple numbers as input

If numbers are to be inputted into a list (eg "1 3 3 5 6") use the following method

```
# will create a list with the inputted string of numbers
numbers = list(map(int, inputString.split()))
```

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

## [Randomization](https://www.w3schools.com/python/module_random.asp)

Import the random module first

`randint(a, b)` generates a random number between a and b (both inclusive)

`random()` generates a floating point number between [0, 1), 1 not being inclusive. Function takes no arguments

`uniform(a, b)` generates a floating point number between a and b (both inclusive)

## [Lists](https://www.w3schools.com/python/python_ref_list.asp)

Negative indices can also be used to access list data. A negative index will start counting from the end of the list.

`append(item)` will add to the end of the list. Function takes only one item to be added as the argument. If an iterable is passed it will be instead added entirely to the list (unlike extend).

`extend(iterable)` will add all the elements of the iterable to the end of the current list.

**Difference between append and extend** - append adds only the element passed to it to the end of the list whereas extend will cycle through the iterable and add all of it's elements to the end of the list

```
testList = ["google", "amazon"]
print(testList)
# output ['google', 'amazon']

testList.append("apple")
print(testList)
# output ['google', 'amazon', 'apple']

anotherList = ["microsoft", "tesla"]
testList.append(anotherList)
print(testList)
# output ['google', 'amazon', 'apple', ['microsoft', 'tesla']]

testList.extend(anotherList)
print(testList)
# output ['google', 'amazon', 'apple', ['microsoft', 'tesla'], 'microsoft', 'tesla']

testList.extend("SpaceX")
print(testList)
# output ['google', 'amazon', 'apple', ['microsoft', 'tesla'], 'microsoft', 'tesla', 'S', 'p', 'a', 'c', 'e', 'X']
```

### [Converting strings to lists](https://www.askpython.com/python/string/convert-string-to-list-in-python)

1. String to a list of strings - Use the `split()` or `rsplit()` functions

2. String to a list of characters

   You can use the `list()` function to return a list from any iterable. It is actually a constructor of the list class

   ```
   name = "atharva"
   testList = list(name)
   print(testlist)
   ```

   Will return `['a', 't', 'h', 'a', 'r', 'v', 'a']` to testList.

3. List of strings to a list of character strings

```
testList = ["atharva", "ashish", "patil"]
# convert to a list of character strings
charList = list(map(list, testList))
print(charList)
```

This will output `[['a', 't', 'h', 'a', 'r', 'v', 'a'], ['a', 's', 'h', 'i', 's', 'h'], ['p', 'a', 't', 'i', 'l']]`
