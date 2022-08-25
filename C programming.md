## Head first C
[book](file:///C:/Users/Willem/OneDrive/Documents/Textbooks%20&%20User%20Manuals/Electrical%20&%20Computer/Programming%20Embedded%20Systems%20With%20C%20and%20GNU%20Development%20Tools,%202nd%20Edition%20-%20Michael%20Barr,%20Anthony%20Massa.pdf)
```bash
gcc hello_world.c -o hello_world
./hello_world
```
`-o file` Place the primary output in file *file*.

The *stdio* library contains code that allows you to read and write data from and to the terminal.

Return type of main() is `int` → 0 means success.

## Declaration & initialization
```c
int var=value;
int var1, var2, var3;
```
Use 'unsigned'. Default is signed.

## Functions
A function declaration tells the compiler about a function's name, return type, and parameters. A function definition provides the actual body of the function.

Put GCC compile command as comment in first line
```c
// gcc -std=c99 -o go go.c neuron.c -lm -Wall -Werror
// gcc -g -Wall -o add add.c -lm
```

Debugging: 
```c
-g 
-ggdb
```

## Headers, libraries and linking

For functions in external .c file: header file can be thought of as interface between source code and the programmer.

.h file contains function declarations or definitions to be used in main program. A .c file can contain the rest of the function definitions of only declarations are given in .h

Never put anything other than function prototypes/declarations, variable declarations, includes and macros inside a header file.

Use compiler option `-Idir` to link to directory not in current.

# Images

![[C-variables.png|600]]
![[C-operators.png|600]]
