# Data structures and algorithms

_This is a reference for data structures and algorithms made for the [Java + DSA + Interview Preparation Course](https://www.youtube.com/playlist?list=PL9gnSGHSqcnr_DxHsP7AW9ftq0AtAyYqJ)_

## Introduction to programming (Video number 5-8)

### Types of languages

[Good video here](https://www.youtube.com/watch?v=aoE-92Ac4zE)

1. Procedural programming - well structured steps and procedures to compose a program and step by step execution

2. Functional programming - Writing a program using only pure functions. Pure functions have the following properties

   1. the function return values are identical for identical arguments (no variation with local static variables, non-local variables, mutable reference arguments or input streams), and
   2. the function has no side effects (no mutation of local static variables, non-local variables, mutable reference arguments or input/output streams).

3. Object oriented programming - based on objects

### Static vs dynamic langauges

1. Static - perform type checking at compile time and type errors will be discovered at compile time. Need to declare data type explicitly

2. Dynamic - perform type checking at run time and type errors may be discovered late during program execution. Variable data type is inferred

### Stack vs heap

https://courses.engr.illinois.edu/cs225/fa2022/resources/stack-heap/

1. Stack - Stores local variables (and the data associated with the local variables). AFter a function returns, the stack memory associated to that functions and all of it's variables are deallocated. **A common mistake is to return a pointer to a stack variable from a helper function and using that returned pointer elsewhere.**

2. Heap - dynamic memory for programmers to allocate. **Unlike stack memory, heap memory is allocated explicitly by programmers and it won’t be deallocated until it is explicitly freed.**

### Prime number algorithm optimization

```
take input
initialize i = 2
while i < sqrt(number)
    if number % i == 0
        print "not prime"
        exit()
    i = i + 1

print "prime"
```

### Java Architecture

Java is both a compiled as well as an interpreted programming language. [Compiled vs interpreted](https://www.freecodecamp.org/news/compiled-versus-interpreted-languages/)

1. The `.java` file which is human readable (soure code) is first compiled by the compiler

2. This compiler compiles the source code into `.class` bytecode which is an intermediate code that is platform independent

3. The intermediate bytecode is then executed line by line by the interpreter.
