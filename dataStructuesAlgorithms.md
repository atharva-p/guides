# Data structures and algorithms

_This is a reference for data structures and algorithms made for the [Java + DSA + Interview Preparation Course](https://www.youtube.com/playlist?list=PL9gnSGHSqcnr_DxHsP7AW9ftq0AtAyYqJ)_

## (Video 5-8) Introduction to programming

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

**_c++ implementation_**

https://courses.engr.illinois.edu/cs225/fa2022/resources/stack-heap/

1. Stack - Stores local variables (and the data associated with the local variables). AFter a function returns, the stack memory associated to that functions and all of it's variables are deallocated. **A common mistake is to return a pointer to a stack variable from a helper function and using that returned pointer elsewhere.**

2. Heap - dynamic memory for programmers to allocate. **Unlike stack memory, heap memory is allocated explicitly by programmers and it won’t be deallocated until it is explicitly freed.**

**_Java implementation_**

yet to be added

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

In java, everything extends into an object class.

Java is both a compiled as well as an interpreted programming language. [Compiled vs interpreted](https://www.freecodecamp.org/news/compiled-versus-interpreted-languages/)

1. The `.java` file which is human readable (soure code) is first compiled by the compiler

2. This compiler compiles the source code into `.class` bytecode which is an intermediate code that is platform independent

3. The intermediate bytecode is then executed line by line by the interpreter.

### Compiling and running file

To compile file, use the following command. This will create a compiled bytecode `.class` file

```
javac filename.java
```

To run the compiled `.class` file using the interpreter, use the following command with the name of the `.class` file.

```
java filename
```

### Basic file structure

```
public class Demo {
    public static void main(String[] args) {
        System.out.println("Hello World!");
}
```

If the file name is `Demo.java` then the class inside the file should also be named `Demo`. Any other name will not work. The `main`(from psvm) function is the entry point of any java program and therefore is necessary

`public` from `public static void main(String[] args)` is an access specifier. Since `main` is the entry point and without it the program will not run, it is necessary to make it accessible from anywhere, hence it should be specified public.

`static` is used to run the `main` function without creating an object of `class Demo`. In java, everything is based on a class-object relationship. Since main is the entry point, we cannot create an object of `class demo`. In order to create an object, we need to first run the code that creates the object and that is not possible because main is where the program starts running. We use `static` keyword to solve this problem.

`void` is the return type of the main function.

### Classes convention

All class names should begin with capital letters. For example, `Scanner` import used for taking inputs is actually a pre defined class.

### Taking inputs in java

Use the Scanner class to take inputs in java. Do not forget to import the Scanner class using `import java.util.Scanner;`

_This code will go into psvm_

```
Scanner input = new Scanner(System.in);
int number = input.nextInt();
input.close();
```

### Primitive data types

String is NOT primitive data type. It is a class. Following are some primitive data types.

```
int number = 62;
char letter = 'a';
float floatingNumber = 98.34f;
double largeDecimalNumbers = 34337.3433;
long largeInteger = 34329382329328L;
boolean check = false; // or true
```

### Literals and identifiers

A **literal** is a notation for representing a fixed constant value. For example, in `int number = 42` 42 is the literal because 42 is literally 42, a constant. Whereas the variable `number` here is the **identifier**. Methods are also identifiers.

### Typecasting and promotions

A widdening type cast (done automatically by java) is when a smaller type is converted into a larger type. For example, if a float is expected as input and as int is provided instead, java will automatically convert the int to a float.

A narrowing type cast is when a larger type is to be converted to a smaller type. This is not done automatically and needs to be done manually using `(typeToCastInto)(data)`

Types should be compatible in order to cast them. A string cannot be cast into an int

#### Automatic type promotion in expressions

If the larger value being cast into smaller type cannot fit, java will use `(largerValue) % (max value of smaller type)`. For example,

```
int a = 257;
byte b = (byte)(a); // max value of byte is 256, so java will use 257 % 256
System.out.println(b);

//output of this will be 1
```

If an expression uses two different data types, java will use widdening (if compatible) to compute the expression. For example, while carrying out `3 * 5.6` java will convert the entire expression into float and the output will be in float.

## (Video 9) Conditionals

### When to use a for loop and when to use a while loop

**For loop** - Use this when you know how many times the loop is going to run. For example, print the first 10 numbers

**While loop** - Use this when you don't know how many times the loop will run. For example, take input from user until the user presses a particular button.

A while loop also sometimes improves code readability

### Difference between do while and while loop

**do while** - In a do while loop, the loop will execute at least once and then the while condition will be checked. Use in cases where running the loop at least once is a requirement.

**while** - Loop may not even run once if the while condition fails

### Print the nth fibonaci number

```
1. take input
2. num1 = 0, num2 = 0, sum = 0
3. print num1 and num2
3. for(int i = 2; i <= target; i++){
    sum = num1 + num2;
    num1 = num2
    num2 = sum
}
4. print sum
```

### Find occurrence of a digit in a number

```
1. input n and target
2. digit = 0, count = 0;
3. while(n != 0){
    digit = n % 10;
    if(digit == target)
        count++;
    n = n / 10;
}
4. print count
```

### Print reverse of a number

#### My solution

```
1. input n
2. placeExponent = -1, temp = n, ans = 0, digit = 0;
3. figure out placeExponent
    while(temp != 0){
            placeExponent++;
            temp = temp / 10;
    }
4. places = 10 ^ placeExponent // use pow function
5. reverse number
    while(n != 0){
            digit = n % 10;
            ans = ans + places * digit;
            n = n / 10;
            places = places / 10;
    }
6. print ans
```

#### Best solution

```
1. input number
2. ans = 0, digit = 0;
3. reverse number
    while(n != 0){
            digit = n % 10;
            ans = ans * 10 + digit;
            n = n / 10;
    }
4. print ans
```
