#lecture 

# Chapter 3: Structure of a C program
*The basics+*

## Expressions
An expression always reduces to a single value in the C programming language.

### Operators
"Language specific syntactical tokens that require an action to be taken"

### Operands
"Recieves an operators actions"

Example:
```c
a = 17;  // FIRST OPERATOR
b = 5;   // SECOND OPERATOR

printf("%d + %d = %d\n", a, b, a + b);
```

### Assignment Expression
An assignment operator evaluates the operand on the right side of the assignment operator (`=`) and saves that value in the memory of the variable on the left.

#### Compound assignment
Shorthand for performing single operators on a variable, then storing the value back into said variable.

Examples:
- `+=` Addition
- `-=` Subtraction
- `*=` Muliplication
- `/=` Division
- `%=` Modulus

### Postfix and Prefix Operators
```c
x++; // Returns x then adds one
++x; // Adds one then returns x

x--; // Returns x then subtracts one
--x; // Subtracts one then returns x
```
More than one prefix/postfix on the same variable creates undefined behavior. Referencing a variable after it has been prefixed/postfixed in an expression also creates undefined behavior.

#### Side Effects
Side effects are resolved at the next squence point (usually a `;`).

### Mixed and Single Data Type Expressions
In a single type expression, the result will always be of the same type as the operands.

In a mixed type expression, the result will always be of the larger data type. This is called type  promotion.

#### Type Casting
One can put a type in parentheses to **cast** a value to a different data type.

#### Assignment Conversion
When assigning to a data type different than the target variable causes an implicit type conversion to the target variable's type. **This can be unsafe**. 

### `floor` and `ceil` functions
`floor` returns the largest number less than or equal to the input that is equivilant to an integer but similar in type to the input. 

`ceil` returns the smallest number greater than or equal to the input that is equivilant to an integer but similar in type to the input. 

## Changing the value of a variable
- `scanf`
- assignment operator
- Prefix and postfix operators 

## Selection via Calculation
Instead of using `if`/`else` for selection, one could cleverly use calculations to mimic selection behavior. An example of this can be seen here:

```C
int x;
int y;

x = 5
y = 7

max = y / x * y + x / y * x 
```

Where max will be the larger number. However, this exact approach will not work when x or y is greater than 2y or 2x, respectfully. This is because `y / x` can output a number that is not 0 nor 1.

```c
int factor1;
int factor2;

factor1 = x / y;
factor2 = y / x;

factor1 = (factor1 + 2) % (factor1 + 1);
factor2 = (factor2 + 2) % (factor2 + 1);

max = factor1 * x + factor2 * y;
```

This will fix out previous equation. But again, this program fails to capture an edge case correctly, that being x == y. This edge case can be accounted simply be the addition of the following line.

```c
max /= factor1 + factor2;
```

