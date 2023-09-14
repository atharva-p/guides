`void*` pointers cannot be dereferenced, nor can you use pointer arithmetic's on
`void*` pointers 

# explicit typecast to `void*` in case of using `std::cout` 

```cpp 
int main() {
	int i = 1025; 
	int* intPointer = &i; 

	std::cout << "size of integer " << sizeof(int) << std::endl;
	std::cout << "address = " << intPointer << " value = " << *intPointer << std::endl;

	char* charPointer = (char*)intPointer;

	std::cout << "size of char " << sizeof(char) << std::endl; 
	std::cout << "using c++ std cout" << "address = " << charPointer << " value = " << *charPointer << std::endl; 
	printf("using c prinf, address = %p, value = %x", charPointer, *charPointer);

	return 0; 
}
```

the output is as follows 

```
size of integer 4
address = 000000E5932FF674 value = 1025
size of char 1
using c++ std coutaddress =  value = 
using c prinf, address = 000000E5932FF674, value = 1
```

the `std::cout` does not work properly in this case because cpp's `cout` function expects a null termination string (`\0`) to consider the end of the string. So it will keep on looking at the next address until it encounters a null termination character

this check is also performed by the C's `printf()` but that is only if the format specifier is set to `%s` which is for strings. we're using `%p` and `%x` which is for addresses and hexadecimal numbers. 

to fix this problem we can do the following with the c++ style code

```cpp 
std::cout << "using the c++ cout function " << "address = " << (void*)charPointer << " value = " << *(int*)charPointer << std::endl;
```

this will fix the address error but in the value you'll end up getting 1025 (unlike 1 for the C code). this is because you cannot dereference a void pointer and dereferencing an `int` pointer means that c++ will consider the next 4 bytes in memory to print as an integer

we can only print the address in case of a `void*` pointer. 

# Pointer to pointer

```c++
#include <iostream> 
int main() {
	int i = 10; 
	int* intPointer = &i; 

	int** pointerToPointer = &intPointer; 
	return 0;
}
```

# Pointers and arrays 

let A be the name of an array 

`*(A + i)` is the same as `A[i]` and 

`(A + i)` is the same as `&A[i]` 

we have the following array, we can declare a pointer to that array by assigning the address of the first element of that array

```c++
int array[5] = {2, 3, 4, 5, 6}; 
int* arrayPointer = &array[0]; 

std::cout << *(arrayPointer + 1) << std::endl; 
```

this will print `3` since we are incrementing the address from the pointer by 1. 

Writing `array` is analogous to `&array[0]` so the above code can also be written as

```c++
int* arrayPointer = array; 
std::cout << *(arrayPointer + 1) << std::endl; 
// std::cout << *(array + 1) << std::endl; will also work
```

`(array + i)` is the same as `&array[i]`. Address of the first element of the array is known as the base address of the array 

consider this 

```c++ 
int* arrayPointer = &array; 
arrayPointer++; // valid 
array++; // invalid
```

You can use a pointer with the array\[index] syntax too 

```c++
int arr[5] = {1, 2, 3, 4, 5}; 
int* p1 = arr; 

std::cout << p1[0] << std::endl; // will print 1 
std::cout << &p1[0] << std::end; // will print the address of 1
```

## arrays as function arguments 

when an array is a parameter for a function, the c++ compiler will use call by reference instead of call by value, which means that 

```c++ 
int someFunction(int array[]){}; 
// is interpreted as
int someFunction(int* array) {}; // pointer to the first element of the array  
```

### why won't this work? 

```c++
void someFunction(int array[]){ // interpreted as int* array
	std::cout << sizeof(array) << std::endl; // expected: 20 bytes
	std::cout << sizeof(array[0]) << std::endl;  // expected: 4 bytes 
}

int main(){
	int a[5] = {1, 1, 1, 1, 1}; 
	std::cout << a << std::endl;  // address of first item of a 
	std::cout << sizeof(a) << std::endl; // address of the array a (4 * 5 = 20bytes)
	someFunction(a); 
}
```

output: 

```
0000006692F8F878
size of the array 20
size of the pointer that holds the memory location of the first element of the array 8
4
```

we don't get the expected 20 bytes size of the array from the function's local scope because we're actually finding the `sizeof(int* array)`, it's a pointer, not the size of the array. size of pointers is 8 bytes in a 64 bit system and 4 bytes in a 32 bit system. 

`&array[0]` and `array` are actually the same thing because of the way compiler interprets arrays and pointers 

keep in mind that array names used to denote addresses are different than pointers that store addresses. pointer arithmetic cannot be applied to array names. 

# character arrays (strings) and pointers 

## ways to store strings *using c* 

