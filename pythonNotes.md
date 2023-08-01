# Essential important python notes

There is no block scope in python. Only functions have local scopes. if-else, loops don't create local scopes. 

## Script vs module vs package vs library

Script - A **script** is a Python file that’s intended to be run directly. When you run it, it should do _something_. This means that scripts will often contain code written outside the scope of any classes or functions

Module - A **module** is a Python file that’s intended to be imported into scripts or other modules. It often defines members like classes, functions, and variables intended to be used in other files that import it.

Library - A **library** is a set of modules which makes sense to be together and that can be used in a program or another library

Package - A **package** is a unit of distribution that can contain a library or an executable or both. It's a way to share your code with the community.

## Taking input

```python
print("hello there " + input("enter your name")) # will wait for input and print hey there input
```

### Taking multiple numbers as input

If numbers are to be inputted into a list (eg "1 3 3 5 6") use the following method

```python
# will create a list with the inputted string of numbers
numbers = list(map(int, inputString.split()))
```

## Mathematical operations

Use `**` to denote a number as an exponent. For example, `print(2**3)` would print 2^3 that is 8

### Rounding numbers

```python
print(round(8 / 3))   # answer 3
print(round(8 / 3, 2))    # answer 2.67
```

The additional 2 will round 8 / 3 to two places after the decimal

