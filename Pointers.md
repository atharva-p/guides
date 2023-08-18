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