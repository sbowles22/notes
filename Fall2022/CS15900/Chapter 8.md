# Chapter 8: Arrays
*Here's where C starts getting really funky.*

## Definition of an Array
An **array** is a **consecutive** series of **variables** that share one name and data type. Each variable, or **element**, of an array has a number known as an **index value** that represents its position in an array. When we reference the name of the array allong...

## Creating an Array
Every array needs a **name**, **data type**, and **size**. 

General:
```c
type array[size];
```

Examples:
```c
int nums[10];
double florts[78];
```

Course standard! *All arrays will be **static** (of fixed-length) until we introduce the topic of **dynamic** memory allocation.*

## Array Initialization
One can put an initialized value for an array during its creation with a set of curly braces.

```c
int data[5] = {1, 2, 0, 9, 219038};
```

Providing too many elements for the size causes a compilation error, but too few elements is okay!

```c
int data[500] = {1, 2, 3};
```

If at least one value is provided, all unassigned values will be initialized to **zero**!

Idiomatic:
```c
int more_data[500] = {0};
```

### Accessing Elements in an Array
Index elements are integral expressions (notably not required to be constant!)

```c
int data[500] = {1, 2, 3};

printf("%d\n", data[8]); // prints 0
```

Negative value indecies are undefinied behavior!

## Inputting Array Values

```c
scanf("%d", &data[5]);
data[7] = 23;
```

## Printing Arrays
No `repr` functions, so a loop must be used.

## Out of Bounds Access
Logical error, will not throw an error, but will still exibit undifined behavior. It could also be a segmentation fault if the array access is outside the bounds of permitted memory. Indecies merely multiply and add the length of the data type to the array pointer. 

### Possible Observations
- No problem, works as expected >> value likely just above array length, writes to memory that program has not allocated
- Program produces unusual behavior >> value likely signifigantly above array length, writes to memory that program is using and has other information in it 
- Program crashes, *seg fault* or *stack smashing* >> value likely far above array length, program is killed by OS b/c program attempts to manipulate unpermitted memory

## Arrays and Function (Inter-function Communication)
We can either pass **elements** or the **entire array**, both work, but behave differently.

### Passing Elements
Elements of an array behave like the element data type. Nothing special needs to be done here. 

Example:
```c
int i;
int factorial;
int nums[ARRAY_LENGTH] = {1, 2, 4, 5, 1};

for (i = 0; i < ARRAY_LENGTH; i++)
{
	factorial = calc_factorial(nums[i]);
	printf("%d! = %d\n", nums[i], factorial)
}
```

But just like variables, they are passed by value. Pass by adress can still be done though.
```c
int i;
int nums[ARRAY_LENGTH] = {1, 2, 4, 5, 1};

for (i = 0; i < ARRAY_LENGTH; i++)
{
	add_two(&nums[i]); // Passes element i by address
	printf("%d + 2 = %d\n", nums[i] - 1, nums[i]) // {3, 4, 6, 7, 3}
}

void add_two(int* p_num)
{
	*p_num += 2;
}
```

### Passing Arrays
We can also pass the entire array as a parameter. We do not include square braces, the size of the array, or the data type of the array when calling.

```c
void add_two(int[], int); // Declaration

int main(void)
{
	int nums[ARRAY_LENGTH] = {1, 2, 4, 5, 1};
	add_two(nums, ARRAY_LENGTH);
	
	for (i = 0; i < ARRAY_LENGTH; i++)
	{
		printf("%d + 2 = %d\n", nums[i] - 1, nums[i]) // {3, 4, 6, 7, 3}
	}
}

void add_two(int nums[], int length) // Definition
{
	i = 0;
	for (i = 0; i < length; i++)
	{
		nums[i] += 2;
	}
}
```
*Note: arrays are always passed by address. Indecies are offsets. All array accesses use pointer artihmetic. To avoid side effects, a copy of the array must be made.*

### Returning Arrays
`int[] f(void)` is not a valid function definition. Returning an array pointer will also cause an error. You should declare an array in main, and manipulate it in the function by passing it by address (which arrays always are).

```c
void add_two(int numsp[], int length)

int main() 
{
	int x[LEN];
	add_two(x, LEN);
}

void add_two(int nums[], int length) // Definition
{
	i = 0;
	for (i = 0; i < length; i++)
	{
		nums[i] += 2;
	}
}
```

### Summary
Obj | By Val? | By addr? | Ret?
---|---|---|---
var | default | & * | Yes 
array elem | default | & * | Yes
array | N/A | default | No

# END OF CONTENT FOR EXAM 2!!!

## Arrays and Measures of Efficiency

Write a function that reverses the elements of an array `x[SIZE]`

```c
void revArray(int x[])
{
	int y[SIZE];
	int i;
	
	for (i = 0; i < SIZE; i++)
	{
		y[i] = x[SIZE - i - 1];
	}
	
	for (i = 0; i < SIZE; i++)
	{
		x[i] = y[i];
	}
}
```