```c++
// string literal
char name[5] = "JOHN" // the null termination character is implicit in this case. One byte extra for the null character
char name[] = "JOHN" // compiler can also figure out the size

// using comma separateed list 
char name[] = {'J', 'O', 'H', 'N', '\0'} // null character is explicit

// can also store manually using the indices 
char name[5]; 
name[0] = 'J'; 
name[1] = 'O'; // and so on 
```

character arrays and pointers can be used in a similar way to what is described in _pointers and arrays_ 

```c++ 
#include <iostream> 

int main(){
	char name[] = "JOHN"; 
	char* stringPointer = &name[0]; 

	std::cout << "before changing " << name << std::endl; 
	stringPointer[1] = 'A';  // same as *(stringPointer + 1)
	// you can also write
	// *(name + 1) = 'A'; since name will denote the address of first element of the char array 

	std::cout << "after changing " << name << std::endl; 
	return 0;
}
```

```
before changing JOHN
after changing JAHN
```

### string literals and `const char` 

string literals always have the type `const char`, but compiler might be lenient in some cases such as 

```c++
char testString[] = "hello"; // the type should've been const char
testString[1] = 'o'; // this is even allowed
```

but the compiler is type strict in other cases, and this does not work with pointers 

```c++ 
void customPrint(const char* charPointer) { // without const char* this wil not work. 
	while (*charPointer != '\0') {
		std::cout << *charPointer << std::endl; 
		charPointer++; 
	}
	std::cout << '\0' << std::endl; 
}

int main() {
	const char testString[] = "hello";
	customPrint(testString); 
	return 0; 
}	
```
# Pointers and multidimensional arrays 

## type mismatch while assigning addresses to arrays 

```c++ 
int testArr[2] = {1, 2}; 
int* pointer = testArr; // allowed

int* pointer = &testArr; // not allowed, a type of int (*[2])pointer is expected

int (*pointer)[2] = &testArr; // allowed
```

just assigning `testArr` to `int*` pointer is valid because `testArr` will be resolved to the address of the first element of the array, which is an integer. 

however, assigning `&testArr` to the `int*` pointer will result in a type mismatch because it resolves to the address of the entire array. 

## using pointers with multidimensional arrays 

```c++
#include <iostream> 

int main(){
	int testArr1[2][3] = { {1, 2, 3}, {4, 5, 6} }; 
	
	int (*p1)[3] = testArr1;

	std::cout << p1 << " with type " << typeid(p1).name() << std::endl;
	std::cout << *p1 << " with type " << typeid(*p1).name() << std::endl;
	std::cout << p1 + 1 << " with type " << typeid((p1 + 1)).name() << std::endl;
	std::cout << *(p1 + 1) << " with type " << typeid(*(p1 + 1)).name() << std::endl;
	std::cout << (*(p1 + 1) + 2) << " with type " << typeid((*(p1 + 1) + 2)).name() << std::endl; 
	std::cout << *(*p1 + 1) << " with type " << typeid(*(*p1 + 1)).name() << std::endl;


	return 0;
} 
```

output 

```
00000095B99CF778 with type int (* __ptr64)[3]
00000095B99CF778 with type int [3]
00000095B99CF784 with type int (* __ptr64)[3]
00000095B99CF784 with type int [3]
00000095B99CF78C with type int * __ptr64
2 with type int
```

## declaring a 3-dimensional array 

```c++
#include <iostream> 

int main() {
	int arr[3][2][2] = { {{1, 2}, {3, 4}}, {{5, 6}, {7, 8}}, {{9, 10}, {11, 12}} }; 

	int(*p1)[2][2] = arr; 

	std::cout << p1 << " with type " << typeid(p1).name() << std::endl; 
	std::cout << *p1 << " with type " << typeid(*p1).name() << std::endl;
	std::cout << **p1 << " with type " << typeid(**p1).name() << std::endl;
	std::cout << ***p1 << " with type " << typeid(***p1).name() << std::endl;
	return 0; 
}
```

output 

```
0000000B3E11F4F8 with type int (* __ptr64)[2][2]
0000000B3E11F4F8 with type int [2][2]
0000000B3E11F4F8 with type int [2]
1 with type int
```

## dereferencing arithmetics 

![](Pasted%20image%2020230826185416.png)

## passing multidimensional arrays to functions 

