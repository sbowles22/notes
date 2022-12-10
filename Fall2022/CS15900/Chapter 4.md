# Chapter 4: User Defined Functions
*We're turing complete now, but just barely*

Functions are integral in designing complex problems from the **top-down**. Large problems can become very complex, so we can break them up into sub-problems. Additionally, repeated expressions with minor differences can be encapsulated into functions to prevent re-writing the sections. Functions can also be reused in other programs as they can be packaged in libraries (think `printf` and `scanf`). Finally, functions are much easier to test than an entire program, as they are inherently isokated from the rest of the program.

## What entails the good use of a function?
Functions should do **one** task (these are known as **functionally cohesive**) that is not already represented as a built in operator or function.

## Basic Function Termonology
- call - the usage of a function
- calling / called function - the function either calling another function or the function being called.   
- parameters - the inputs to a function, `void` for functions with no parameters
- returning - the value(s) that a function will represent in the calling function
- return type - the type that the function must return, `void` for non-returning functions

## Function Definition
The definition of a function will tell the compiler:
- The return type of the function
- The name of the function
- Any data being sent to the funtion, including their order and type

Examples: 
```c
int my_function(int a, int b) 
{
	return a + b;
}
```

Generalized:
```c
<T> name(<T> var1,...) 
{
	return (T)...;
}
```

Examples of function call:
|                    | Yes parameters | No parameters |
|--------------------|----------------|---------------|
| Yes value returned |  `z = pow(x,y);` |  `z = func();`  |
| No value returned  |  `printf(x);`    |  `greeting();`  |

### Function Headers
Use `:hfx` to insert a function header into a file. **It is course standard to use this before all function declarations.** 