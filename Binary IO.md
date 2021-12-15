# Binary I/O
There are different types of files. Instead of working with [text files](File%20IO%20and%20Assertions.md#C%20File%20I%20O) (one byte stores one char through ANSI standard mapping), we work directly with 0's and 1's. We call anything that isn't a text file a "binary file".  
- Storing binary can be much more efficient than text (for some types of data). For example, numbers stored in ANSI uses one byte per decimal digit. Instead of storing 0-255, one byte is used to store only 0-9. 
- Large data files like images, audios, and video files are typically stored in binary format. 
	- If you want to store a lot of 0-255 values (images). In text, storing 255 takes 3 bytes. If we use binary, it only takes 1 byte (8 bits). This reduces size by a factor of three. 

## Reading and Writing to Binary File
Tell C to open a file as a binary file using the `"b"` mode.
```c
FILE *fp = fopen("data.dat", "rb");
```
This will open the file in binary read mode. 

Use `fread` for reading and `fwrite` for writing. 
- Works for arrays, structs, and arrays of structs.
- Useful for reading/writing large amounts of data in one operation.
- It copies bits from disk to memory (`fread`) or memory to disk (`fwrite`).
- Binary files are less portable than text because some types are different sizes on some architectures. 

### fread and fwrite
`fread` and `fwrite` take a pointer to a block of memory, an element size, a number of elements, and a file handle

`fread` reads `size_of_el * num_els` bytes of memory from the file beginning at the fursor location `fp`, and stores them starting at pointer location `where_to`:
```c
int items_read = fread(where_to, size_of_el, num_els, fp);
```

`fwrite` does the opposite, copying data from memory to the specified file:
```c
int items_written = fwrite(where_from, size_of_el, num_els, fp);
```

### Example
```c
// bin_io.c:
#include <stdio.h>

int main() {

	const int SIZE = 100;  
	int arr_write[SIZE];  
	for (int i = 0; i < 100; i++) {
		arr_write[i] = i * 10; 
	}
	FILE *fp = fopen("data.dat", "wb");
	if (!fp) {
		printf("Error opening data.dat\n");
		return 1;
	}
	// writes an array of integers
	fwrite(arr_write, sizeof(arr_write[0]), SIZE, fp);
	fclose(fp);
	
	int arr_read[SIZE];  
	fp = fopen("data.dat","rb");
	if (!fp) {
		printf("Error opening data.dat\n");
		return 1;
	}
	// reads an array of integer
	int num_of_ints = fread(arr_read, sizeof(arr_read[0]), SIZE, fp);
	if(num_of_ints != SIZE) { 
		printf("problem reading data.dat\n");
		return 1;
	}  
	if (feof(fp)) {
		printf("error: unexpected eof\n");
		return 1; 
	}
	if (ferror(fp)) {  
		printf("error reading data.dat\n");
	}  
	for (int i = 0; i < 100; i++) {
		printf("arr_read[%d] = %d\n", i, arr_read[i]);
	}
	fclose(fp); 
}
```