```c++
#include <iostream> 

void receiveOneDimArr(int* arr) {
	std::cout << arr << std::endl;
}

void receiveTwoDimArr(int(*arr)[2]) {
	std::cout << arr << std::endl; 
}

void receiveThreeDimArr(int(*arr)[2][2]) {
	std::cout << arr << std::endl; 
}

int main() {
	int oneDimArr[2] = { 1, 2 }; 
	int twoDimArr[2][2] = { {1, 2}, {3, 4} }; 
	int threeDimArr[3][2][2] = { {{1, 2}, {3, 4}}, {{5, 6}, {7, 8}}, {{9, 10}, {11, 12}} };

	receiveOneDimArr(oneDimArr); 
	receiveTwoDimArr(twoDimArr); 
	receiveThreeDimArr(threeDimArr); 

	return 0;
} 
```

# Pointers and dynamic memory 

## memory structure of an application 

![](Pasted%20image%2020230826202125.png)

## allocation 

Dynamic memory is the heap memory (or the RAM of the system). dynamic memory allocation in C can be done with mainly four functions. these can also be used in c++ 

1. malloc 
2. calloc 
3. realloc 
4. free 

in c++ this can be done using 
1. new 
2. delete 

malloc (and calloc, realloc) will return a void pointer that will be needed to be typecast into the correct type so we can use the pointer obtained to dereference it (since void pointers cannot be dereferenced). 

```c++ 
int* pointer = (int*)malloc(20 * sizeof(int)); // will return a block of memory with space for 20 integers
```

calloc will take two arguments. Unlike malloc, calloc will actually initialize values to all positions with value 0 (instead of garbage wtih malloc). 

```c++ 
int* pointer = (int*)calloc(20, sizeof(int)); // calloc(number of elements, size of one element)
```

realloc is used to change the size of a block of memory. you can also reduce the size. realloc will copy the values from the previous memory block to the new memory block. 

```c++
int* new_pointer = (int*)realloc(pointer, 3 * sizeof(int)) // realloc(old_pointer, new size)
```

passing NULL to realloc's old_pointer parameter makes realloc equivalent to calling malloc 

```c++
int* pointer = (int*)realloc(NULL, 20 * sizeof(int)); 
```

### c++ allocation 

```c++ 
data_type *pointer_name = new data_type;
// use the pointer obtained 
// free the memory used 
delete pointer_name; 
```

```c++
// example 
int *intPtr = new int;
*intPtr = 42;

// Use intPtr as needed

delete intPtr; // Don't forget to free the memory when you're done using it
```

allocation (and deallocation) for arrays 

```c++ 
date_type *pointer_name = new data_type[size]; 
// use the pointer obtained 
// free the resources 
delete[] pointer_name; 
```

# returning pointers from functions 

## unsafe returning of a pointer from a function

```c++
#include <iostream> 

int* add(int* x, int* y) {
	int c = (*x) + (*y); 
	return &c; 
}

int main() {
	int a = 1, b = 2; 

	int* answer = add(&a, &b); 
	std::cout << *answer << std::endl; 
	return 0;
}
// output 3 (still works because the memory address of c is yet to be overwritten by something else)
```

`int* add(int*, int*)` returns a pointer to a variable that is local to the `add()` function. This is unsafe because after the execution of `add()`, it is removed from the stack and all of the memory allocations (including address of c) to `add()` are free to be used by other functions. 

we can test that it is unsafe by calling another function (thereby making it allocate memory that was once occupied by `add()`) right before we dereference the address used by `c` 

```c++
#include <iostream> 

int* add(int* x, int* y) {
	int c = (*x) + (*y); 
	return &c; 
}

void printSomething() {
	std::cout << "this is a long sentence to be printed for seemingly no reason" << std::endl; 
}

int main() {
	int a = 1, b = 2; 

	int* answer = add(&a, &b); 
	printSomething(); 
	std::cout << *answer << std::endl; 
	return 0;
}
```

output 

```
this is a long sentence to be printed for seemingly no reason
32762 //wrong output 
```

this can be solved by making a call to malloc and instead storing the answer in the heap. 

```c++
#include <iostream> 
#include <stdio.h>
#include <stdlib.h> 
int* add(int* x, int* y) {
	int* c = (int*)malloc(sizeof(int)); 
	*c = *x + *y; 
	return c; 
}

void printSomething() {
	std::cout << "this is a long sentence to be printed for seemingly no reason" << std::endl; 
}

int main() {
	int a = 1, b = 2; 

	int* answer = add(&a, &b); 
	printSomething(); 
	std::cout << *answer << std::endl; 
	free(answer); 
	return 0;
}
```

# Function pointers 

Pointers can also point to functions. A function is a set of instructions stored in a contiguous block of memory (for most programming languages). This block is called the function's code segment or the text segment. Pointers that store address to functions store the address of the entry point of the function. 

You can use pointers to call functions and to pass functions as arguments to other functions. You cannot perform pointer arithmetic on pointers to functions.

## declaring function pointers 

