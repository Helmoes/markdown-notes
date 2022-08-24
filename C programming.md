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

# Head first C

```bash
gcc main.c -o main
./main
```

# Images

![[C-variables.png]]
![[C-operators.png]]
