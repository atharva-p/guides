
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
	def print_info(self): 
		print(f"{self.name}, {self.age}, and {self.species})

# create instances 
dog1 = Dog("Tyler", 24)
```

Instance attributes - Attributes created in `.__init__()` are called **instance attributes**. An instance attribute’s value is specific to a particular instance of the class. All `Dog` objects have a name and an age, but the values for the `name` and `age` attributes will vary depending on the `Dog` instance.

Class attributes - On the other hand, [class attributes](https://realpython.com/python-classes/#class-attributes) are attributes that have the same value for all class instances. You can define a class attribute by assigning a value to a variable name outside of `.__init__()`.

These objects created using custom data structures (classes) are mutable by default
