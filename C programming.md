### books
[Head first C](file:///C:/Users/Willem/OneDrive/Documents/Textbooks%20&%20User%20Manuals/Programming%20non-embedded%20&%20networking/C/Head%20First%20C%20-%20David%20Griffiths,%20Dawn%20Griffiths%20(2012,%20O'Reilly%20Media).pdf)
[Beginning C](file:///C:/Users/Willem/OneDrive/Documents/Textbooks%20&%20User%20Manuals/Springer/Electronics%20&%20Embedded/C/Beginning%20C%20(674p).pdf): C11, GNU, 2013
[Programming for engineers](file:///C:/Users/Willem/OneDrive/Documents/Textbooks%20&%20User%20Manuals/Springer/Programming%20for%20Engineers.pdf): stack, heap, memory
[Programming Embedded Systems With C and GNU Development Tools](file:///C:/Users/Willem/OneDrive/Documents/Textbooks%20&%20User%20Manuals/Electrical%20&%20Computer/Programming%20Embedded%20Systems%20With%20C%20and%20GNU%20Development%20Tools,%202nd%20Edition%20-%20Michael%20Barr,%20Anthony%20Massa.pdf)
[Modern C, 2nd edition (2019)](file:///C:/Users/Willem/OneDrive/Documents/Textbooks%20&%20User%20Manuals/Programming%20non-embedded%20&%20networking/C/Modern%20C%202nd%20edition.pdf)
[Effective C, An Introduction to Professional C Programming (2020)](file:///C:/Users/Willem/OneDrive/Documents/Textbooks%20&%20User%20Manuals/Programming%20non-embedded%20&%20networking/C/Effective%20C%20An%20Introduction%20to%20Professional%20C%20Programming%20-%20Robert%20C.%20Seacord.pdf)


## To learn
- [x] VS Code tasks to debug and build → launch.json, tasks.json?
- [ ] 

## Head first C
Current page: 48

```bash
gcc hello_world.c -o hello_world -std=gnu11
./hello_world

gcc cards.c -o cards -std=gnu11 -Wall -Wextra -ggdb && ./cards
```
`-o file` Place the primary output in file *file*.

The *stdio* library contains code that allows you to read and write data from and to the terminal.

Return type of main() is `int` → 0 means success. 

Compilation can involve up to four stages: **preprocessing**, **compilation proper**, **assembly** and **linking**, always in that order. GCC is capable of preprocessing and compiling several files either into several assembler input files, or into one assembler input file; then each assembler input file produces an object file, and linking combines all the object files (those newly compiled, and those specified as input) into an executable file. [source](https://gcc.gnu.org/onlinedocs/gcc/Overall-Options.html#Overall-Options)

### main()
- Start of program.
- Return type: `int` → 0 means success.

### switch()
- Can replace a sequence of `if` statements.
- Will continue to run until `break` or end of switch statement.
- Check for correct breaks.

### scanf()
`%[width]s` matches a sequence of non-whitespace characters (a string).
If `width` specifier is used, matches up to width or until the first whitespace character, whichever appears first. **Always stores a null character in addition to the characters matched (so the argument array must have room for at least width+1 characters**). [scanf, fscanf, sscanf, scanf_s, fscanf_s, sscanf_s - cppreference.com](https://en.cppreference.com/w/c/io/fscanf)

### atoi()
Part of stdlib.h
Interprets an integer value in a byte string pointed to by `str`.
Integer value corresponding to the contents of `str` on success.
If no conversion can be performed, `0` is returned.
The name stands for "ASCII to integer".

## Declaration & initialization
```c
int var=value;
int var1, var2, var3;
var1 = var2 = 7;
```
Use 'unsigned'. Default is signed.

## Functions
A function declaration tells the compiler about a function's name, return type, and parameters. A function definition provides the actual body of the function.

## Pointers


## GCC options
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

## Memory
Regions: static data, stack (automatic), heap (programmer controlled).
### Static data
- Lifetime: entire program duration
- Size: fixed, known at compile time
- ex: global variables

#### Global or `static` variables
- Global are always `static`
- Have one copy
- Declaring variable in function as `static` → won't be destroyed after function returns

### Stack (automatic)
- Lifetime: temporary, stores local variables during function calls
- Size: grows when calling nested functions
- Grows high to low address
- 'normal' variables → get destroyed after function returns
- variables get allocated and destroyed automatically
- Faster than heap
- Less control
- LIFO

### Heap (dynamic)
- Lifetime: discretion of programmer
- Size: discretion of programmer
- `malloc()` and `free()`

## Headers, libraries and linking

For functions in external .c file: header file can be thought of as interface between source code and the programmer.

.h file contains function declarations or definitions to be used in main program. A .c file can contain the rest of the function definitions of only declarations are given in .h

Never put anything other than function prototypes/declarations, variable declarations, includes and macros inside a header file.

Use compiler option `-Idir` to link to directory not in current.

# Images

![[C-variables.png|600]]
![[C-operators.png|600]]
