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

## array names and pointers

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

### string literals 

string literals always have the type `const char`, but compiler might be lenient in some cases such as 

```c++
char testString[] = "hello"; // the type should've been const char
testString[1] = 'o'; // this is even allowed
```

but this does not work with pointers 

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






