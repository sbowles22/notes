# Chapter 11: Strings
*C does not have a string data type. You will start to learn that C is very dumb.*

## `char` arrays
Strings in C are declared using `char` arrays and string literals.

```c
char str[17] = "Hello, World!";
```

Just like in normal arrays, excess space in the declared array is filled with 0s. Or the `NUL` charachter. The C language defines this 0 as the end of the string (you can probably see why this is problamatic).

![](https://www.asciitable.com/asciifull.gif)

## `scanf` with Strings
`%s` is the formatting string will take in a whole string. `scanf` will terminate at white space by default, so it can't handle multiple words/space characters.

## `gets` function
NEVER USE THIS. YOU DUMB WHORE. NEVER. DANGEROUS. NO BOUNDS CHECKING.

## `getchar` function
gets one charachter from `stdin`, the safest way to take in charachters.

## `strlen` function
Gets the length of a string, (everything before null terminator).

## `strcpy` function
Copies the second string into the first string. Does not check string length.

## `strcmp` function
Sees if two strings are equal. Returns the difference between the first two unlike charachters. Returns 0 if there is no difference. 

