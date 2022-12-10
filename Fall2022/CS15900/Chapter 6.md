# Chapter 6: Repetition
*Chapter 6: Repetition, Chapter 6: Repetition, Chapter 6: Repetition*

## Terminology:
- loop - one of two possible techniques of repetition, utilizes a contruct to repeat designated statements undar a predetermined set of conditions
- loop iteration - one execution of the instructions inside the body of the loop construct
- loop control expression - the logical expressino to determine whether the loop should initiate another iteration
- loop initialization - preperation work to be completed before the first evaluation of the loop control expression
- loop update - an executable statement found inside the body of the loop that when executed a sufficient number of time will lead to a change in the evaluation of the loop control expression
- loop control variable - the variable that is initialized, part of the loop control expression, and the recipient of the update action

## Pre-test loops vs. Post-test loops
Pretest loops run the loop control expression then the body if true, repeating. Post-test loops run the body then the loop control expression, repeating if true. Pre-test loop bodies are not garunteed to run as a result, whereas post-test loop bodies are garunteed to run at least once. Try to use a post-test loop when otherwise code would need to be repeated.

## Counter-controlled process vs. event-controlled process
Counter-controlled processes have a known number of iterations, whereas even-controlled processes. Input validation, making sure an input is a value which the program is designed to handle, is a great example of an event-controlled process.

### Input Validation 
*This course will be required to perform input validations on the range of data. Data type valiation is not required. It is preferred to have individual UDFs for each inputs to be validated.*

## `while` loops
`while` loops are pre-test loops. Basic syntax:
```C
while (expression)
{
	// executable statements
	// will repeat until expression is false
}
```

Example:
```c
int calc_factorial(int num)
{
	int fact = 1;

	while (num > 0)
	{
		fact *= 1;
		num--;
	}

	return fact;
}
```

## `do-while` loops
`do-while` loops are post-test loops. Basic syntax:
```C
do
{
	// executable statements
	// will repeat until expression is false, but at least once
} while (expression);  // on same line as closing brace by course-standard
```

Example:
```c
int get_number()
{
	int buf;

	do
	{
		printf("Enter a number n to calculate n! -> ")
		scanf("%d", &buf)

		if (num < 0)
		{
			printf("Error: Enter non-negative number\n");
		}
	} while(num < 0);

	return num;
}
```

## `break` and `continue`
Don't use 'em in loops. Life is easier that way :D

## Calculating a Range of Factorials
```c
int calc_factorial(int);
int get_start(void);
int get_end(int);
void display_results(int, int)

int main(void)
{
	int fact;
	int start;
	int end;

	start = get_start();
	end = get_end(start);

	while (start <= end)
	{
		fact = calc_factorial(start);
		display_results(start, fact);
		start++;
	}
}
```

```c
int get_start(void)
{
	int buf;
	do 
	{
		printf("Input start -> ");
		scanf("%d", &buf);
		
		if (buf < 0)
		{
			printf("ERR: non-negative number required!\n");
		}
	} while (buf < 0); 

	return buf;
}
```

```c
int get_end(int start)
{
	int buf;
	do 
	{
		printf("Input end -> ");
		scanf("%d", &buf);
		
		if (buf < start)
		{
			printf("ERR: end mustn't be smaller than start!\n");
		}
	} while (buf < start); 

	return buf;
}
```

## Infinite loops
*You can always quit your code with `ctrl + C`* 

```c
do {
	printf("Input start -> ");
	scanf("%d", &buf);
} while (buf < 0 && buf > 0);
```

You can use `printf("%d", num); fflush(stdout);` to help diagnose infinite loop statements.

## `for` Loops!
The third and final looping construct in the C programming language is the `for` loop. `for` loops have the initialization, loop control expression, and loop update all together. These are usually used for counter controlled processes. *Its just a compressed and preformatted typical while loop.*

Syntax:
```c
for (expr1; expr2; expr3)
{
	// Code
}
```

Example:
```c
for (int i = 0; i < 5; i++)
{
	printf("%d\n", i);
}
```

Is the same as:
```c
int i = 0;
while (i < 5)
{
	printf("%d\n", i);
	i++;
}
```

Example:
```c
for (;;) // infinite loop, equivilant to `while (1 == 1)`
```

## Rearranging Digits in a Number Example
*I really can't be bothered to write out the whole code, he's going fast; left as exersise for the reader*

```c
int main()
{
	int number;
	int sorted;

	number = get_number();
	sorted = sort_digits(number);
	printf("%d\n", sorted);
	
	return 0;
}
```

```c
int rearrange(int number)
{
	int sorted;
	int zeros;
	int max_digit;
	int max_location;

	sorted = 0;
	zeros = count_zeros(number);
	while (number > 0)
	{
		max_digit = find_max(number, &max_location);
		number = remove_max(number, max_digit, max_location);
		sorted = append_max(sorted, max_digit);
	}

	sorted *= pow(10, zeros);
	
	return sorted
}
```

## Recursion!
*Finally >:)*

Recursion is when a function calls itself. This can be used to create repition without loops. This is equivilant to loops by the church-turning equivilance theorem (*That Turing Paper, like, the **one***). A base case must be used so that the recursion is not infinite. Recursive calls store the current call in memory, so don't use them for infinite loops.

Example:
```c
int factorial(int num)
{
	int res;
	
	if (num == 0)
	{
		res = 1;	
	}
	else
	{
		res = num * factorial(num - 1);
	}

	return res;
}
```

or...
```c
int factorial(int num)
{
	return (num == 0) ? 1 : num * factorial(num - 1);
}
```

or!
```c
int f(int n){return n==0?1:n*f(n-1);}
```
Code golfing is a way of life.

### Event Controlled Recursion
*Probably shouldn't do this.*
Could lead to stack overflows.