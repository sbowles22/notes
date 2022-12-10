# Chapter 9: Dynamic Memory Allocation
*Pointers are spicy variables, but still variables*

*Lab 12 requires 1-fixed length array and 2-dynamically allocated*

Declared but uninitialized pointers have a random value! Don't use pointers improperly or you will get *undefined behavior!* 😱

Like any other variable, pointers are stored in memory, have specific sizes, and can be changed. Remember `*` dereferences a pointer, and `&` gets the address of a variable. 

Pointers can point to pointers, perhaps that point to other pointers! `int**` points to an `int*` which points to an `int`.

A 3 or 4 star developer is someone who uses to many recursive pointers.

## `malloc`
Short for memory allocate, returns `void*` pointing to beginning of an allocated chunk of memory. Creates a dynamically sized array! `malloc` should pretty much always be called with the `sizeof` operator multiplied by some integer in its parameter. Will return `0` or `NULL` pointer on failure. Make sure to check!

```c
int* x;
```

You should also free up any data you've stopped using. This will be done using `free`. 
## Arrays and Pointers
`x` is the same data type in `int x[]` and `int* x`

```c
int main(void)
{
	int x[5] = {1, 4, 9, 2, 1};
	
	f(x);
	printf("%d", x[0]); // prints 9
}

void f(int* x)
{
	x[0] = 9;
}
```

## Pointer Arithmetic
Integers can be added or subtracted from a pointer to yield a new pointer. This will always be done in increments of the type which the pointer is declared to point to.

```c
int* x; // x = 0x1000 
x++; // x = 0x1000 + sizeof(int) 
```

This means that for arrays, we can add to the array to get the adress of a different element of the array. Basically, $$a + i = \&a[i]$$Pointer arithmetic will take care of the minor details for you. 

## 2-D lists????
Initialization