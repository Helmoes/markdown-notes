# To learn
- [x] VS Code tasks to debug and build → launch.json, tasks.json?
- [ ] -> operator pointer to struct member how to use?
- [ ] Pre-processor macros

# Head first C
Current page: 217 

```bash
gcc hello_world.c -o hello_world -std=gnu11
./hello_world

gcc cards.c -o cards -std=gnu11 -Wall -Wextra -ggdb && ./cards
```
`-o file` Place the primary output in file *file*.

The `stdio.h` library contains code that allows you to read and write data from and to the terminal.

Return type of main() is `int` → 0 means success. 

Compilation can involve up to four stages: **preprocessing**, **compilation proper**, **assembly** and **linking**, always in that order. GCC is capable of preprocessing and compiling several files either into several assembler input files, or into one assembler input file; then each assembler input file produces an object file, and linking combines all the object files (those newly compiled, and those specified as input) into an executable file. [source](https://gcc.gnu.org/onlinedocs/gcc/Overall-Options.html#Overall-Options)

# main()
- Start of program.
- Return type: `int` → 0 means success.

To use cli arguments and options main is declared like this: (p. 141)
```c
int main(int argc, char *argv[])
{
    // Check for number of arguments
    if (argc != 6)
    {
        fprintf(stderr, "You need to give 5 arguments\n");
        return 1;
    }

    // Use arv[] as strings
    FILE *file1 = fopen(argv[2], "w");
}
```
The main function reads the cli arguments as an array of strings(character pointers to strings technically).
**`argv[0]` is name of program -> first cli argument is `argv[1].`**

![[Pasted image 20221009134924.png|850]]

## Using library for cli options
The “:” means that the e option needs an argument. If an option character is followed by two colons (‘::’), its argument is optional; this is a GNU extension.

Key points:
-   Normally, `getopt` is called in a loop. When `getopt` returns `-1` or `EOF`, indicating no more options are present, the loop terminates.
-   A `switch` statement is used to dispatch on the return value from `getopt`. In typical use, each case just sets a variable that is used later in the program.
-   A second loop is used to process the remaining non-option arguments. 

```ad-code
```c
#include <unistd.h>

int engine_count;
char ch;

while ((ch = getopt(argc, argv, "ae:")) != EOF)
{
    switch (ch)
    {
    case 'e':
        engine_count = optarg;
    }
}

argc -= optind;
argv += optind;
```

```ad-code
title: [Example of Getopt (The GNU C Library)](https://www.gnu.org/software/libc/manual/html_node/Example-of-Getopt.html)
```c
#include <ctype.h>
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main(int argc, char **argv)
{
    int aflag = 0;
    int bflag = 0;
    char *cvalue = NULL;
    int index;
    int c;

    opterr = 0;

    while ((c = getopt(argc, argv, "abc:")) != -1)
        switch (c)
        {
        case 'a':
            aflag = 1;
            break;
        case 'b':
            bflag = 1;
            break;
        case 'c':
            cvalue = optarg;
            break;
        case '?':
            if (optopt == 'c')
                fprintf(stderr, "Option -%c requires an argument.\n", optopt);
            else if (isprint(optopt))
                fprintf(stderr, "Unknown option `-%c'.\n", optopt);
            else
                fprintf(stderr,
                        "Unknown option character `\\x%x'.\n",
                        optopt);
            return 1;
        default:
            abort();
        }

    printf("aflag = %d, bflag = %d, cvalue = %s\n",
           aflag, bflag, cvalue);

    for (index = optind; index < argc; index++)
        printf("Non-option argument %s\n", argv[index]);
    return 0;
    // argv[0] will point to first cli argument that follows options
    argc -= optind;
    argv += optind;
}
```


# Declaration & initialization of variables
```c
int var=value;
int var1, var2, var3;
var1 = var2 = 7;
```
Use 'unsigned'. Default is signed.
You can force an integer constant to be of a long and/or unsigned integer type by appending a sequence of one or more letters to the end of the constant:
- `U`: unsigned
- `L`: long
Example: `45UL`, `0x3UL`

## Casting
```c
int x = 7;
int y = 2;
float z = (float)x / (float)y;
// same:
float z = (float)x / y;
```

## Limits of int & float
```c
#include <limits.h>
INT_MAX
INT_MIN