[Real python rounding numbers](https://realpython.com/python-rounding/)

**Floor division** Use double dashes to do a floor division. The float is automatically rounded off to an integer and returns an integer data type `print(8 // 3)` will print 2. **Floor** means to return smallest integer lower or equal to x.

**Rounding a number up**
Use the `math.ceil()` function to round a number to an integer higher or equal to x. To **ceil** is to return an integer that is equal or higher than x.

## Lower() and count()

`lower()` function will make a string lowercase. The `count()` function will return the count of the string or substring passed to it from a list.

```python
name = "Atharva"
lower = name.lower() # will become "atharva"
count = name.count("a") # will return 3
```

`lower()` is part of [python string methods](https://www.w3schools.com/python/python_ref_string.asp) and `count()` is a part of python list methods

## [Randomization](https://www.w3schools.com/python/module_random.asp)

`randint(a, b)` - generates a random number between a and b (both inclusive)

`random()` - generates a floating point number between [0, 1), 1 not being inclusive. Function takes no arguments

`uniform(a, b)` - generates a floating point number between a and b (both inclusive)

`choice(iterable)` - will return a randomly chosen element from any iterable that is passed to it

`shuffle(iterable)` - will shuffle the original iterable passed to it. This method changes the original list, it does not return a new list.

## [Lists](https://www.w3schools.com/python/python_ref_list.asp)

Negative indices can also be used to access list data. A negative index will start counting from the end of the list.

The `index(item)` method for a list will return the first position of `item` from the given index

`append(item)` will add to the end of the list. Function takes only one item to be added as the argument. If an iterable is passed it will be instead added entirely to the list (unlike extend).

**Warning:** - The `append()` returns `None` after running so do not assign `append()` to a variable

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

### Enumerate function

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

An enumerated object converted into a list can be used as a normal 2D list. It creates a matrix\[x]\[y] with x representing the counter column assigned by enumerate and y the column with the actual iterable values.

## [Terminating a program](https://www.geeksforgeeks.org/python-exit-commands-quit-exit-sys-exit-and-os-_exit/)

Use the `sys.exit()` function from the `sys` module to exit a program.

It takes an optional argument, either an integer or a string. 0 integer indicates successful program termination.

### Membership operators

Used to test whether an item is present in an object.

`in` - will return true if the item is found in object.
`not in` - will return true if the item is not found in object

## Loops

### For loop with a range function

Loop will work between the range defined by the range function. `range(a, b)` will be between a and b, including a but **not including b** [a, b)

By default the next iteration using a range function will increase by 1. If you want any other number, you can pass an extra parameter to the function `for i in range(0, 11, 2)` will print 0 2 4 6 8 10

## [String concatenation](https://www.digitalocean.com/community/tutorials/python-string-concatenation)

1. Using + operator
2. using `join()` method

   `join()` method takes all items in an iterable and joins them into a string

3. using %
4. using `format()`
5. Using [f strings](#f-strings)

_TODO add about from file import something_

## Functions

### Scope and the `global` keyword 

In order to modify variables of the global scope through a local function, a variable needs to be explicitly defined as global inside the local function's scope. Modifying into the global scope often is considered a bad practice. 

**Remember**, the `global` keyword is NOT required if global variables are ONLY BEING ACCESSED inside a local scope

```python
varible_global = 1 
def local_function(): 
	global variable_global
	variable_global += 1      # will change the value of global variable_global to 2 when this function is called 
```

### Parameters vs Arguments

**Parameters** - `def greet(name):` in this the name variable is the parameter. The variables that are defined when the function is declared are known as a parameter.

**Arguments** - `greet("atharva")` in this the string "atharva" passed to the function is known as the argument. The values that are declared within a function when the function is called are known as an argument.

### Keyword Arguments

You can add arguments with their respective parameters during a function call. For example, if we have a function `def testfun(a, b, c)` we can pass arguments to specific parameters `testfun(b = 10, a = 1, c = 30)`

### Returning Unicode value of a unicode character and vice versa

Use the `ord()` function to convert character to unicode

Use the `chr()` function to convert unicode to character

### Lambda functions

TODO add syntax

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

## Dictionaries

```python
test_dict = {
   "key": "value",
   "anotherKey": "anotherValue",
}
```

Used to store key value pairs. Passing a key to the dictionary will return the value associated with that key

Dictionary keys can also have function names as their values

### Operations on a dictionary

```python
# Adding or modifying a key's value in a dictionary
dictonary_name[key] = "another value"
# looping through a dictionary and printing values
for key in dictionary_name:
   print(dictionary_name[key])
```

### Nesting lists and dictionaries inside a dictionary

Both lists and dictionaries can be listed. Following code nests dictionaries with the country name inside the root dictionary `travel_log` to describe attributes of countries (like cities_visited, food_eaten, etc). Lists are also nested inside the country dictionaries to denote multiple items associated with that attribute.

```python
travel_log = {
   "France": { # attribute dictionary with nested lists as the values of the keys
      "cities_visited": ["Paris", "Dijon"],
      "food_eaten": ["croissant", "Ratatoullie"]
   },
   "Germany": {
      "cities_visited": ["Berlin"]
   },
}
```

You could also nest multiple dictonaries inside a list and access them according to the list index numbers

## Docstrings

Give your functions a description that IDEs and other programming tools can also read and show during function call

```python
def test_function():
   """ This is the function description """
   return None
```

# Virtual environments 

## Using `python -m` while running commands in venv

Always prepend your command with `python -m`, not doing so will execute the command using the global python interpreter, which will make the virtual environment pointless 

## What do you mean by "executing a module as a script"?

Modules that can be executed as scripts have an outer scope that acts as an entry point for running the module directly from the command line. This outer scope allows the module to be invoked and executed as a standalone script, providing functionality or performing actions specific to that module.

When a module is executed as a script using `python -m`, the code within the module's outer scope is executed. This allows the module to perform any necessary setup, define functions or classes, and potentially interact with the user or perform specific actions. The outer scope serves as the entry point for running the module as a script.

In addition to the outer scope, the module may also contain other functions, classes, or variables that can be imported and used by other Python scripts. These internal components of the module can be accessed when importing the module using `import` statements, but they are not executed when the module is invoked as a script.

By having the ability to execute a module as a script, Python modules can be versatile and serve multiple purposes. They can be used as libraries of reusable code, but also as standalone scripts with their own functionality and behavior. This flexibility allows modules to be utilized in various contexts, depending on how they are invoked.


# Object oriented programming 

## Declaration and basic syntax

```python 
class Dog:
	# species is a class attribute, all dogs will have belong to this species
	species = "Canis familiaris"      

	def __init__(self, name, age): 
		self.name = name 
		self.age = age
		
	# instance method
	def __str__(self): 
		print(f"{self.name}, {self.age}, and {self.species})

# create instances 
dog1 = Dog("Tyler", 24)
```

Instance attributes - Attributes created in `.__init__()` are called **instance attributes**. An instance attribute’s value is specific to a particular instance of the class. All `Dog` objects have a name and an age, but the values for the `name` and `age` attributes will vary depending on the `Dog` instance.

Class attributes - On the other hand, [class attributes](https://realpython.com/python-classes/#class-attributes) are attributes that have the same value for all class instances. You can define a class attribute by assigning a value to a variable name outside of `.__init__()`.

These objects created using custom data structures (classes) are mutable by default

### `self` in class methods

When you instantiate an object, Python creates a new instance and passes it to the first parameter of `.__init__()`, which is the `self` parameter (this first parameter can be named anything, but convention is to name it self). This essentially removes the `self` parameter, so you only need to worry about the parameters that follow `self`. 

## `__str__()` instance method

You can change the default behavior of `print(class_object)` by defining an `__str__(self)` special instance method. This method should return a string of your choice

Methods that start and end with double underscores are called **dunder methods** 

## Inheritance

Pass the parent class to your child class as an argument to perform inheritance

Use `isinstance(object_name, class_name)` and `type()` built in functions to know if an object is an instance of some class (to find if it has any inheritance) and find the type of the object (class it belongs to) respectively

## `super()` method 

Sometimes it makes sense to completely overwrite the parent's method, however sometimes, you also want use the parent's method but have some child exclusive customizations. To do this, you can use `super()` method, to access the parent class's method. 

Do achieve this, you need to call the parent class's method from child using `super()` and pass arguments from the child class, like it is done in the following example. 

In the example, you could use the parent's `speak()` function without using the `super()` method since child class inherits parent. However, we want to customize the child class's `speak()` by giving the `sound="BULL"` parameter a default argument. To do add any customization to parent's functions, we use the `super()` method

```python
class Dog:  
# species is a class attribute, all dogs will have belong to this species  
species = "Canis familiaris"  
  
def __init__(self, name, age):  
	self.name = name  
	self.age = age  
  
def __str__(self):  
	return f"{self.name}, {self.age}, and {self.species}"  
  
def speak(self, sound):  
	return f"{self.name} says, and sometimes also barks {sound}, from parent"  
  
  
# child class  
class Bulldog(Dog):  
  
def speak(self, sound="BULL"):  
	return super().speak(sound)  
  
  
# create instances  
tyler = Dog("Tyler", 4)  
print(tyler.speak("woof"))  
  
goldie = Bulldog("Goldie", 5)  
print(goldie.speak())  
print(goldie.speak("grrrr"))
```

Output: 
```
Tyler says, and sometimes also barks woof, from parent
Goldie says, and sometimes also barks BULL, from parent
Goldie says, and sometimes also barks grrrr, from parent
```

## Class attributes vs instance attributes

Class attributes - Attributes that may be shared across objects are called class attributes. These are declared outside `__init__()` and do not use the `self` tag

Instance attributes - Attributes that will be unique to each object of the class are instance attributes. These are declared inside the `__init__()` function and use the `self` tag

# List comprehensions 

Used for creating a new list using items from an already existing list. A sequence of operators (+) and operands (a  and b) is called an expression

```python 
# syntax 
new_list = [expression for item in iterable if condition]
```

Below example will divide the numbers by 2 (expression) in the old_list and copy them to the new_list as integers if the number is smaller than 100 (condition)

```python 
old_list = [10, 20, 30, 440, 343, 134]

new_list = [int((number / 2)) for number in old_list if number < 100]
print(new_list)

# output 
# [5, 10, 15]
```

# Exception handling 

Useful links: 
https://realpython.com/python-exceptions/
https://www.datacamp.com/tutorial/exception-handling-python

## raising exceptions

```python 
x = 100
if x < 0: 
	raise Exception("exception message")
```

## catching exceptions 

```python
try:
    linux_interaction()
except AssertionError as error:
    print(error)
else:
    try:
        with open('file.log') as file:
            read_data = file.read()
    except FileNotFoundError as fnf_error:
        print(fnf_error)
finally: 
	print("clean up code here")
```

`try` contains the code you want to test for exceptions, `except` is the exception handler in which code to run in case of an exception is put. `else` will only run in case there were no exceptions while executing the `try` block. 

`finally` will execute code regardless of exceptions or not. It is used for cleanup code that needs to run every time. [Why should i use finally and not put cleanup code outside the try-except-else block in the outer scope?](https://chat.openai.com/share/380149b9-4f6b-4c6d-8fac-00798a211a57)


# Animate sprites (neat trick)

```python
index = (index + 1) % len(sprite_list)
```

Above code creates a looping effect, index resets to zero as it approaches the end of `sprite_list` 

- Frame 1: `index = (0 + 1) % 5 = 1`. The sprite image at index 1 is displayed.
- Frame 2: `index = (1 + 1) % 5 = 2`. The sprite image at index 2 is displayed.
- Frame 3: `index = (2 + 1) % 5 = 3`. The sprite image at index 3 is displayed.
- Frame 4: `index = (3 + 1) % 5 = 4`. The sprite image at index 4 is displayed.
- Frame 5: `index = (4 + 1) % 5 = 0`. The sprite image at index 0 is displayed (looping back to the first image)

# `with` keyword

Another way to use the `try-except-finally` conveniently 

Used to manage resources that require cleanup or release of resources. Eliminates boilerplate code and makes code readable

Every `with` keyword uses the `__enter()__`  and `__exit__()` functions from the context manager. A context manger is any object that has an associated `__enter()` and `__exit()__` block

```python 
with expression as target:
	# code block for with
```

1. The context expression (the expression given in the [`with_item`](https://docs.python.org/3/reference/compound_stmts.html#grammar-token-python-grammar-with_item)) is evaluated to obtain a context manager.
    
2. The context manager’s `__enter__()` is loaded for later use.
    
3. The context manager’s `__exit__()` is loaded for later use.
    
4. The context manager’s `__enter__()` method is invoked.
    
5. If a target was included in the [`with`](https://docs.python.org/3/reference/compound_stmts.html#with) statement, the return value from `__enter__()` is assigned to it.

# Equality vs identity (`is`) 

Equality is denoted by the `==` symbol whereas identity is denoted by the `===` symbol. 

Identity is python is checked using the `is` keyword

- `==` checks for equality of values.
- `is` checks if two variables refer to the same object in memory.
