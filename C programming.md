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
# Head first C

```bash
gcc main.c -o main
./main
```