#include <float.h>
FLT_MAX
FLT_MIN
```

# Functions
A function declaration tells the compiler about a function's name, return type, and parameters. A function definition provides the actual body of the function.
## Specific functions
### switch()
- Can replace a sequence of `if` statements.
- Will continue to run until `break` or end of switch statement.
- Check for correct breaks.
```c
switch (expression)
{
case /* constant-expression */:
    /* code */
    break;

default:
    break;
}
```

### atoi()
Part of stdlib.h
Interprets an integer value in a byte string pointed to by `str`.
Integer value corresponding to the contents of `str` on success.
If no conversion can be performed, `0` is returned.
The name stands for "ASCII to integer".

## Function declaration
-> at beginning of source file or in separate header file.


# Pointers
To get address of variable use `&`.

Create a pointer variable:
```c
int *p_address_of_x = &x;
```

Read address contents:
```c
int value_stored = *p_address_of_x;
```

`*` operator is said to dereference a pointer. **It reads and can be used to set the contents of a memory address**.

Change contents of address:
```c
*p_address_of_x = 99;
```

Template:
```c
void function(int *p_var1, int *p_var2)
{
    *p_var1 = ... + *p_var2;
}

int main()
{
    int var1;
    int var2;
    function(&var1, &var2);
}
```

## Arrays
Array variable is pointer to lowest memory address of array.
Using & on the array var will result in the array itself.

Member access through pointer to a struct or union:
```c
#include <stdio.h>
struct s {int x;};
int main(void)
{
    struct s s={1}, *p = &s;
    p->x = 7; // changes the value of s.x through the pointer
    printf("%d\n", p->x); // prints 7
}
```

## Little endian
![[Pasted image 20220914202910.png|325]]
![[Pasted image 20220914202853.png|325]]
## restrict
- Type qualifier used in pointer declarations.
- Hints to the compiler that for the lifetime of the pointer, no other pointer will be used to access the object to which it points.
- a way for programmer to inform about an optimization that compiler can make.

# Structures
Custom data type made up of other data types. Kind of like a template of how we want the new data type to look.
- fixed length
- when you’re assigning struct variables, you are telling the computer to copy data.
- structs are nestable
```c
struct new_struct
{
    const char *name;  // will store a pointer to the string literal.
    char nickname[20]; // will store the whole string/char array in the struct.
    int height;
    int age;
};
// declare struct:
struct new_struct new_struct_instance = {"George", 180, 20};
// access struct with dot operator:
new_struct_instance.name;
new_struct_instance.height = ...;
other_struct.new_struct.height: ...; // with nested structs multiple dot access operators
```

## typedef structs
- To not always have to include the `struct` keyword
```c
typedef struct new_struct // we can actually skip the struct name, 'new_struct'. This is called an anonymous struct.
{
    ...
}new_struct_alias;
```
## structs in functions with pointers
- To pass a struct to a function we need to use pointers
```c
typedef struct
{
    ...
}new_struct_alias;

void function_name(new_struct_alias *s)
{
    (*s).height = ...; // (*s) is needed. Wrong: *s.height or *(s.height)
}

