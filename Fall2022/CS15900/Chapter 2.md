#lecture 

# Chapter 2: Intro to C
*This language is*

## Structure of a C Program

### Preprocessor Directives
Special instructions to the preprocessir that tell it how to prepare your program for compilation.

```c
#include <stdio.h>
#define
```

### Global Declarations
Declaration of "objects" that will be visible (usable) to all parts of the program.

### Main functions
```c
int main(void) {
	// Local Declarations
	// Statements

	return 0;
}
```

### Other Functions
More in [[chapter 4]]!

## Our First Program
```c
#include <stdio.h>  // Preprocessor directives
  // Global declarations (empty)
int main(void) {  // main function
	printf("Hello, World!\n");  // printing

	return 0;  // return 0
}
```

## Comments
- `//` begins a single-line comment
- `/*` begins a multi-line comment
- `*/` ends a multi-line comment

Comments are text not read by the compiler used to notate code.

## Identifiers
**Identifiers** allow us to name data and other objects in a program.

Good
- `numStudents`
- `depth`
- `examAvg`
- `first_lab`
Bad
- `x`
- `DEPTH`
- `exam-avg`
- `1st_lab`
Rules
- The first charachter must be alphabetic
- Must contain only alphabetic, number, and underscores
- Only the first 63 charachters of an identifier are signifigant
- Cannot duplicate a reserved word (`int`, `void`, etc.)

## Types!
C has **strict typing**.

Types dictate:
- the amount of memory necessary to store a value
- how a value is stored in the memory of the computer
- which operations can be performed on the value

### `int`
Number wthout fractional part. C has different sizes of the integer data type:
- `short`
- `int`
- `long`
- `long long`

### `char`
ASCII value of a single letter, number, etc. Dictated with single quotes ('x')

### `bool`
Boolean value (`true`/`false`). We will not use `bool` this semester :(

Analagous to using a nonzero number to represent true and a zero value to represent false.

### `float`
Number with a fractional part. E.g. `3.6` 

Sizes:
- `float`
- `double`
- `long double`

## Variables
A **variable** is a named memory location that has a given type.

**Course standard**: all variables must be declared on their own line that contains a comment.

It is possible to **initialize** a variable at the same time that it is created. E.g.

```c
int count;
count = 0;

int count = 0;
```

## Undefined behavior (UB)
Behavior that the compiler doesn't expect the program to do ever. Don't reference variables before they are initialized.

## Literal Constants
Unamned values used to specify data. E.g. `2` or `3.6`. The compiler assumes the types based on how the literal is written. Use of these structures leads to **hard coding**, forcing the programmer to change all instances of the literal whenever the value needs to be manipulated.

## Defined Constant
the `#define` preprocessor directive is used to create **symbolic constants**. For example:

```C
#define PI 3.141592
```

Always use all uppercase letters for defined constants. *Note the lack of semicolon.* Defined constants take up no memory because the constant is replaced before compilation with its value for every instance.

The `#define` keyword technically is just the decleration for a macro, but in this class, we only use it to declare literal constants.

## Memory Constant
The use of memory constants is discouraged. *Why request memory for a value that wont change?* 
For Example:

```c
const int bruh = 23398;
```

## Formatted I/O
### Output
The `printf` function is used to write to stdout, given a string with format placeholders to be replaced by a value.
	`printf(format string, data list);`

#### Format placeholder codes
*Sub-bullets dictate size charachters to be added.*
- `%d` Integer format
	- `ld` long
	- `lld` long long
- `%f` Float format
	- `lf` double
	- `Lf` long double
- `%c` Charachter Format

#### Placeholder Summary 
`%` + flag + minimum width (+ for right or - for left alligned) + precision (default to 6) + size + code
Use an `*` to leave declaring a width for compile time. 

The order that format variables appear in the string must be held in `printf` args. For example:

```c
float circumfrence = 35.698213;
int decimalPlaces = 2;

printf("Circumfrence: %7.*f\n", decimalPlaces, circumfrence)
```

The output should be:

```
Circumfrence:  35.70
```

### Input
The `scanf` is used to read from stdin. 
	`scanf(format string, address list);`
For example:

```c
int number;

printf("Give me a number -> ")
scanf("%d", &number)
```

## Syntax Errors
Syntax errors are a kind of **compile time error**. If a compile time error is reached, the compiler will not produce an `a.out` file. This is contrasted with a warning, which is the compiler thinking you have made a mistake, but one that is not preventing the code from running *something*. Use `:set nu!` to show line numbers for where the syntax error happened.

## Run Time Errors
The common types are:
- **segmentation fault**: usually an invalid adress (i.e. used a variable name for scanf)
- **floating exception**: usually division by zero :(
- *logical errors*: your implementation or algorithm doesn't work to achieve your goal
Not all run time errors will cause the program to crash.

## Debugging
Time to be a python programmer and add in some printf statements :)

(Or use `gbd`!)