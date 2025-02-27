# GDB Tutorial

As programmers, we all make errors. Certainly, most of us at least have tried placing "printf" statements in our code hoping to catch the errors, however, we need to know more than that. Debugger is a good tool for tracing bugs. In this tutorial, we will show you how to use gdb -- a "GNU" debugger. 

### Compiling programs to run with gdb:

Below is a not-so-well written program (crash.c) which reads a number n from standard input, calculates the sum from 1 to n and prints out the result:

```C
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

char *buf;

int sum_to_n(int num)
{
    int i, sum = 0;
    for (i = 1; i <= num; i++)
        sum += i;
    return sum;
}

void printSum()
{
    char line[10];
    printf("enter a number:\n");
    fgets(line, 10, stdin);
    if (line != NULL)
        strtok(line, "\n");
    sprintf(buf, "sum=%d", sum_to_n(atoi(line)));
    printf("%s\n", buf);
}

int main(void)
{
    printSum();
    return 0;
}
```

In order to run *crash.c* with gdb, we must compile it with the -g option which tells the compiler to embed debugging information for the debugger to use. So, we compile *crash.c* as follows:

`gcc -g -o crash crash.c`

Now, let's run the program.

```bash
./crash
enter a number:
10
Segmentation fault
```

Looks familiar? The infamous "Segmentation fault" means there is some kind of invalid memory access. Unfortunately, that is all the compiler tells us. Now, let's see how we can use GDB to spot the problem(s).