function_name(&struct_var);
```
To avoid `(*s)` we can use the `->` notation. `(*s).height` is the same as `s->height`.



# GCC options
Put GCC compile command as comment in first line
```bash
// gcc -std=c99 -o go go.c neuron.c -lm -Wall -Werror
// gcc -g -Wall -o add add.c -lm
gcc ${fileBasename}.c -fdiagnostics-color=always -ggdb -std=gnu17 -Wall -Wextra -Werror -o ./bin/${fileBasenameNoExtension}
```

Options:
- `-g` or `-ggdb`: provide debugging info in executable
- `-c`: Compile or assemble, but don't link. Output is object file `.o`
- `-o file`: Place the primary output in file file. This applies to whatever sort of output is being produced, whether it be an executable file, an object file, an assembler file or preprocessed C code.
- 

# Strings
Strings are arrays of chars. The array variable is a pointer to the first element in the array, not the contents of the array/string itself!
`char *s = "some string";` this is not modifiable (string literal).

## scanf() p.65
`%[width]s` matches a sequence of non-whitespace characters (a string).
If `width` specifier is used, matches up to width or until the first whitespace character, whichever appears first. **Always stores a null character in addition to the characters matched (so the argument array must have room for at least width+1 characters**). [scanf, fscanf, sscanf, scanf_s, fscanf_s, sscanf_s - cppreference.com](https://en.cppreference.com/w/c/io/fscanf)

scanf needs pointers to char array or variables.
```c
int age;
scanf("%i", &age);
```

**Return value:** Number of receiving arguments successfully assigned (which may be zero in case a matching failure occurred before the first receiving argument was assigned), or [EOF](https://en.cppreference.com/w/c/io "c/io") if input failure occurs before the first receiving argument was assigned.

# Files
p. 138

We can create our own data streams. Each data stream is represented by a pointer to a file, and you can create a new data stream using the fopen() function:
```c
FILE *in_file = fopen("input.txt", "r");
FILE *out_file = fopen("output.txt", "w");
```

The fopen() function takes two parameters: a filename and a mode. The mode can be **w** to write to a file, **r** to read from a file, or **a** to append data to the end of a file.
Once you’ve created a data stream, you can print to it using fprintf(). Or read from it with fscanf().

```c
fprintf(out_file, "Don't wear %s with %s", "red", "green");
fscanf(in_file, "%79[^\n]\n", sentence);
```

When finished the data stream needs to be closed.
```c
fclose(in_file);
fclose(out_file);
```

Error checking on opening file:
```c
FILE *in;
if (!(in = fopen("dont_exist.txt", "r")))
{
    fprintf(stderr, "Can't open the file.\n");
    return 1;
}
```

## Data streams
Amount of data streams we can use depends on OS, but usually up to 256.


# Standard input/output/error
Scanf() and printf() use std in and out. The Standard Input and Standard Output are created by the operating system when the program runs.
The program receives data through the Standard Input, The program outputs data through the Standard Output.

The operating system controls how data gets into and out of the Standard Input and Output. If you run a program from the command prompt or terminal, the operating system will send all of the keystrokes from the keyboard into the Standard Input. If the operating system reads any data from the Standard Output, by default it will send that data to the display. 

The scanf() and printf() functions don’t know, or care, where the data comes from or goes to. They just read and write Standard Input and the Standard Output.

**You can redirect the Standard Input and Standard Output so that they read (<) and write (>) data somewhere else, such as to and from files. Use >> to append and not overwrite.** [Redirections (Bash Reference Manual)](https://www.gnu.org/software/bash/manual/html_node/Redirections.html)
```bash
./ex_p105 < gpsdata.csv > output.json
```

Redirect stderr
```bash
./ex_p105 >2 output.json
```

Redirect stdout and stderror:
```bash
&>word # or &>>word
# or
>word 2>&1
# Of the two forms, the first is preferred. This is semantically equivalent
```

In c code using `fprintf()`:
```c
fprintf(stderr, "%s\n", word);
```

See exit status of last command:
```bash
echo $?
```

## Connecting stdin & stdout with pipes |
```bash
(./bermuda | ./geo2json) < spooky.csv > output.json
```


# Memory
Regions: static data, stack (automatic), heap (programmer controlled).
## Static data
- Lifetime: entire program duration
- Size: fixed, known at compile time
- ex: global variables

### Global or `static` variables
- Global are always `static`
- Have one copy
- Declaring variable in function as `static` → won't be destroyed after function returns

## Stack (automatic)
- Lifetime: temporary, stores local variables during function calls
- Size: grows when calling nested functions
- Grows high to low address
- 'normal' variables → get destroyed after function returns
- variables get allocated and destroyed automatically
- Faster than heap
- Less control
- LIFO

## Heap (dynamic)
- Lifetime: discretion of programmer
- Size: discretion of programmer
- `malloc()` and `free()`

# Headers, libraries and linking

For functions in external .c file: header file can be thought of as interface between source code and the programmer.
.h file contains function declarations or definitions to be used in main program. A .c file can contain the rest of the function definitions of only declarations are given in .h
Never put anything other than function prototypes/declarations, variable declarations, includes and macros inside a header file.
Use compiler option `-Idir` to link to directory not in current.

1. Compile source into object files using `-c` option

# The C Preprocessor
- Use `#define` for constants.
- When using more complex constants that need to be evaluated: use `const` instead.
```c
const unsigned int SIDE = 10 + 2;
```
- Use \\ to extend macro over several lines.
## Parameterized Macros
- Parameterized macros allow us to give arguments to macros.
- Use inline functions instead of parameterized macros whenever possible. Because inline functions are part of the C language, the compiler can make sure they’re being used correctly.
```c
#define DOUBLE(x) (2 * (x))
```
## Conditional compilation
If `DEBUG` is defined, calls to debug will be replaced with calls to printf; otherwise, they’ll be replaced by blank space.
```c
#ifdef DEBUG
#define debug(msg) printf(msg)
#else // DEBUG
#define debug(msg) /* nothing */
#endif // DEBUG

int main()
{
    debug("Debug version\n");
    debug("Starting main loop\n");
 
    while (1) {
        debug("Before process file \n");
        processFile();
        debug("After process file \n");
```

