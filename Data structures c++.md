# Bubble sort

```c++ 
void bubbleSort(int* array, int size){
	for (int i = size - 1; i >= 0; i--) { 
		for (int j = 0; j <= i - 1; j++) {  
			if (array[j] > array[j + 1]) {
				// swap positions 
				int temp = array[j]; 
				array[j] = array[j + 1]; 
				array[j + 1] = temp; 
			}
		}
	}
}
```

# abstract data types 

these define data and the operations on data, but provide no implementation details. for example, list is an abstract data type. (lists are implemented as arrays in many programming languages. A linked list is also an implementation of a list)



