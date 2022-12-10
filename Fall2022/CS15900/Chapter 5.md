# Chapter 5: Selection
*Thou shalt remember, and before or.*

## "Truthiness"
To catagorize all numbers as either true or false -> in c, false is 0 and true is everything else. This applies to anything that compares equal to zero (so `0.0` and `'\0'`, the null delimiter, is false). 

## Logical Operators
Logical operators output an integer 0 or 1.
- `!a` - NOT
- `a && b` - AND (Precedence 5)
- `a || b` - OR (Precedence 4)

```c
!!x  // Same as (x + 2) % (x + 1), but works with negatives.
```

### Short circuiting 
Because the compiler hopes to optimize the speed of the program, and the usage of `&&` and `||` involves two operands, it can lead to situations where the compiler does not evaluate the second operator because it could not change the result of the expression. 
```C
int a = 0
int b = 0
int c;

c = a++ && b++;

printf("%d %d %d", a, b, c); // Output: 1 0 0
```

## Relational (Comparative) Operators
- Comparative (Precedence 9)
	- `a == b` - Is equal to  
	- `a != b` - Is unequal to
- Relational (Precedence 10)
	- `a > b` - greater than
	- `a < b` - less than
	- `a >= b` - greater than or equal to
	- `a <= b` - less than or equal to

## Comparative / Compound Statement
*Operator precedence is very important.*

Incorrect:
```C
int x = 11;

printf("%d", 0 < x < 10); // Output: 1
```

Correct:
```C
int x = 11;

printf("%d", 0 < x && x < 10); // Output: 1
```

Another Example:
```c
int x = 3;
int y = 2;
int z = 3;

 x <= 3 || y >= 2 && z != 3
// TRUE || y >= 2 && z != 3
// TRUE || SHORT CIRCUIT
// TRUE
// Same as: ((x <= 3) || ((y >= 2) && (z != 3)))
```

## Logical Complements
Logical expressions can be redone to give the opposite outputs with the same inputs. 

- The complement of `>` is `<=`
- The complement of `<`  is `>=`
- The complement of `!` is `!!` or `(nothing)` 
- The complement of `&&` is `||`\*

Replacement of all logical expressions with its complementary expression can yield  the logical complement of an expression.
```c
x >  0 && x <  10
x <= 0 || x >= 10
```

Operator precedence must be preserved:
```c
 x >  0 && x <  10  || y != 0
(x <= 0 || x >= 10) && y == 0
```

Not is already a complement operator:
```C
 !(x != 1 || x != 2)
!!(x != 1 || x != 2)
  (x != 1 || x != 2)  // Also Complement
```

`&&` and `||` have an interesting complementary behavior
```c
!x && !y
 x || y
```

```c
x == 0 || y == 0
x != 0 && y != 0
```

## Two Way Selection
*It is 2:00 pm on 10/4/2022 and we are finally learning this.*

One can use `if` and `else` statements to create **branching** code which selects between two possible paths of execution and not running the other.

```c
if (/*Logical Expression*/)
{
	// Code 1
} 
else
{
	// Code 2
}
```

Example:
```c
int change_number(int n)
{
	if (n % 2 == 0)
	{
		n++;
	}
	else
	{
		n--;
	}
	
	return n;
}
```

Note that `n` is returned after the `if`/`else` statements. Try to minimize code in branches for testing and ease purposes. `else` can be optionally omitted. *Never leave a body empty*.

### Nested Selection
`if` statements can be nested for even more complex executions.

```c
if (a)
{
	if (b)
	{
		if (c)
		{
			// Execution code
		}
	}
	else
	{
	// Other execution code
	}

	// More execution code
}
```

### Dangling Else Logical Error
*`{` and `}` arent necessary when making an `if`/`else` statement, however improper use of this fact can lead to unintended effects. We must always use braces in this class as per course standard*

```c
if (x == 3)
	if(y != 2)
		z++;
else
	z--; // Grouped with closest if statement
```

**C does not care about indentation and whitespace.**

## Ternary Operators
Ternary operators can be used to create simple, inline selection statements. They are of the form `(expression) ? true_expression : false_expression` and return the selected value.

Example:
```c
a = (x > y) ? b : c;
```

## `if`/`else if`/`else` Selection
Just as `if/else` statements can be nested to provide more than two branching paths, `else if (expression)` can be placed after an if statement to select one of more than two paths. These constructs can be chained for more than three paths of selection.

Example:
```c
int score;
char grade;
scanf("%d", &score);

if (score >= MINA) 
{
	grade = 'A';
}
else if (score >= MINB)
{
	grade = 'B';
}
else if (score >= MINC)
{
	grade = 'C';
}
else if (score >= MIND)
{
	grade = 'D';
}
else
{
	grade = 'F';
}

printf("%c", grade);
```
*Remember that once any `else if` statement is reached, all preceeding conditions were false, and if found to be true, no remaining conditions are evaluated.* 

## Switch Construct
Switch constructs allow for checking the equivilancy of some variable. The switch case will evaluate all options, running **all** remaining code in the switch statement until it reaches a `break` statement or the end of the switch construct. `default` statements will always run. 
```c
switch(grade)
{
	case 'A':   printf("Great job!!!\n");
				break;
	case 'B':   printf("Well done!!!\n");
				break;
	case 'C':   printf("Okay sure???\n");
				break;
	case 'D':   printf("Do better!!!\n");
				break;
	default:    printf("L + ratio!!!\n");
}
```

Fall through example, this code will run all print statements after a case is met.
```c
switch(grade)
{
	case 'A':   printf("Great job!!!\n");
	case 'B':   printf("Well done!!!\n");
	case 'C':   printf("Okay sure???\n");
	case 'D':   printf("Do better!!!\n");
	default:    printf("L + ratio!!!\n");
}
```

Cases must be unique ICEs (integer constant expressions), so no variables, floating point types, or repeated integral types may be used! All of these will produce compilation errors. 

### Switch Construct Rules
1. The control expression must be integral
2. Each `case` label is the keyword case followed by a constant expression
3. No two `case` labels can represent the same value
4. Two `case` statements can be associated with the same executable statemet
5. The `default` label is neirther required nor must come last
6. There is a maximum of one `default` label
Violations of these rules raise compilation errors. 

## Floating point equality
Floating point numbers are a bitch and you shouldn't compare them directly.
```c
float x = 0.1;
printf("%d\n", x == 0.1)  // False
printf("%d\n", 0.1 * 3 == 0.3)  // False
```

You have to compare the absolute difference against some error.
```c
double epsilon = 0.000001
float x = 0.1;
printf("%d\n", abs(x - 0.1) < epsilon)  // True
```