# Makefiles
[GNU make](https://www.gnu.org/software/make/manual/make.html)
Running `make` without argument starts the target `all` in the `makefile`. 
A makefile consists of a set of rules. A rule consists of 3 parts: 
- a target
- a list of pre-requisites
- and a command
```makefile
target: pre-req-1 pre-req-2 ...
	command
```
- Makefiles use TABs, NOT spaces!
- The _target_ and _pre-requisites_ are separated by a colon (`:`).
- The rules are usually organized in such as way the more general rules come first. 
- The overall rule is often name "`all`", which is the default target for `make`.
- A target that does not represent a file is called a phony target.
- Phony target is always out-of-date and its command will be run. The standard phony targets are: `all`, `clean`, `install`.
- A variable begins with a `$` and is enclosed within parentheses `(...)` or braces `{...}`.

Automatic variables are set by make after a rule is matched:
- `$@`: the target filename.
- `$*`: the target filename without the file extension.
- `$<`: the first prerequisite filename.
- `$^`: the filenames of all the prerequisites, separated by spaces, discard duplicates.
- `$+`: similar to `$^`, but includes duplicates.
- `$?`: the names of all prerequisites that are newer than the target, separated by spaces.

You can use `VPATH` (uppercase) to specify the directory to search for dependencies and target files. For example,
```makefile
# Search for dependencies and targets from "src" and "include" directories
# The directories are separated by space
VPATH = src include
```
You can also use `vpath` (lowercase) to be more precise about the file type and its search directory. For example,
```makefile
# Search for .c files in "src" directory; .h files in "include" directory
# The pattern matching character '%' matches filename without the extension
vpath %.c src
vpath %.h include
```

A pattern rule, which uses pattern matching character `'%'` as the filename, can be applied to create a target, if there is no explicit rule.
```makefile
%.o: %.c
	$(COMPILE.c) $(OUTPUT_OPTION) $<

%: %.o
$(LINK.o) $^ $(LOADLIBES) $(LDLIBS) -o $@
```

# Unit testing
Options:
- Unity
- [cmocka - unit testing framework for C](https://cmocka.org/)
- [AceUnit](https://aceunit.sourceforge.net/): used by headfirst c
- [Check | Unit testing framework for C](https://libcheck.github.io/check/)
- [µnit — C Unit Testing Framework](https://nemequ.github.io/munit/)
- [CUnit Home](https://cunit.sourceforge.net/)
- [CuTest: The Cutest C Unit Testing Framework](https://cutest.sourceforge.net/)
- 

# Images

![[C-variables.png|600]]
![[C-operators.png|600]]
