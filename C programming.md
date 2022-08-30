### books
[Head first C](file:///C:/Users/Willem/OneDrive/Documents/Textbooks%20&%20User%20Manuals/Programming%20non-embedded%20&%20networking/C/Head%20First%20C%20-%20David%20Griffiths,%20Dawn%20Griffiths%20(2012,%20O'Reilly%20Media).pdf)
[Beginning C](file:///C:/Users/Willem/OneDrive/Documents/Textbooks%20&%20User%20Manuals/Springer/Electronics%20&%20Embedded/C/Beginning%20C%20(674p).pdf): C11, GNU
[Programming for engineers](file:///C:/Users/Willem/OneDrive/Documents/Textbooks%20&%20User%20Manuals/Springer/Programming%20for%20Engineers.pdf): stack, heap, memory
[Programming Embedded Systems With C and GNU Development Tools](file:///C:/Users/Willem/OneDrive/Documents/Textbooks%20&%20User%20Manuals/Electrical%20&%20Computer/Programming%20Embedded%20Systems%20With%20C%20and%20GNU%20Development%20Tools,%202nd%20Edition%20-%20Michael%20Barr,%20Anthony%20Massa.pdf)

## Head first C
Current page: 8

```bash
gcc hello_world.c -o hello_world -std=gnu11
./hello_world

gcc cards.c -o cards -std=gnu11 && ./cards
```
`-o file` Place the primary output in file *file*.

The *stdio* library contains code that allows you to read and write data from and to the terminal.

Return type of main() is `int` → 0 means success. 

Compilation can involve up to four stages: **preprocessing**, **compilation proper**, **assembly** and **linking**, always in that order. GCC is capable of preprocessing and compiling several files either into several assembler input files, or into one assembler input file; then each assembler input file produces an object file, and linking combines all the object files (those newly compiled, and those specified as input) into an executable file. [source](https://gcc.gnu.org/onlinedocs/gcc/Overall-Options.html#Overall-Options)

### main()
- Start of program.
- Return type: `int` → 0 means success.

### scanf()
`%[width]s`      matches a sequence of non-whitespace characters (a string).
If `width` specifier is used, matches up to width or until the first whitespace character, whichever appears first. **Always stores a null character in addition to the characters matched (so the argument array must have room for at least width+1 characters**). [scanf, fscanf, sscanf, scanf_s, fscanf_s, sscanf_s - cppreference.com](https://en.cppreference.com/w/c/io/fscanf)

### atoi()
Interprets an integer value in a byte string pointed to by `str`.
Integer value corresponding to the contents of `str` on success.
If no conversion can be performed, `0` is returned.
The name stands for "ASCII to integer".

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