I mean it works??? But it's not *efficient*. It needs an extra `int[SIZE]` array! It also takes `SIZE*2` loop iterations.

```c
void revArray(int x[])
{
	int temp;
	int i;
	
	for (i = 0; i < SIZE / 2; i++)
	{
		temp = x[i];
		x[i] = x[SIZE - i - 1];
		x[SIZE - i - 1] = temp;
	}
}
```

This is much better! It only needs an extra `int` of memory, and it only takes `SIZE / 2` loop iterations!

## Sorting Arrays
*Lists refer to subsections of an array. Pass is one iteration of the algorithm.*

### Selection Sort!
In place modification (by not creating another list). Designates a sorted list and an unsorted list. The sorted list is of an initial size of zero. The implementation will be S <- L, where the unsorted list is on the left and the array will be sorted from smallest to largest. Selection sort will swap the minimum/maximum value of the unsorted array with leftmost/rightmost element of the unsorted array.

```c
selection_sort(int nums[], int len)
{
	int i;
	int j;
	int temp;
	
	for (i = 0; i < len; i++)
	{
		for (j = i + 1; j < len; j++)
		{
			if (nums[i] > nums[j])
			{
				temp = nums[i];
				nums[i] = nums[j];
				nums[j] = temp;
			}
		}
	}
}

/*
Swap the minimum unsorted with the leftmost unsorted. "|" designates sorted and unsorted parts of the list. 

{| 15, 21, 24, 12, 18, 20} Swap 12 & 15
{12, | 21, 24, 15, 18, 20} Swap 15 & 21
{12, 15, | 24, 21, 18, 20} Swap 18 & 24
{12, 15, 18, | 21, 24, 20} Swap 20 & 21
{12, 15, 18, 20, | 24, 21} Swap 21 & 24
{12, 15, 18, 20, 21, 24 |} Done, len - 1 passes
*/
```

### Bubble Sort!
Bubble sort will compare every adjacent pair of elements, and swap them if they are out of order. The example is also S <- L. 

```c
bubble_sort(int nums[], int len)
{
	int i;
	int j;
	int temp;
	
	for (i = 0; i < len; i++)
	{
		for (j = len - 1; j > i; j--)
		{
			if (nums[j - 1] > nums[j])
			{
				temp = nums[j - 1];
				nums[j - 1] = nums[j];
				nums[j] = temp;
			}
		}
	}
}

/*
Swap adjacent elements if unsorted. "|" designates sorted and unsorted parts of the list. 

{| 15, 21, 24, 12, 18, 20}
{12, | 15, 21, 24, 18, 20}
{12, 15, | 18, 21, 24, 20}
{12, 15, 18, | 10, 21, 24}
{12, 15, 18, 20, | 21, 24}
{12, 15, 18, 20, 21, 24 |} 
*/
```

### Insertion Sort!
Insertion sort repeatedly inserts the leftmost/righmost value into its correct place in the sorted array, shifting over the other elements in the sorted array. The example is also S <- L. 

```c
insertion_sort(int nums[], int len)
{
	int i;
	int j;
	int k;
	int temp;
	
	for (i = 1; i < len; i++)
	{
		for (j = 0; j < i; j++)
		{
			if (nums[j] > nums[i])
			{
				temp = nums[i];
				for (k = i; k > j; k--)
				{
					nums[k] = nums[k - 1];
				}
				nums[j] = temp
			}
		}
	}
}

/*
Inserts the leftmost value from the unsorted list into the correct point in the sorted array. "|" designates sorted and unsorted parts of the list. 

{15, | 21, 24, 12, 18, 20}
{15, 21, | 24, 12, 18, 20}
{15, 21, 24, | 12, 18, 20}
{12, 15, 21, 24, | 18, 20}
{12, 15, 18, 21, 24, | 20}
{12, 15, 18, 21, 20, 24 |}
*/
```

## Searching

### Sequential Search
Go through every element sequentially to find element. It is assumed that elements are unique in array.

```c
sequential_search(int nums[], int length, int target)
{
	int i = 0;
	int index = NOT_FOUND;
	
	for (i = 0; i < length; i++)
	{
		if (nums[i] == target)
		{
			index = i;
			i = length;
		} 
	}
		
	return i;
}
```

### Binary Search
Go through every element starting at middle of knowlege. It is assumed that elements are unique in array and the array is sorted.

```c
binary_search(int nums[], int length, int target)
{
	int index;
	int mid;
	int first;
	int last;

	index = NOT_FOUND;
	first = 0;
	last = length - 1;
	
	do
	{
		mid = (first + last) / 2;
		
		if (nums[mid] > target)
		{
			last = mid - 1;
		}
		else if (nums[mid] < target)
		{
			first = mid + 1;
		}
		else
		{
			index = mid;
			last = first - 1; // break
		}
	} while (first <= last);

	return index;
}
```