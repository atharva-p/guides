
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

When you instantiate an object, Python creates a new instance and passes it to the first parameter of `.__init__()`, which is the `self` parameter (this first parameter can be named anything, but convention is to name it self). This essentially removes the `self` parameter, so you only need to worry about the parameters that follow `self`. 

## `__str__()` instance method

You can change the default behavior of `print(class_object)` by defining an `__str__(self)` special instance method. This method should return a string of your choice

Methods that start and end with double underscores are called **dunder methods** 

## Inheritance

Pass the parent class to your child class as an argument to perform inheritance

Use `isinstance(object_name, class_name)` and `type()` built in functions to know if an object is an instance of some class (to find if it has any inheritance) and find the type of the object (class it belongs to) respectively

## `super()` method 

Sometimes it makes sense to completely overwrite the parent's method, however sometimes, you also want use the parent's method but have some child exclusive customizations. To do this, you can use `super()` method, to access the parent class's method. 

Do achieve this, you need to call the parent class's method from child using `super()` and pass arguments from the child class, like it is done in the following example

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