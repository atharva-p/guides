# Beginner level - [Python udemy course](https://www.udemy.com/course/100-days-of-code/)

You can import any python file that you write in the project folder as a module using `import file-name or module-name`

## Taking input

Use the `input(prompt)` function to take input. It will display prompt and wait for input, afer which the input function will be replaced by what is inputted

```python
print("hello there " + input("enter your name")) # will wait for input and print hey there input
```

**Printing multiple lines of string** To create strings that span multiple lines, triple single quotes ''' or triple double quotes """ are used to enclose the string.

### Taking multiple numbers as input

If numbers are to be inputted into a list (eg "1 3 3 5 6") use the following method

```python
# will create a list with the inputted string of numbers
numbers = list(map(int, inputString.split()))
```

## Type conversions

Convert to a string using the `str()` function. Similarly use `int()` or `float()` to convert.

You check the type of an object/data using `type` function. example, `print(type(entityName))`

## Mathematical operations

**Exponents** use `**` to denote a number as an exponent. For example, `print(2**3)` would print 2^3 that is 8

### Rounding numbers

```python
print(round(8 / 3))   # answer 3
print(round(8 / 3, 2))    # answer 2.67
```

The additional 2 will round 8 / 3 to two places afer the decimal

_TODO insert link here after finishing rounding properly_

**Floor division** Use double dashes to do a floor division. The float is automatically rounded off to an integer and returns an integer data type `print(8 // 3)` will print 2. **Floor** means to return smallest integer lower or equal to x.

**Rounding a number up**
Use the `math.ceil()` function to round a number to an integer higher or equal to x. To **ceil** is to return an integer that is equal or higher than x.

## F strings

Automatically converts data into string and concatenates with the rest of the string. Needs an f before the string

## Lower() and count()

`lower()` function will make a string lowercase. The `count()` function will return the count of the string or substring passed to it from a list.

```python
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

`choice(iterable)` will return a randomly chosen element from any iterable that is passed to it

`shuffle(iterable)` will shuffle the original iterable passed to it

## [Lists](https://www.w3schools.com/python/python_ref_list.asp)

Negative indices can also be used to access list data. A negative index will start counting from the end of the list.

The `index(item)` method for a list will return the first position of `item` from the given index

`append(item)` will add to the end of the list. Function takes only one item to be added as the argument. If an iterable is passed it will be instead added entirely to the list (unlike extend).

`extend(iterable)` will add all the elements of the iterable to the end of the current list.

**Difference between append and extend** - append adds only the element passed to it to the end of the list whereas extend will cycle through the iterable and add all of it's elements to the end of the list

```python
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

1. String to a list of strings - Use the `split()` or `rsplit()` functions. These functions will split a string at the specified separator and returns a **list of substrings**.

The default separator for `split()` is any whitespace.

2. String to a list of characters

   You can use the `list()` function to return a list from any iterable. It is actually a constructor of the list class

   ```python
   name = "atharva"
   testList = list(name)
   print(testlist)
   ```

   Will return `['a', 't', 'h', 'a', 'r', 'v', 'a']` to testList. Even though `split()` method also returns a substring, it can only be used in this case when the string is made up of multiple words, since the `split()` function separator argument cannot be empty

3. List of strings to a list of character strings

```python
testList = ["atharva", "ashish", "patil"]
# convert to a list of character strings
charList = list(map(list, testList))
print(charList)
```

This will output `[['a', 't', 'h', 'a', 'r', 'v', 'a'], ['a', 's', 'h', 'i', 's', 'h'], ['p', 'a', 't', 'i', 'l']]`

### Strings are immutable

If it is not possible to alter the value of an object over time, it is known as immutable. Strings are immutable so the following code will work in C but not in python

```python
# will not work!!
name = "atharva"
# swaping t for r
temp = name[1]
name[1] = name[4]
name[4] = temp
```

A work around for this is to [convert the string into a list of characters](#converting-strings-to-lists), manipulate the list and then concatenate the list as needed into a string using the [`join()`](#string-concatenation) method

```python
name = "atharva"
nameAsAList = list(atharva)

# swap the characters inside the list

newString = "".join(nameAsAList)
```

### The enumerate function

the `enumerate(iterable, optional-starting-number)` function adds counter to an iterable and returns it as an enumerate object which can then be converted into a list or tuple.

#### Enumerate function in for loops

```python
testList = ["apple", "microsoft", "google", "lenovo", "bing", "tesla"]
for index, item in enumerate(testList):
    print(f"{index} {item}")

# this will output
0 apple
1 microsoft
2 google
3 lenovo
4 bing
5 tesla
```

#### Converting enumerate object into a list

An enumerated object converted into a list can be used as a normal 2D list. It creates a matrix[x][y] with x representing the counter column assigned by enumerate and y the column with the actual iterable values.

## [Terminating a program](https://www.geeksforgeeks.org/python-exit-commands-quit-exit-sys-exit-and-os-_exit/)

Use the `sys.exit()` function from the `sys` module to exit a program.

It takes an optional argument, either an integer or a string. 0 integer indicates successful program termination.

### Membership operators

Used to test whether an item is present in an object.

`in` - will return true if the item is found in object
`not in` - will return true if the item is not found in object

## Loops

### For loop with a range function

```python
for i in range(0, 100):
   print(i)
```

Loop will work between the range defined by the range function. `range(a, b)` will be between a and b, including a but **not including b** [a, b)

By default the next iteration using a range function will increase by 1. If you want any other number, you can pass an extra parameter to the function `for i in range(0, 11, 2)` will print 0 2 4 6 8 10

## [String concatenation](https://www.digitalocean.com/community/tutorials/python-string-concatenation)

1. Using + operator
2. using `join()` method

   `join()` method takes all items in an iterable and joins them into a string

3. using %
4. using `format()`
5. Uisng [f strings](#f-strings)

_TODO add about from file import something_

## Functions

### Parameters vs Arguments

**Parameters** - `def greet(name):` in this the name variable is the parameter. The variables that are defined when the function is declared are known as a parameter.

**Arguments** - `greet("atharva")` in this the string "atharva" passed to the function is known as the argument. The values that are declared within a function when the function is called are known as an argument.

### Keyword Arguments

You can add arguments with their respective parameters during a function call. For example, if we have a function `def testfun(a, b, c)` we can pass arguments to specific parameters `testfun(b = 10, a = 1, c = 30)`

### Returning Unicode value of a unicode character and vice versa

Use the `ord()` function to convert character to unicode

Use the `chr()` function to convert unicode to character

### Lambda functions

Lambda functions are used to create small, one-time-use functions that don't need a name. They are often used as arguments to higher-order functions that take other functions as inputs. They can also be used to write more concise code.

The main difference between lambda and def is that lambda is an expression, not a statement. This means that it can appear in places where def cannot, such as inside a list comprehension or an argument list.

Lambda functions are also useful when you want to create a function that takes an argument and returns a function. For example, if you want to create a function that returns a function that multiplies its input by a certain factor, you could use a lambda function like this:

```python
def multiply_by(factor):
    return lambda x: x * factor

double = multiply_by(2)
triple = multiply_by(3)

print(double(5)) # Output: 10
print(triple(5)) # Output: 15
```

Here, we define a function `multiply_by` that takes an argument `factor` and returns a lambda function that multiplies its input by `factor`. We then use this function to create two new functions `double` and `triple` that multiply their input by 2 and 3 respectively.
