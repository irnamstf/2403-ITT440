`MUHAMAD MUQRI BIN ABU HARIRAH | 2022464906 | M3CS2554A | ITT440`
# Comparison Between C And Python

## Origin of the C language
The C language is a imperative language that is commonly used in Unix systems and is the lingua franca of implanted software development. The C language was developed for the Unix operating system by Dennis Ritchie as a systems programming language in 1970. From its inception in the early 1970s, it has grown to become one of the most widely used computer languages ever.


## Why C
* C is easy to debug because it does not require complex statement in execution.
* C is one of the most widely used programming language so there are many existing libraries      and tools are written in C.
* C has fast execution speed because it uses fewer instructions than other programming         
  languages.

## Tools in C language
1) Man Pages - Man command in Linux is used to display the user manual of any command that can 
   run  on the terminal by providing a detailed view of the command which includes NAME,     
   SYNOPSIS, DESCRIPTION, OPTIONS, EXIT STATUS, RETURN VALUES, ERRORS, FILES, VERSIONS, and SEE 
   ALSO. The syntax of Man: '$man [OPTION]... [COMMAND NAME]...'.

2) Editor - The editor that can be used:
  * Vim
  * Nano
  * ee
  * Graphical text editor
  * Online editor

3) Compiler - The two most popular in Linux and Unix operating system:
  * Gcc
  * Clang

## Overview
```c
#include <stdio.h>

int main() {
    int num1, num2, sum;

// Input the first number
printf("Enter the first number: ");
scanf("%d", &num1);

// Input the second number
printf ("Enter the first number: ");
scanf ("%d", &num2);

// Calculate the sum
sum = num1 + num2;

// Display the sum
printf ("The sum of %d and %d is %d\n", num1, num2, sum);

return 0;

}
```
## Output
![Assignment Sir Shahadan](https://github.com/addff/2403-ITT440/assets/166004612/d6a06ccc-923d-4ead-bf27-28f7cc1b87df)

## Origin of Python
Python is programming language that was created by Guido van Rossum in late 1980s as a successor to the ABC programming language. It was created at Centrum Wiskunde & Informatica (CWI) which is situated in the Netherlands. Python is an Open-source, high-level and general-purpose programming language. 

## Why Python
* Python can work wide different platforms such as Windows, Mac or Linux.
* Python is a high-level language so it has a simple syntax similar to the english language.
* Python has syntax that allows developers to write programs with fewer lines than some other     programming language.

## Tool in Python language
* python3

## Overview
```python
def main():
    # Input the first number
    num1 = float(input("Enter the first number: "))

    # Input the second number
    num2 = float(input("Enter the second number: "))

    # Calculate the sum
    sum = num1 + num2

    # Display the sum
    print("The sum of", num1, "and", num2, "is", sum)

if __name__ == "__main__":
    main()

```
## Output
![Assignment Sir Shahadan 2](https://github.com/addff/2403-ITT440/assets/166004612/e179e9c5-c69a-4ba3-96e4-e5789bef7e19)