use this syntax `return_type (*pointer_name)(function_signature) = &function_name ` 

```c++
#include <iostream> 
#include <stdio.h> 
#include <stdlib.h> 

int add(int a, int b) {
	int ans = a + b; 
	return ans; 
}

int main() {
	int a = 10, b = 20; 
	// function pointer to add 
	// return_type (*pointer_name)(function_signature) = &function_name 
	int (*funcPointer)(int, int) = &add; 

	//calling the function using the pointer 
	int answer = (*funcPointer)(a, b); 
	std::cout << answer << std::endl; 

	return 0;
}
```

## syntactical convenience 

```c++
#include <iostream> 
#include <stdio.h> 
#include <stdlib.h> 

int add(int a, int b) {
	int ans = a + b; 
	return ans; 
}

int main() {
	int a = 10, b = 20; 
	int (*funcPointer)(int, int) = add; 

	//calling the function using the pointer 
	int answer = funcPointer(a, b); 
	std::cout << answer << std::endl; 

	return 0;
}
```

instead of `&function_name` just `function_name` is also fine. and to call the function using pointer you can use the name of the pointer `pointer_name(arguments)` instead of having to dereference the pointer. 

## why use parenthesis for the declaration? 

without the parenthesis, the compiler will interpret the pointer declaration as a function declaration instead

```c++
int *pointer_name(int, int) = &function_name // error because this is a function that is named "pointer_name" that returns an integer pointer
```

## another example 

```c++
#include <iostream> 
#include <stdio.h> 
#include <stdlib.h> 

int add(int a, int b) {
	int ans = a + b; 
	return ans; 
}

void printGreeting(char* name) {
	std::cout << "hello " << name << std::endl; 
}

int main() {
	char myName[20] = "Atharva"; 

	void (*pointer)(char*) = &printGreeting;
	(*pointer)(myName);

	return 0;
}
```

## how NOT to dereference

```c++ 
// will result in a compiler error
*(functionPointer)(arguments); 

// correct way 
(*functionPointer)(arguments); 
```
# function pointers and callbacks 

A callback function is a function that is passed to another function as a argument and can be called by the caller function. 

with callback functions, you can have a modular function (a caller function) and you can change the behavior of some part of that function (a module or a callback) by changing the callback function passed to that caller function. 

following is an example of callback functions being used to specify the ranking mechanism of bubble sort 

```c++
#include <iostream> 
#include <cstdlib>

void printArray(int* array, int size) {
	for (int i = 0; i < size; i++) {
		std::cout << array[i] << " "; 
	}
	std::cout << "\n"; 
}

int compare(int a, int b) {
	if (a > b) {
		return 1;
	}
	else
		return 0;
}

int absoluteCompare(int a, int b) {
	if (std::abs(a) > std::abs(b)) {
		return 1;
	}
	else {
		return 0; 
	}

}

void bubbleSort(int* array, int size, int (*rankCallback)(int, int) ) {
	for (int i = size - 1; i >= 0; i--) { 
		for (int j = 0; j <= i - 1; j++) {  
			if (rankCallback(array[j], array[j + 1])) {		// array[j] > array[j + 1]
				// swap positions 
				int temp = array[j]; 
				array[j] = array[j + 1]; 
				array[j + 1] = temp; 
			}
		}
	}
}

int main() {
	//int test[6] = { 1, 10, 11, 7, 6, 5 }; 
	int test[6] = {-31, 22, -1, 50, -6, 4};

	int size = sizeof(test) / sizeof(test[0]); 

	bubbleSort(&test[0], size, &compare); 
	printArray(test, size); 

	return 0;
}
```

output `-31 -6 -1 4 22 50` 

if we change the code to `bubbleSort(&test[0], size, &absoluteCompare)` we would the array sorted ignoring the size of the integers

output `-1 4 -6 22 -31 50`

note that we never had to change the implementation of our `bubbleSort()` function to change sorting order (ascending / descending) or the way numbers are ranked (ignoring signs). we did this by writing separate callback functions for each use case and just passing those to our `bubbleSort()` function. 

callbacks are used in event handling. 

# Memory leaks 

memory leaks occur when unreferenced blocks of memory stay in the heap (as a result of not being deallocated using `delete` or `free` for C) or more blocks of memory are being added to the heap without releasing them when they are not needed. 

this can occur if the pointer that points to heap memory block is a local variable on the stack for a function and multiple calls are made to that said function. This results in multiple calls to dynamic memory allocation, each time with a different pointer variable, resulting in the allocation of a different memory block. This consumes more and more heap memory overtime. 

memory leaks are not just about not having unreferenced memory, they also occur when memory that is not being used isn't deallocated. 





