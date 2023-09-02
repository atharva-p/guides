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