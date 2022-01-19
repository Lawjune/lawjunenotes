
#001 - Hello World

```c
#include <stdio.h>

int main(int argc, char *argv[]) 
{
    printf("Hello World\n");

    return 0;
}
```

#002 - Data Types: "int" and "char"

```c
#include <stdio.h>

int main(int argc, char *argv[]) 
{   

    int k;
    int zznum;
    int sumnum;

    char mychar;

    printf("Hello World\n");

    k = 24;
    printf("Value of k = %d\n", k);

    zznum = 4;
    printf("Value of zznum = %d\n", zznum);
    printf("Values of two vars are: %d and %d\n", k, zznum);

    sumnum = k + zznum;
    printf("Values of sum = %d\n", sumnum);

    mychar = 'c';
    printf("mychar is %c\n", mychar);
    printf("mychar ASCII code is %d\n", mychar);

    return 0;
}
```
```output
Hello World
Value of k = 24
Value of zznum = 4
Values of two vars are: 24 and 4
Values of sum = 28
mychar is c
mychar ASCII code is 99
```

#003 - Data Types: "float", "double", and "long int"

```c
#include <stdio.h>

int main(int argc, char *argv[]) 
{   

    int my_int;
    char my_char;
    float my_num;

    long int my_long_int;
    double my_double, my_sum_db;

    my_num = 24.3;
    printf("24.3 - my_num = %f\n", my_num);

    my_num = 24.4;
    printf("24.4 - my_num = %f\n", my_num);

    printf("Size of int = %d\n", sizeof(int));
    printf("Size of int = %d\n", sizeof(my_int));

    printf("Size of char = %d\n", sizeof(char));
    printf("Size of char = %d\n", sizeof(my_char));

    printf("Size of float = %d\n", sizeof(float));
    printf("Size of float = %d\n", sizeof(my_num));

    printf("Size of long int  = %d\n", sizeof(long int ));
    printf("Size of long int  = %d\n", sizeof(my_long_int));

    printf("Size of double = %d\n", sizeof(double));
    printf("Size of double = %d\n", sizeof(my_double));

    my_double = 243.25;
    my_sum_db = 3.5 + my_double;
    printf("Value of my_sum_db = %f\n", my_sum_db);

    my_int = 3;
    my_sum_db = 3.2 + my_int;
    printf("Value of my_sum_db = %f\n", my_sum_db);

    my_sum_db = 22.4 + 4.0;
    printf("Value of my_sum_db = %f\n", my_sum_db);

    return 0;
}
```
```output
24.3 - my_num = 24.299999
24.4 - my_num = 24.400000
Size of int = 4
Size of int = 4
Size of char = 1
Size of char = 1
Size of float = 4
Size of float = 4
Size of long int  = 8
Size of long int  = 8
Size of double = 8
Size of double = 8
Value of my_sum_db = 246.750000
Value of my_sum_db = 6.200000
Value of my_sum_db = 26.400000
```

#004 - Data Types: strings

```c
#include <stdio.h>

int main(int argc, char *argv[]) 
{   

    char message[13] = "Hello World!";

    printf("Message is %s\n", message);

    printf("array 2 is message %c\n", message[1]);

    return 0;
}
```
```output
Message is Hello World!
Array 2 is message e
```

#005 - Data Types: pointer

```c
#include <stdio.h>

int main(int argc, char *argv[]) 
{   
    int n;
    int *k;

    n = 25;
    k = &n;

    printf("&n = %x\n", &n);
    printf("n = %d\n", n);
    printf("k = %x\n", k);
    printf("*k = %d\n", *k);

    *k = 10;
    printf("n = %d\n", n);
    printf("k = %x\n", k);
    printf("*k = %d\n", *k);
    
    return 0;
}
```
```output
&n = 2af6393c
n = 25
k = 2af6393c
*k = 25
n = 10
k = 2af6393c
*k = 10
```

***An integer***
```c
int a;
```

***A pointer to an integer***
```c
int *a;
```

***A pointer to a pointer to an integer***
```c
int **a;
```

***An array of 10 integers***
```c
int a[10];
```

***An array of 10 pointers to integers***
```c
int *a[10]
```

***A pointer to an array of 10 integers***
```c
int (*a)[10]
```

***A pointer to a function that takes an integer as an argument and returns an integer***
```c
int (*a)(int a)
```

***An array of ten pointers to functions that take an integer argument and return an integer***
```c
int (*a[10])(int)
```



#006 - Data Types: Array

```c
#include <stdio.h>

int main(int argc, char *argv[]) 
{   
    int a[4];

    a[0]  = 3;
    a[1] = 2;
    a[2] = 7;
    a[3] = 10;

    int length;
    length = sizeof(a) / sizeof(int);


    for(int i=0; i<length; i++) {
        printf("a[%d] = %d\n", i, a[i]);
    }

    return 0;
}
```
```output
a[0] = 3
a[1] = 2
a[2] = 7
a[3] = 10
```

#007 - If-Then-Else Statement

#008 - For Loop Statement

#009 - "while" Loop

#010 - "struct" Statement

```c
#include <stdio.h>

int main(int argc, char *argv[]) 
{   

    struct 
    {
        int a;
        float b;
        int c; 
    } myst;

    myst.a = 4;
    myst.b = 3.37;
    myst.c = 1;
    
    printf("a = %d, b = %f, c = %d/n", myst.a, myst.b, myst.c);

    return 0;
}
```
```output
a = 4, b = 3.370000, c = 1/n
```

#011 - typedef Statement

```c
#include <stdio.h>

typedef int INT32;
typedef char MYCHR;

typedef struct mystruct_t
{
    int a;
    int b;
} MYSTRUCTX;


int main(int argc, char *argv[]) 
{   

    INT32 i;
    MYCHR mystr[20] = "Hello World!";

    MYSTRUCTX my_struct;
    my_struct.a = 2;
    my_struct.b = 4;

    printf("i = %d\n", i);
    printf("mystr = %s\n", mystr);

    printf("my_struct.a = %d\n", my_struct.a);
    printf("my_struct.b = %d\n", my_struct.b);

    return 0;
}
```
```output
i = 0
mystr = Hello World!
my_struct.a = 2
my_struct.b = 4
```

#012 - Functions

#013 - Function Pointers

```c
#include <stdio.h>

int add(int a, int b)
{
    int sum;
    sum = a + b;
    return sum;
}

int main(int argc, char *argv[]) 
{       
    int result, prt_result;
    int (*add_ptr)(int, int);
    add_ptr = &add;
    result = add(3, 7);
    prt_result = add_ptr(3, 7); 
    printf("result = %d\n", result);
    printf("prt_result = %d\n", result);
    return 0;
}
```
```output
result = 10
prt_result = 10
```

#014 - Adding Comments in Source Code

#015 - argc argv

**gcc -o helloc helloc.c**

```c
#include <stdio.h>

int main(int argc, char *argv[]) 
{       
    printf("argc = %d\n", argc);
    return 0;
}
```
```sh
./helloworld
`=>
argc = 1
```
```sh
./helloworld one
`=>
argc = 2
```
```sh
./helloworld one anyinput
`=>
argc = 3
```

```c
#include <stdio.h>

int main(int argc, char *argv[]) 
{        
    
    printf("argc = %d\n", argc);

    for(int i = 0; i < argc; i++)
    {
        printf("argv[%d] = %s\n", i, argv[i]);
    }
    return 0;
}
```
```sh
./helloworld
`=>
argc = 1
argv[0] = /home/lawjune/Documents/cppLinux/projects/helloworld/helloworld
```
```sh
./helloworld one
`=>
argc = 2
argv[0] = ./helloworld
argv[1] = one
```
```sh
./helloworld one anyinput
`=>
argc = 3
argv[0] = ./helloworld
argv[1] = one
argv[2] = anyinput
```

#016 - Multiple Source Files

*addnums.c*
```c
#include<stdio.h>

int addnumbers(int a, int b)
{
    int sum;
    sum = a + b;
    return sum;
}
```

*helloworld.c*
```c
#include <stdio.h>

int main(int argc, char *argv[]) 
{   
    int total;
    total = addnumbers(2, 4);
    printf("total = %d\n", total);     
    return 0;
}
```

```sh
gcc -c helloworld.c
gcc -c addnum.c
ls
`=>
addnum.c  addnum.o   helloworld.c  helloworld.o
```
```sh
gcc -o helloworld helloworld.o addnum.o
./helloworld
`=> 
total = 6
```

```c
#include <stdio.h>

int addnumbers(int a, int b);

int main(int argc, char *argv[]) 
{   
    int total;
    total = addnumbers(2, 4);
    printf("total = %d\n", total);     
    return 0;
}
```

```sh
gcc -o helloworld helloworld.c addnum.c
```

*addnums.h*
```c
int addnumbers(int a, int b);
```

*addnums.c*
```c
#include <stdio.h>
#include "addnum.h"

int addnumbers(int a, int b)
{
    int sum;
    sum = a + b;
    return sum;
}
```

```c
#include <stdio.h>
#include "addnum.h"

int main(int argc, char *argv[]) 
{   
    int total;
    total = addnumbers(2, 4);
    printf("total = %d\n", total);     
    return 0;
}
```

```sh
gcc -o helloworld helloworld.c addnum.c
```

#017 - String Functions and Operations

```c
#include <stdio.h>
#include <string.h>

int main(int argc, char *argv[]) 
{   
    char str[24];
    char str2[24];
    int i;
    int n;

    sprintf(str, "Hello World!");
    printf("%s\n", str);

    i = 4;
    sprintf(str, "Value of i = %d", i);
    printf("%s\n", str);

    n = strlen(str);
    printf("Length of str is %d\n", n);

    strcpy(str2, str);
    printf("str2 is %s\n", str2);

    memset(str, 0, 24);
    printf("New str is %s\n", str);

    memset(str, 'a', 10);
    printf("New str is %s\n", str);

    return 0;
}
```
```output
Hello World!
Value of i = 4
Length of str is 14
str2 is Value of i = 4
New str is 
New str is aaaaaaaaaa
```

#018 - Char Pointer vs Array Char

```c
#include <stdio.h>
#include <string.h>

int main(int argc, char *argv[]) 
{   
    char str[24] = "First string";
    char *ptr = "Second string";

    printf("str = %s\n", str);
    printf("ptr = %s\n", ptr);

    printf("&ptr = %x\n", &ptr);
    printf("The pointed array address: *(&ptr) = %x\n", *(&ptr));
    printf("ptr moving forward 1 step.\n");
    ptr = ptr + 1;  // We can't manipulate str[24] address directly
    printf("ptr = %s\n", ptr);
    printf("&ptr = %x\n", &ptr);
    printf("The pointed array address: *(&ptr) = %x\n", *(&ptr));
    printf("ptr moving forward 1 one more step.\n");
    ptr = ptr + 1; 
    printf("ptr = %s\n", ptr);
    printf("&ptr = %x\n", &ptr);
    printf("The pointed array address: *(&ptr) = %x\n", *(&ptr));

    printf("Length of ptr is %d\n", strlen(ptr));
    strcpy(str, ptr);
    printf("New str is %s\n", str);

    ptr = ptr - 2;
    printf("Recoved ptr: %s\n", ptr);

    memset(&ptr, 0, strlen(ptr));
    printf("Reset ptr: %s\n", ptr);

    return 0;
}
```
```output
str = First string
ptr = Second string
&ptr = aa4ef218
The pointed array address: *(&ptr) = eb835008
ptr moving forward 1 step.
ptr = econd string
&ptr = aa4ef218
The pointed array address: *(&ptr) = eb835009
ptr moving forward 1 one more step.
ptr = cond string
&ptr = aa4ef218
The pointed array address: *(&ptr) = eb83500a
Length of ptr is 11
New str is cond string
Recoved ptr: Second string
Reset ptr: (null)
```

*The 'S' missing will becomde the garbage!!!*

str -> 0x08ffff -> 'F'
    -> 0x090000 -> 'i'
    ......
    -> 0x09000B -> 'g'
    -> 0x09000C -> unkonwn char

ptr -> 0x0cffef -> 0x0d0001
    
    -> 0x0d0001 -> 'S'
    -> 0x0d0002 -> 'e'
    ......
    -> 0x0d000E -> 'g'


#019 - Preprocessor

```sh
gcc -E -c helloworld.c
`=>
# 1 "helloworld.c"
# 1 "<built-in>"
# 1 "<command-line>"
# 31 "<command-line>"
# 1 "/usr/include/stdc-predef.h" 1 3 4
# 32 "<command-line>" 2
# 1 "helloworld.c"
# 1 "/usr/include/stdio.h" 1 3 4
# 27 "/usr/include/stdio.h" 3 4
# 1 "/usr/include/x86_64-linux-gnu/bits/libc-header-start.h" 1 3 4
# 33 "/usr/include/x86_64-linux-gnu/bits/libc-header-start.h" 3 4
# 1 "/usr/include/features.h" 1 3 4
# 461 "/usr/include/features.h" 3 4
# 1 "/usr/include/x86_64-linux-gnu/sys/cdefs.h" 1 3 4
# 449 "/usr/include/x86_64-linux-gnu/sys/cdefs.h" 3 4
# 1 "/usr/include/x86_64-linux-gnu/bits/wordsize.h" 1 3 4
# 450 "/usr/include/x86_64-linux-gnu/sys/cdefs.h" 2 3 4
# 1 "/usr/include/x86_64-linux-gnu/bits/long-double.h" 1 3 4
# 451 "/usr/include/x86_64-linux-gnu/sys/cdefs.h" 2 3 4
# 462 "/usr/include/features.h" 2 3 4
# 485 "/usr/include/features.h" 3 4
# 1 "/usr/include/x86_64-linux-gnu/gnu/stubs.h" 1 3 4
# 10 "/usr/include/x86_64-linux-gnu/gnu/stubs.h" 3 4
# 1 "/usr/include/x86_64-linux-gnu/gnu/stubs-64.h" 1 3 4
# 11 "/usr/include/x86_64-linux-gnu/gnu/stubs.h" 2 3 4
# 486 "/usr/include/features.h" 2 3 4
# 34 "/usr/include/x86_64-linux-gnu/bits/libc-header-start.h" 2 3 4
# 28 "/usr/include/stdio.h" 2 3 4





# 1 "/usr/lib/gcc/x86_64-linux-gnu/9/include/stddef.h" 1 3 4
# 209 "/usr/lib/gcc/x86_64-linux-gnu/9/include/stddef.h" 3 4

# 209 "/usr/lib/gcc/x86_64-linux-gnu/9/include/stddef.h" 3 4
typedef long unsigned int size_t;
# 34 "/usr/include/stdio.h" 2 3 4


# 1 "/usr/lib/gcc/x86_64-linux-gnu/9/include/stdarg.h" 1 3 4
# 40 "/usr/lib/gcc/x86_64-linux-gnu/9/include/stdarg.h" 3 4
typedef __builtin_va_list __gnuc_va_list;
# 37 "/usr/include/stdio.h" 2 3 4

# 1 "/usr/include/x86_64-linux-gnu/bits/types.h" 1 3 4
# 27 "/usr/include/x86_64-linux-gnu/bits/types.h" 3 4
# 1 "/usr/include/x86_64-linux-gnu/bits/wordsize.h" 1 3 4
# 28 "/usr/include/x86_64-linux-gnu/bits/types.h" 2 3 4
# 1 "/usr/include/x86_64-linux-gnu/bits/timesize.h" 1 3 4
# 29 "/usr/include/x86_64-linux-gnu/bits/types.h" 2 3 4


typedef unsigned char __u_char;
typedef unsigned short int __u_short;
typedef unsigned int __u_int;
typedef unsigned long int __u_long;


typedef signed char __int8_t;
typedef unsigned char __uint8_t;
typedef signed short int __int16_t;
typedef unsigned short int __uint16_t;
typedef signed int __int32_t;
typedef unsigned int __uint32_t;

typedef signed long int __int64_t;
typedef unsigned long int __uint64_t;
```

```c
#include <stdio.h>

#define NUM1 5
#define NUM2 8

#define SUM(x, y) x+y

int main(int argc, char *argv[]) 
{   

    int i;
    int k;
    int sum;

    i = NUM1;
    k = NUM2;

    sum = SUM(i, k);

    /* This is my comment */

    return 0;
}
```
```sh
gcc -E -c helloworld.c
......
# 8 "helloworld.c"
int main(int argc, char *argv[])
{

    int i;
    int k;
    int sum;

    i = 5;
    k = 8;

    sum = i+k;



    return 0;
}
````

```c
#include <stdio.h>

#define NUM1 5
#define NUM2 8

#define SUM(x, y) x+y
#define ADD

int main(int argc, char *argv[]) 
{   

    int i;
    int k;
    int sum;

    i = NUM1;
    k = NUM2;

    sum = SUM(i, k);

    /* This is my comment */

#ifdef ADD
    sum = i + k;
#else
    sum = SUM(i, k);
#endif

    return 0;
}
```
```sh
gcc -E -c helloworld.c
......
# 9 "helloworld.c"
int main(int argc, char *argv[])
{

    int i;
    int k;
    int sum;

    i = 5;
    k = 8;

    sum = i+k;




    sum = i + k;




    return 0;
}
````

#020 - Unary and Binary Operations

```c
#include <stdio.h>


int main(int argc, char *argv[]) 
{  
    int a, b, sum;
    
    a = 4;
    a++; 
    printf("a = %d\n", a);

    a = 2;
    a += 4;
    printf("a = %d\n", a);

    a = 7;
    a--;
    printf("a = %d\n", a);

    a = 7;
    a -= 3;
    printf("a = %d\n", a);

    a = 7;
    a *= 3;
    printf("a = %d\n", a);

    a = 7;
    a /= 3;
    printf("a = %d\n", a);

    a = 7;
    printf("a = %d\n", a--);
    a = 7;
    printf("a = %d\n", --a);

    return 0;
}
```
```output
a = 5
a = 6
a = 6
a = 4
a = 21
a = 2
a = 7
a = 6
```

#021 - Type Casting

```c
#include <stdio.h>


int main(int argc, char *argv[]) 
{  
    int i;
    char c;

    char *ptr;
    char s;

    c = 'w';
    i = (int) c;
    printf("i = %d, %c\n", i, i);

    s = 'x';
    ptr = &s;
    i = (int) ptr;
    printf("i = %x\n", i);
    
    i = 3000;
    c = (char) i;
    printf("c = %d\n", c);

    return 0;
}
```
```output
i = 119, w
i = 1fab0e0a
c = -72
```

#022 - malloc() free()

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main(int argc, char *argv[]) 
{  

    char *ptr;
    ptr = (char *) malloc(24);

    if(ptr == NULL)
    {
        printf("Failed to get or allocate memory!\n");
        exit(1);
    }

    strcpy(ptr, "Hello there!");
    printf("ptr: %s\n", ptr);

    free(ptr);

    return 0;
}
```

#023 - Creating Header File

*addnum.h*
```c
#ifndef _ADDNUM__H__
#define _ADDNUM__H__

#define addnum(x, y) x+y
int addnumbers(int a, int b);

#endif
```

```c
#include <stdio.h>
#include "addnum.h"

int main(int argc, char *argv[]) 
{  
    printf("sum = %d\n", addnum(7, 6));
    printf("sum = %d\n", addnumbers(7, 6));
    return 0;
}
```
```output
sum = 13
sum = 13
```

#024 - open() read() write() Functions

```c
#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <sys/stat.h>
#include <fcntl.h>
#include <unistd.h>

int main(int argc, char *argv[]) 
{  

    int fd;
    char buf[16];

    /* write */
    fd = open("myfile.txt", O_CREAT | O_WRONLY, 0600);

    if(fd == -1) 
    {
        printf("Failed to create and open the file.\n");
        exit(1);
    }

    write(fd, "Hello World!\n", 13);

    close(fd);

    /* read */
    fd = open("myfile.txt", O_RDONLY);

    if(fd == -1) 
    {
        printf("Failed to open and read the file.\n");
        exit(1);
    }

    read(fd, buf, 13);
    buf[13] = '\0';

    close(fd);

    printf("buf: %s\n", buf);

    return 0;
}
```
```output
buf: Hello World!
```

#025 - readdir() opendir() Functions

```c
#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <dirent.h>

int main(int argc, char *argv[]) 
{  
    DIR *dir;
    struct dirent *sd;

    dir = opendir(".");

    if(dir == NULL)
    {
        printf("Error! Unable to open directory.\n");
        exit(1);
    }

    while ( (sd=readdir(dir)) != NULL)
    {
        printf(">> %s\n", sd->d_name);
    }
    

    closedir(dir);

    return 0;
}
```
```output
>> addnum.c
>> addnum.h
>> myfile.txt
>> ..
>> .
>> .vscode
>> helloworld.c
>> helloworld
```

#026 - fork() Function

```c
#include <stdio.h>
#include <unistd.h>

int main(int argc, char *argv[]) 
{   
    int childpid;
    int count1 = 0, count2 = 0;

    printf("Before it forks!\n");

    childpid = fork();

    if (childpid == 0)
    {
        printf("This is a child process\n");
        while (count1 < 10)
        {
            printf("Child process: %d\n", count1);
            sleep(1);
            count1++;
        }
        
    } else {
        printf("This is the parent process\n");
        while (count2 < 20)
        {
            printf("Parent process: %d\n", count2);
            sleep(1);
            count2++;
        }
    }

    return 0;
}
```
```output
Before it forks!
This is the parent process
Parent process: 0
This is a child process
Child process: 0
Parent process: 1
Child process: 1
Parent process: 2
Child process: 2
Parent process: 3
Child process: 3
Parent process: 4
Child process: 4
Child process: 5
Parent process: 5
Parent process: 6
Child process: 6
Child process: 7
Parent process: 7
Child process: 8
Parent process: 8
Child process: 9
Parent process: 9
Parent process: 10
Parent process: 11
Parent process: 12
Parent process: 13
Parent process: 14
Parent process: 15
Parent process: 16
Parent process: 17
Parent process: 18
Parent process: 19
```

```sh
ps -aux | grep helloworld
```

```c
#include <stdio.h>
#include <unistd.h>
#include <signal.h>

int main(int argc, char *argv[]) 
{   
    int childpid;
    int count1 = 0, count2 = 0;

    printf("Before it forks!\n");

    childpid = fork();

    if (childpid == 0)
    {
        printf("This is a child process\n");
        while (count1 < 20)
        {
            printf("Child process: %d\n", count1);
            sleep(1);
            count1++;
        }
        
    } else {
        printf("This is the parent process\n");
        while (count2 < 10)
        {
            printf("Parent process: %d\n", count2);
            sleep(1);
            count2++;
        }

        // If the parenet does not kill the child
        // The child process will keep running
        kill(childpid, SIGKILL);
    }

    return 0;
}
```
```output
Before it forks!
This is the parent process
Parent process: 0
This is a child process
Child process: 0
Parent process: 1
Child process: 1
Parent process: 2
Child process: 2
Child process: 3
Parent process: 3
Child process: 4
Parent process: 4
Parent process: 5
Child process: 5
Parent process: 6
Child process: 6
Child process: 7
Parent process: 7
Parent process: 8
Child process: 8
Parent process: 9
Child process: 9
```

https://www.geeksforgeeks.org/fork-system-call/

*Fork system call is used for creating a new process, which is called **child process**, which runs concurrently with the process that makes the fork() call (parent process). After a new child process is created, both processes will execute the next instruction following the fork() system call. **A child process uses the same pc(program counter), same CPU registers, same open files which use in the parent process.***


- ***Negative Value:** creation of a child process was unsuccessful.*
- ***Zero:** Returned to the newly created child process.*
- ***Positive value:** Returned to parent or caller. The value contains process ID of newly created child process.*

**1. Predict the Output of the following program:**

```c
#include <stdio.h>
#include <sys/types.h>
#include <unistd.h>
int main()
{
  
    // make two process which run same
    // program after this instruction
    fork();
  
    printf("Hello world!\n");
    return 0;
}
```
```output
Hello world!
Hello world!
```

**2. Calculate number of times hello is printed:**

```c
#include <stdio.h>
#include <sys/types.h>
#include <unistd.h>
int main()
{
    fork();
    fork();
    fork();
    printf("hello\n");
    return 0;
}
```
```output
hello
hello
hello
hello
hello
hello
hello
hello
```

*The number of times ‘hello’ is printed is equal to number of process created. Total Number of Processes = 2n, where n is number of fork system calls. So here n = 3, 23 = 8*

**Let us put some label names for the three lines:**
```
fork ();   // Line 1
fork ();   // Line 2
fork ();   // Line 3

       L1       // There will be 1 child process 
    /     \     // created by line 1.
  L2      L2    // There will be 2 child processes
 /  \    /  \   //  created by line 2
L3  L3  L3  L3  // There will be 4 child processes 
                // created by line 3
```

*So there are total eight processes (new child processes and one original process).*

*If we want to represent the relationship between the processes as a tree hierarchy it would be the following:*

- **The main process: P0**
- **Processes created by the 1st fork: P1**
- **Processes created by the 2nd fork: P2, P3**
- **Processes created by the 3rd fork: P4, P5, P6, P7**
```
             P0
         /   |   \
       P1    P4   P2
      /  \          \
    P3    P6         P5
   /
 P7
 ```

 **3. Predict the Output of the following program:**

```c
#include <stdio.h>
#include <sys/types.h>
#include <unistd.h>
void forkexample()
{
    // child process because return value zero
    if (fork() == 0)
        printf("Hello from Child!\n");

    // parent process because return value non-zero.
    else
        printf("Hello from Parent!\n");
}
int main()
{
    forkexample();
    return 0;
}
```
```output
1.
Hello from Child!
Hello from Parent!
     (or)
2.
Hello from Parent!
Hello from Child!
```

*In the above code, a child process is created. fork() returns 0 in the child process and positive integer in the parent process.
Here, two outputs are possible because the parent process and child process are running concurrently. So we don’t know whether the OS will first give control to the parent process or the child process.*

***Important:** Parent process and child process are running the same program, but it does not mean they are identical. OS allocate different data and states for these two processes, and the control flow of these processes can be different.* 


**4. Predict the Output of the following program:**
```c
#include <stdio.h>
#include <sys/types.h>
#include <unistd.h>

void forkexample()
{
    int x = 1;

    if (fork() == 0)
        printf("Child has x = %d\n", ++x);
    else
        printf("Parent has x = %d\n", --x);
}
int main()
{
    forkexample();
    return 0;
}
```
```output
Parent has x = 0
Child has x = 2
     (or)
Child has x = 2
Parent has x = 0
```
*Here, global variable change in one process does not affected two other processes because data/state of two processes are different. And also parent and child run simultaneously so two outputs are possible.*

**GATE-CS-2005**

```c
#include <stdio.h>
#include <sys/types.h>
#include <unistd.h>

void forkexample()
{
    int a = 5;
    if (fork() == 0) {
        a = a + 5;
        printf("%d, %x\n", a, &a);
    }
    else {
        a = a - 5;
        printf("%d, %x\n", a, &a);
}

}
int main()
{
    forkexample();
    return 0;
}
```
```output
0, 2b5e6224
10, 2b5e6224
```

*The physical addresses of ‘a’ in parent and child must be different. But our program accesses virtual addresses (assuming we are running on an OS that uses virtual memory). The child process gets an exact copy of parent process and virtual address of ‘a’ doesn’t change in child process. Therefore, we get same addresses in both parent and child. But in python3 v and y will not be equal.*

https://www.geeksforgeeks.org/fork-and-binary-tree/

**A note on C/C++ logical operators:**

*The logical operator && has more precedence than ||, and have left to right associativity. After executing left operand, the final result will be estimated and execution of right operand depends on outcome of left operand as well as type of operation.*

```c
#include <stdio.h>
#include <sys/types.h>
#include <unistd.h>

int print_num(int num)
{
    printf(" %d ", num);
    return num;
}

int main()
{
    print_num(0) && print_num(0) || print_num(0);
    printf("\n");
    print_num(1) && print_num(0) || print_num(0);
    printf("\n");
    print_num(0) && print_num(1) || print_num(0);
    printf("\n");
    print_num(0) && print_num(0) || print_num(1);
    printf("\n");
    print_num(1) && print_num(1) || print_num(0);
    printf("\n");
    print_num(0) && print_num(1) || print_num(1);
    printf("\n");
    print_num(1) && print_num(0) || print_num(1);
    printf("\n");
    print_num(1) && print_num(1) || print_num(1);
    printf("\n");
    return 0;
}
```
```output
0  0 
1  0  0 
0  0 
0  1 
1  1 
0  1 
1  0  1 
1  1 
```

#027 - Bubble Sort
```c
#include <stdio.h>

int main(int argc, char *argv[]) 
{  

    int a[10] = {8, 20, 5, 11, 21, 45, 7, 2, 22, 17};
    int temp;

    int count, current;

    for ( count=9; count > 0; count--)
    {
        for(current=0; current<count; current++)
        {
            if(a[current] > a[current+1])
            {
                temp = a[current];
                a[current] = a[current+1];
                a[current+1] = temp;
            }
        }
    }

    for (count=0; count<10; count++)
        printf("a[%d] = %d\n", count, a[count]);

    return 0;
}
```
```output
a[0] = 2
a[1] = 5
a[2] = 7
a[3] = 8
a[4] = 11
a[5] = 17
a[6] = 20
a[7] = 21
a[8] = 22
a[9] = 45
```

```c
#include <stdio.h>
#include <stdlib.h>

void sorted_bubble(int **array,int length)
{

    int temp_value, count, current;
    for (count = 0; count > 0; count--)
    {
        for (current = 0; current < count; current++)
        {
            if((*array)[current] > (*array)[current + 1])
            {
                temp_value = (*array)[current];
                (*array)[current] = (*array)[current + 1];
                (*array)[current + 1] = temp_value;
            }
        }
    }

}

void print(int *array, int length)
{
    int i;
    for(i = 0 ; i < length ; i++)
        printf("%d ", array[i]);
    printf("\n");
}

int main(int argc, char *argv[]) 
{   
    int length = 3;
    int* test_array = calloc(length, sizeof(int));
    test_array[0] = 1;
    test_array[1] = 2;
    test_array[2] = 3;
    sorted_bubble(&test_array, length);
    print(test_array, length);
    return 0;
}
```
```output
1 2 3 
```

#028 - Recursion

```c
#include <stdio.h>

int accumlate(int a)
{
    int ret;
    a = a*2 + 2;
    printf("a = %d\n", a);
    if (a < 100)
        ret = accumlate(a);
    else
        ret = a ;
    printf("ret = %d\n", ret);
    return ret;
}

int main(int argc, char *argv[]) 
{  
    int ret;
    ret = accumlate(1);
    printf("main: ret = %d\n", ret);

    return 0;
}
```
```output
a = 4
a = 10
a = 22
a = 46
a = 94
a = 190
ret = 190
ret = 190
ret = 190
ret = 190
ret = 190
ret = 190
main: ret = 190
```

#029 - pthreads

```c
#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>
#include <unistd.h>

void *myfunc (void *myvar);

int main(int argc, char *argv[]) 
{   
    pthread_t thread1, thread2;
    char *msg1 = "First thread";
    char *msg2 = "Second thread";
    int ret1, ret2;

    ret1 = pthread_create(&thread1, NULL, myfunc, (void *) msg1);
    ret2 = pthread_create(&thread2, NULL, myfunc, (void *) msg2);

    printf("Main function after pthread_create\n");

    pthread_join(thread1, NULL);
    pthread_join(thread2, NULL);
    printf("First thread ret1 = %d\n", ret1);
    printf("First thread ret2 = %d\n", ret2);

    return 0;
}

void *myfunc (void *myvar)
{
    char *msg;
    msg = (char *) myvar;

    int i;
    for (i=0; i<10; i++)
    {
        printf("%s %d\n", msg, i);
        sleep(1);
    }

    return NULL;
}
```
```sh
gcc -pthread -o helloworld helloworld.c
```
```output
Main function after pthread_create
Second thread 0
First thread 0
First thread 1
Second thread 1
First thread 2
Second thread 2
First thread 3
Second thread 3
First thread 4
Second thread 4
First thread 5
Second thread 5
Second thread 6
First thread 6
First thread 7
Second thread 7
First thread 8
Second thread 8
First thread 9
Second thread 9
First thread ret1 = 0
First thread ret2 = 0
```

```c
#include <pthread.h>
#include <string.h>
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <errno.h>
#include <ctype.h>

#define handle_error_en(en, msg) \
    do { errno = en; perror(msg); exit(EXIT_FAILURE); } while (0)


#define handle_error(msg) \
    do { perror(msg); exit(EXIT_FAILURE); } while(0)

struct thread_info { /* Used as argument to thread_start */
    pthread_t   thread_id;      /* ID returned by pthread_create() */
    int         thread_num;     /* Application-defined thread # */
    char        *argv_string;   /* From command-line argument */
};

/*  Thread start function: display address near top of our stack,
    and return upper-cased copy of argv_string */

static void * thread_start(void *arg)
{
    struct thread_info *tinfo = arg;
    char *uargv, *p;

    printf("Thread %d: top of stack near %p; arv_string=%s\n",
            tinfo->thread_num, &p, tinfo->argv_string);

    uargv = strdup(tinfo->argv_string);
    if (uargv == NULL)
        handle_error("strdup");
    for (p = uargv; *p != '\0'; p++)
        *p = toupper(*p);
    
    return uargv;
}    

int main(int argc, char *argv[])
{
    int s, tnum, opt, num_threads;
    struct thread_info *tinfo;
    pthread_attr_t attr;
    int stack_size;
    void *res;

    /*  The "-s" option specifies a stack size for our threads */

    stack_size = -1;
    while ((opt = getopt(argc, argv, "s: ")) != -1) {
        switch (opt)
        {
        case 's':
            stack_size = strtoul(optarg, NULL, 0);
            break;
        
        default:
            fprintf(stderr, "Usage: %s [-s stack-size] arg...\n", argv[0]);
            exit(EXIT_FAILURE);
            break;
        }
    }
    
    num_threads = argc - optind;

    /*  Initialized thread creation attributes */

    s = pthread_attr_init(&attr);
    if (s != 0)
        handle_error_en(s, "pthread_attr_init");

    if (stack_size > 0) {
        s = pthread_attr_setstacksize(&attr, stack_size);
        if (s != 0)
            handle_error_en(s, "pthread_attr_setstacksize");
    }

    /*  Allocate memory for pthread_create() arguments */

    tinfo = calloc(num_threads, sizeof(struct thread_info));
    if (tinfo == NULL)
        handle_error("calloc");
    
    /*  Create one thread for each command-line argument */

    for (tnum = 0; tnum < num_threads; tnum++) {
        tinfo[tnum].thread_num = tnum + 1;
        tinfo[tnum].argv_string = argv[optind + tnum];

        /*  The pthread_create() call stores the thread ID into corresponding element of tinfo[]*/

        s = pthread_create(&tinfo[tnum].thread_id, &attr, &thread_start, &tinfo[tnum]);
        if (s != 0)
            handle_error_en(s, "pthread_create");
    }

    /* Destroy the thread attributes object, since it is no longer needed */

    s = pthread_attr_destroy(&attr);
    if (s != 0)
        handle_error_en(s, "pthread_attr_destroy");

    /* Now join with each thread, and display its returned value */

    for (tnum = 0; tnum < num_threads; tnum++) {
        s = pthread_join(tinfo[tnum].thread_id, &res);
        if (s != 0)
            handle_error_en(s, "pthread_join");
        
        printf("Joined with thread %d; return value was %s\n",
                tinfo[tnum].thread_num, (char *)res);
        free(res);
    }

    free(tinfo);
    exit(EXIT_SUCCESS);
}
```
```sh
ulimit -s
`=>
8192            # The stack size limit is 8 MB (0x800000 bytes)
```
```sh
gcc -pthread -o main main.c
./main hola salut servus
`=>
Thread 1: top of stack near 0x7f1a184fded0; arv_string=hola
Thread 2: top of stack near 0x7f1a17cfced0; arv_string=salut
Joined with thread 1; return value was HOLA
Joined with thread 2; return value was SALUT
Thread 3: top of stack near 0x7f1a174fbed0; arv_string=servus
Joined with thread 3; return value was SERVUS
```

#030 - scanf() Function

```c
#include <stdio.h>

int main(int argc, char *argv[]) 
{   
    int input;
    scanf("%d", &input);
    printf("input = %d\n", input);

    char name[10];
    scanf("%s", name);
    printf("name = %s\n", name);

    return 0;
}
```
***Recommend to use command line instead of scanf!***


#031 - Switch-Case

#032 - qsort

```c
#include <stdio.h>
#include <stdlib.h>

int comparefunc(const void *a, const void *b)
{
    return ( *(int*)a - *(int*)b );
}

int main(int argc, char *argv[]) 
{
    int numbers[] = {5, 2, 23, 14, 7, 8, 42, 1, 33 ,10};

    printf("Before sorted:\n");
    for (int i=0; i<10; i++)
        printf("%d ", numbers[i]);
    printf("\n\n");

    qsort(numbers, 10, sizeof(int), comparefunc);

    printf("After sorted:\n");
    for (int i=0; i<10; i++)
        printf("%d ", numbers[i]);
    printf("\n\n");
    
    return 0;
}
```
```output
Before sorted:
5 2 23 14 7 8 42 1 33 10 

After sorted:
1 2 5 7 8 10 14 23 33 42 
```

```c
void qsort(void *base, size_t nitems, size_t size, int (*compar)(const void *, const void*))
```

* base − This is the pointer to the first element of the array to be sorted.

* nitems − This is the number of elements in the array pointed by base.

* size − This is the size in bytes of each element in the array.

* compar − This is the function that compares two elements.

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

static int cmpstringp(const void *p1, const void *p2)
{
    /*  The actual arguments to this function are "pointers 
        to pointers to char", but strcmp(3) arguments are 
        "pointers to char", hence the following cast 
        plus dereference */
    
    return strcmp(* (char * const *) p1, * (char * const *) p2);
}

int main(int argc, char *argv[])
{
    int j;

    if (argc < 2){
        fprintf(stderr, "Usage: %s <string>...\n", argv[0]);
        exit(EXIT_FAILURE);
    }

    qsort(&argv[1], argc - 1, sizeof(char *), cmpstringp);

    for (j = 1; j < argc; j++) 
        puts(argv[j]);
    exit(EXIT_SUCCESS);
}
```
```sh
./main s f w x A b
`=>
A
b
f
s
w
x
```


#033 - read() write() Functions

```c
#include <stdio.h>
#include <unistd.h>

int main(int argc, char *argv[]) 
{
    char buf[10];
    int ret;

    while (1)
    {
        ret = read(0, buf, 10);

        if(ret < 10)
        {
            buf[ret] = '\0';
            printf("%s\n", buf);
            break;
        } else
            printf("%s\n", buf);
    }
    
    
    return 0;
}
```

#034 - Socket Programming

```c
#include <stdio.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <string.h>
#include <stdlib.h>
#include <unistd.h>

int main(int argc, char *argv[]) 
{
    
    /* Variables */
    int sock;
    struct sockaddr_in server;
    int mysock;
    char buf[1024];
    int rval;

    /* Create socket */   
    sock = socket(AF_INET, SOCK_STREAM, 0);
    if (sock < 0) 
    {
        perror("Failed to create socket.");
        close(sock);
        exit(1);
    }

    server.sin_family = AF_INET;
    server.sin_addr.s_addr = INADDR_ANY;
    server.sin_port = htons(5000);

    /* Call bind */  
    if(bind(sock, (struct sockaddr *) &server, sizeof(server))) 
    {
        perror("Bind failed.");
        close(sock);
        exit(1);
    }

    /* Listen */ 
    listen(sock, 5);

    /* Accpet */   
    do {
        mysock = accept(sock, (struct sockaddr *) 0, 0);
        if(mysock == -1)
        {
            close(sock);
            perror("Accept failed.");
        } else
        {
            memset(buf, 0, sizeof(buf));
            if((rval = recv(mysock, buf, sizeof(buf), 0)) < 0 )
                perror("Reading stream message error");
            else if (rval == 0)
                printf("Ending connection.\n");
            else
                printf("MSG: %s\n", buf);
            printf("Got the message: (rval = %d)\n", rval);
            close(mysock);
        }
    } while(1);
    
    return 0;
}
```
```c
#include <stdio.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <string.h>
#include <stdlib.h>
#include <unistd.h>
#include <netdb.h>

#define DATA "Hello World of socket"

int main(int argc, char *argv[]) 
{
    
    /* Variables */
    int sock;
    struct sockaddr_in server;
    struct hostent *hp;
    char buf[1024];

    /* Create socket */   
    sock = socket(AF_INET, SOCK_STREAM, 0);
    if (sock < 0) 
    {
        perror("Failed to create socket.");
        exit(1);
    }

    server.sin_family = AF_INET;
    // server.sin_addr.s_addr = INADDR_ANY;
    // server.sin_port = 5000;
    hp = gethostbyname(argv[1]);
    if(hp == 0)
    {
        perror("Get host via gethostbyname failed.");
        close(sock);
        exit(1);
    }

    memcpy(&server.sin_addr, hp->h_addr, hp->h_length);
    server.sin_port = htons(5000);

    if (connect(sock, (struct sockaddr *) &server, sizeof(server)))
    {
        perror("Connect server failed.");
        close(sock);
        exit(1);
    } 

    if (send(sock, DATA, sizeof(DATA), 0) < 0)
    {
        perror("Send data failed.");
        close(sock);
        exit(1);
    }
    printf("Sent %s\n", DATA);
    close(sock);
    
    return 0;
}
```
```sh
./server
MSG: Hello World of socket
`=>
Got the message: (rval = 22)
```
```sh
./client localhost
`=>
Sent Hello World of socket
```

***Offical Example***
*server.c*
```c
#include <sys/types.h> // ssize_t
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h> // socklen_t
#include <string.h> // memset
#include <sys/socket.h> // sockaddr_storage, bind, socket
#include <netdb.h> // addrinfo, freeaddrinfo

#define BUF_SIZE 500

int main(int argc, char *argv[])
{
    struct addrinfo hints;
    struct addrinfo *result, *rp;
    int sfd, s;
    struct sockaddr_storage peer_addr;
    socklen_t peer_addr_len;
    ssize_t nread;
    char buf[BUF_SIZE];

    if (argc != 2) {
        fprintf(stderr, "Usage: %s port\n", argv[0]);
        exit(EXIT_FAILURE);
    }

    memset(&hints, 0, sizeof(struct addrinfo));
    hints.ai_family = AF_UNSPEC; /* Allow IPv4 or IPv6 */
    hints.ai_socktype = SOCK_DGRAM; /* Datagram socket */
    hints.ai_flags = AI_PASSIVE; /* For wildcard IP address */
    hints.ai_protocol = 0; /* Any protocol */
    hints.ai_canonname = NULL; 
    hints.ai_addr = NULL;
    hints.ai_next = NULL;

    s = getaddrinfo(NULL, argv[1], &hints, &result);
    if (s != 0) {
        fprintf(stderr, "getaddrinfo: %s\n", gai_strerror(s));
        exit(EXIT_FAILURE);
    }

    /*  getaddrinfo() returns a list of address structures.
        Try each address until we successfully bind(2).
        If socket(2) (or bind(2)) fails, we (close the socket 
        and) try the next address. */

    for (rp = result; rp != NULL; rp = rp->ai_next) {
        sfd = socket(rp->ai_family, rp->ai_socktype, rp->ai_protocol);
        if (sfd == -1)
            continue;
        if(bind(sfd, rp->ai_addr, rp->ai_addrlen) == 0)
            break;                      /* success */
        close(sfd);
    }

    if (rp == NULL) {                   /* No address succeeded */
        fprintf(stderr, "Could not bind\n");
        exit(EXIT_FAILURE);
    }

    freeaddrinfo(result);               /* No longer needed */

    /* Read datagrams and echo them back to sender */

    for (;;) {
        peer_addr_len = sizeof(struct sockaddr_storage);
        nread = recvfrom(sfd, buf, BUF_SIZE, 0, 
                (struct sockaddr *) &peer_addr, &peer_addr_len);
        if (nread == -1)
            continue;                   /* Ignore failed request */

        char host[NI_MAXHOST], service[NI_MAXSERV];

        s = getnameinfo((struct sockaddr *) &peer_addr,
                        peer_addr_len, host, NI_MAXHOST,
                        service, NI_MAXSERV, NI_NUMERICSERV);

        if (s == 0)
            printf("Received %zd bytes from %s:%s\n",
                    nread, host, service);
        else
            fprintf(stderr, "getnameinfo: %s\n", gai_strerror(s));

        if (sendto(sfd, buf, nread, 0, 
                    (struct sockaddr *) &peer_addr,
                    peer_addr_len) != nread)
            fprintf(stderr, "Error sending response\n");
    }

}
```

*client.c*
```c
#include <sys/types.h> 
#include <sys/socket.h> 
#include <netdb.h> 
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h> 
#include <string.h> 


#define BUF_SIZE 500

int main(int argc, char *argv[])
{
    struct addrinfo hints;
    struct addrinfo *result, *rp;
    int sfd, s, j;
    size_t len;
    ssize_t nread;
    char buf[BUF_SIZE];

    if (argc < 3) {
        fprintf(stderr, "Usage: %s host port msg\n", argv[0]);
        exit(EXIT_FAILURE);
    }

    /*  Obtain address(es) mathcing host/port */

    memset(&hints, 0, sizeof(struct addrinfo));
    hints.ai_family = AF_UNSPEC; /* Allow IPv4 or IPv6 */
    hints.ai_socktype = SOCK_DGRAM; /* Datagram socket */
    hints.ai_flags = 0; 
    hints.ai_protocol = 0; /* Any protocol */

    s = getaddrinfo(argv[1], argv[2], &hints, &result);
    if (s != 0) {
        fprintf(stderr, "getaddrinfo: %s\n", gai_strerror(s));
        exit(EXIT_FAILURE);
    }

    /*  getaddrinfo() returns a list of address structures.
        Try each address until we successfully bind(2).
        If socket(2) (or bind(2)) fails, we (close the socket 
        and) try the next address. */

    for (rp = result; rp != NULL; rp = rp->ai_next) {
        sfd = socket(rp->ai_family, rp->ai_socktype, rp->ai_protocol);
        if (sfd == -1)
            continue;
        if(connect(sfd, rp->ai_addr, rp->ai_addrlen) != -1)
            break;                      /* success */
        close(sfd);
    }

    if (rp == NULL) {                   /* No address succeeded */
        fprintf(stderr, "Could not connect\n");
        exit(EXIT_FAILURE);
    }

    freeaddrinfo(result);               /* No longer needed */

    /* Read datagrams and echo them back to sender */

    for (j = 3; j < argc; j++) {
        len = strlen(argv[j]) + 1; /* +1 for terminating null byte */

        if (len > BUF_SIZE) {
            fprintf(stderr,
                    "Ignoring long message in argument %d\n", j);
            continue;
        }

        if (write(sfd, argv[j], len) != len) {
            fprintf(stderr, "partial/failed write\n");
            exit(EXIT_FAILURE);
        }

        nread = read(sfd, buf, BUF_SIZE);
        if (nread == -1) {
            perror("read");
            exit(EXIT_FAILURE);
        }

        printf("Received %zd bytes: %s\n", nread, buf);
    }

    exit(EXIT_SUCCESS);


}
```


#035 (Rev. 2) - Linked List

{ ["Paul"] ["Gonzales"] [18] [next->{"{Peter"}] }
{ ["Peter"] ["Mars"] [24] [next->{"John"}] }
{ ["John"] ["Doe"] [34] [next->*{"Andy"}] }
{ ["Andy"] ["Mars"] [22] [NULL] }

```c
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

typedef struct  people_tag
{
    char firstname[16];
    char lastname[16];
    unsigned int age;
    struct people_tag *next;
} people_t;


int main(int argc, char *argv[]) 
{
    people_t *head = NULL;
    people_t *new;
    people_t *list;

    char *name[] = {"Andy", "John", "Peter", "Paul", NULL};
    char *last[] = {"Mars", "Doe", "Mars", "Gonzales", NULL};
    unsigned int age[] = {22, 34, 24, 18, 0};

    int i = 0;

    while (name[i])
    {
        new = (people_t *) malloc(sizeof(people_t));
        if (new == NULL)
        {
            fprintf(stderr, "Unable to allocate memory.\n");
            exit(1);
        }

        strcpy(new->firstname, name[i]);
        strcpy(new->lastname, last[i]);
        new->age = age[i];
        new->next = head;
        head = new;
        i++;
    }
    
    list = head;

    while (list != NULL)
    {
        printf("Firstname: %s\n", list->firstname);
        printf("Lasttname: %s\n", list->lastname);
        printf("Age: %d\n", list->age);

        list = list->next;
    }

    list = head;

    while (list != NULL)
    {
        head = list->next;
        free(list);
        list = head;
    }

    return 0;
}
```
```output
Firstname: Paul
Lasttname: Gonzales
Age: 18
Firstname: Peter
Lasttname: Mars
Age: 24
Firstname: John
Lasttname: Doe
Age: 34
Firstname: Andy
Lasttname: Mars
Age: 22
```

## 35.1 Why Linked List?

Why Linked List? 
Arrays can be used to store linear data of similar types, but arrays have the following limitations. 
1) The size of the arrays is fixed: So we must know the upper limit on the number of elements in advance. Also, generally, the allocated memory is equal to the upper limit irrespective of the usage. 
2) Inserting a new element in an array of elements is expensive because the room has to be created for the new elements and to create room existing elements have to be shifted. 
For example, in a system, if we maintain a sorted list of IDs in an array id[]. 
id[] = [1000, 1010, 1050, 2000, 2040]. 
And if we want to insert a new ID 1005, then to maintain the sorted order, we have to move all the elements after 1000 (excluding 1000). 
Deletion is also expensive with arrays until unless some special techniques are used. For example, to delete 1010 in id[], everything after 1010 has to be moved.
Advantages over arrays 
1) Dynamic size 
2) Ease of insertion/deletion
Drawbacks: 
1) Random access is not allowed. We have to access elements sequentially starting from the first node. So we cannot do binary search with linked lists efficiently with its default implementation. Read about it here. 
2) Extra memory space for a pointer is required with each element of the list. 
3) Not cache friendly. Since array elements are contiguous locations, there is locality of reference which is not there in case of linked lists.
Representation: 
A linked list is represented by a pointer to the first node of the linked list. The first node is called the head. If the linked list is empty, then the value of the head is NULL. 
Each node in a list consists of at least two parts: 
1) data 
2) Pointer (Or Reference) to the next node 
In C, we can represent a node using structures. Below is an example of a linked list node with integer data. 
In Java or C#, LinkedList can be represented as a class and a Node as a separate class. The LinkedList class contains a reference of Node class type. 

```c
// A linked list node
struct Node {
    int data;
    struct Node* next;
};
```

```cpp
class Node {
public:
    int data;
    Node* next;
};
```

```java
class LinkedList {
    Node head; // head of the list
 
    /* Linked list Node*/
    class Node {
        int data;
        Node next;
 
        // Constructor to create a new node
        // Next is by default initialized
        // as null
        Node(int d) { data = d; }
    }
}
```
## 35.2 Creating a Node

**First Simple Linked List in C** Let us create a simple linked list with 3 nodes.

```c
// A simple C program to introduce
// a linked list
#include <stdio.h>
#include <stdlib.h>
 
struct Node {
    int data;
    struct Node* next;
};
 
// Program to create a simple linked
// list with 3 nodes
int main()
{
    struct Node* head = NULL;
    struct Node* second = NULL;
    struct Node* third = NULL;
 
    // allocate 3 nodes in the heap
    head = (struct Node*)malloc(sizeof(struct Node));
    second = (struct Node*)malloc(sizeof(struct Node));
    third = (struct Node*)malloc(sizeof(struct Node));
 
    /* Three blocks have been allocated dynamically.
     We have pointers to these three blocks as head,
     second and third    
       head           second           third
        |                |               |
        |                |               |
    +---+-----+     +----+----+     +----+----+
    | #  | #  |     | #  | #  |     |  # |  # |
    +---+-----+     +----+----+     +----+----+
    
   # represents any random value.
   Data is random because we haven’t assigned
   anything yet  */
 
    head->data = 1; // assign data in first node
    head->next = second; // Link first node with
    // the second node
 
    /* data has been assigned to the data part of the first
     block (block pointed by the head). And next
     pointer of first block points to second. 
     So they both are linked.
 
       head          second         third
        |              |              |
        |              |              |
    +---+---+     +----+----+     +-----+----+
    | 1  | o----->| #  | #  |     |  #  | #  |
    +---+---+     +----+----+     +-----+----+   
  */
 
    // assign data to second node
    second->data = 2;
 
    // Link second node with the third node
    second->next = third;
 
    /* data has been assigned to the data part of the second
     block (block pointed by second). And next
     pointer of the second block points to the third
     block. So all three blocks are linked.
   
       head         second         third
        |             |             |
        |             |             |
    +---+---+     +---+---+     +----+----+
    | 1  | o----->| 2 | o-----> |  # |  # |
    +---+---+     +---+---+     +----+----+      */
 
    third->data = 3; // assign data to third node
    third->next = NULL;
 
    /* data has been assigned to data part of third
    block (block pointed by third). And next pointer
    of the third block is made NULL to indicate
    that the linked list is terminated here.
 
     We have the linked list ready. 
 
           head   
             |
             |
        +---+---+     +---+---+       +----+------+
        | 1  | o----->|  2  | o-----> |  3 | NULL |
        +---+---+     +---+---+       +----+------+      
    
     
    Note that only head is sufficient to represent
    the whole list.  We can traverse the complete
    list by following next pointers.    */
 
    return 0;
}
```

**Linked List Traversal**
```c
void printList(struct Node* n)
{
    while (n != NULL) {
        printf(" %d ", n->data);
        n = n->next;
    }
    printf("\n");
}
```

## 35.3 Inserting Nodes 

**Add a node at the front: (4 steps process)**

```c
/* Given a reference (pointer to pointer) to the head of a list
   and an int,  inserts a new node on the front of the list. */
void push(struct Node** head_ref, int new_data)
{
    /* 1. allocate node */
    struct Node* new_node = (struct Node*) malloc(sizeof(struct Node));
  
    /* 2. put in the data  */
    new_node->data  = new_data;
  
    /* 3. Make next of new node as head */
    new_node->next = (*head_ref);
  
    /* 4. move the head to point to the new node */
    (*head_ref)    = new_node;
}
```

**Add a node after a given node: (5 steps process)**

```c
/* Given a node prev_node, insert a new node after the given
prev_node */
void insertAfter(struct Node* prev_node, int new_data)
{
    /*1. check if the given prev_node is NULL */
    if (prev_node == NULL)
    {
        printf("the given previous node cannot be NULL");    
        return;
    }
         
    /* 2. allocate new node */
    struct Node* new_node =(struct Node*) malloc(sizeof(struct Node));
 
    /* 3. put in the data */
    new_node->data = new_data;
 
    /* 4. Make next of new node as next of prev_node */
    new_node->next = prev_node->next;
 
    /* 5. move the next of prev_node as new_node */
    prev_node->next = new_node;
}
```

**Add a node at the end: (6 steps process)**

```c
/* Given a reference (pointer to pointer) to the head
   of a list and an int, appends a new node at the end  */
void append(struct Node** head_ref, int new_data)
{
    /* 1. allocate node */
    struct Node* new_node = (struct Node*) malloc(sizeof(struct Node));
 
    struct Node *last = *head_ref;  /* used in step 5*/
  
    /* 2. put in the data  */
    new_node->data  = new_data;
 
    /* 3. This new node is going to be the last node, so make next
          of it as NULL*/
    new_node->next = NULL;
 
    /* 4. If the Linked List is empty, then make the new node as head */
    if (*head_ref == NULL)
    {
       *head_ref = new_node;
       return;
    } 
      
    /* 5. Else traverse till the last node */
    while (last->next != NULL)
        last = last->next;
  
    /* 6. Change the next of last node */
    last->next = new_node;
    return;   
}
```

**Completed Code**
```c
// A simple C program to introduce
// a linked list
#include <stdio.h>
#include <stdlib.h>
 
struct Node {
    int data;
    struct Node* next;
};

void printList(struct Node* n)
{
    while (n != NULL) {
        printf(" %d ", n->data);
        n = n->next;
    }
    printf("\n");
}

/* Given a reference (pointer to pointer) to the head of a list
   and an int,  inserts a new node on the front of the list. */
void push(struct Node** head_ref, int new_data)
{
    /* 1. allocate node */
    struct Node* new_node = (struct Node*) malloc(sizeof(struct Node));
  
    /* 2. put in the data  */
    new_node->data  = new_data;
  
    /* 3. Make next of new node as head */
    new_node->next = (*head_ref);
  
    /* 4. move the head to point to the new node */
    (*head_ref)    = new_node;
}

/* Given a node prev_node, insert a new node after the given
prev_node */
void insertAfter(struct Node* prev_node, int new_data)
{
    /*1. check if the given prev_node is NULL */
    if (prev_node == NULL)
    {
        printf("the given previous node cannot be NULL");    
        return;
    }
         
    /* 2. allocate new node */
    struct Node* new_node =(struct Node*) malloc(sizeof(struct Node));
 
    /* 3. put in the data */
    new_node->data = new_data;
 
    /* 4. Make next of new node as next of prev_node */
    new_node->next = prev_node->next;
 
    /* 5. move the next of prev_node as new_node */
    prev_node->next = new_node;
}

/* Given a reference (pointer to pointer) to the head
   of a list and an int, appends a new node at the end  */
void append(struct Node** head_ref, int new_data)
{
    /* 1. allocate node */
    struct Node* new_node = (struct Node*) malloc(sizeof(struct Node));
 
    struct Node *last = *head_ref;  /* used in step 5*/
  
    /* 2. put in the data  */
    new_node->data  = new_data;
 
    /* 3. This new node is going to be the last node, so make next
          of it as NULL*/
    new_node->next = NULL;
 
    /* 4. If the Linked List is empty, then make the new node as head */
    if (*head_ref == NULL)
    {
       *head_ref = new_node;
       return;
    } 
      
    /* 5. Else traverse till the last node */
    while (last->next != NULL)
        last = last->next;
  
    /* 6. Change the next of last node */
    last->next = new_node;
    return;   
}
 
int main()
{
    struct Node* head = NULL;
    struct Node* second = NULL;
    struct Node* third = NULL;
 
    // allocate 3 nodes in the heap
    head = (struct Node*)malloc(sizeof(struct Node));
    second = (struct Node*)malloc(sizeof(struct Node));
    third = (struct Node*)malloc(sizeof(struct Node));
 

 
    head->data = 1; // assign data in first node
    head->next = second; // Link first node with

    // the second node
    // assign data to second node
    second->data = 2;
    // Link second node with the third node
    second->next = third;

    third->data = 3; // assign data to third node
    third->next = NULL;

    push(&head, 6);
    insertAfter(second, 7);
    append(&head, 13);

    printList(head);
 
    return 0;
}
```
```output
 6  1  2  7  3  13
 ```

## 35.4 Deleting Node by Data

**Iterative Method:**
To delete a node from the linked list, we need to do the following steps. 
1) Find the previous node of the node to be deleted. 
2) Change the next of the previous node. 
3) Free memory for the node to be deleted.

```c
/* Given a reference (pointer to pointer) to the head of a
   list and a key, deletes the first occurrence of key in
   linked list */
void deleteNode(struct Node** head_ref, int key)
{
    // Store head node
    struct Node *temp = *head_ref, *prev;
 
    // If head node itself holds the key to be deleted
    if (temp != NULL && temp->data == key) {
        *head_ref = temp->next; // Changed head
        free(temp); // free old head
        return;
    }
 
    // Search for the key to be deleted, keep track of the
    // previous node as we need to change 'prev->next'
    while (temp != NULL && temp->data != key) {
        prev = temp;
        temp = temp->next;
    }
 
    // If key was not present in linked list
    if (temp == NULL)
        return;
 
    // Unlink the node from linked list
    prev->next = temp->next;
 
    free(temp); // Free memory
}
```

**Recursive Method:**

To delete a node of a linked list recursively we need to do the following steps.

1. We pass node* (node pointer) as a reference to the function (as in node* &head)

2. Now since the current node pointer is derived from the previous node’s next (which is passed by reference) so now if the value of the current node pointer is changed, the previous next node’s value also gets changed which is the required operation while deleting a node (i.e points previous node’s next to current node’s (containing key) next).

3. Find the node containing the given value.

4. Store this node to deallocate it later using the free() function.

5. Change this node pointer so that it points to its next and by performing this previous node’s next also gets properly linked.

```c
#include <stdio.h>
#include <stdlib.h>
 
// A linked list node
struct Node {
    int data;
    struct Node* next;
};

// This function prints contents of linked list starting
// from the given node
void printList(struct Node* node)
{
    while (node != NULL) {
        printf(" %d ", node->data);
        node = node->next;
    }
}
 
/* Given a reference (pointer to pointer) to the head of a
   list and an int, inserts a new node on the front of the
   list. */
void push(struct Node** head_ref, int new_data)
{
    struct Node* new_node
        = (struct Node*)malloc(sizeof(struct Node));
    new_node->data = new_data;
    new_node->next = (*head_ref);
    (*head_ref) = new_node;
}
 
/* Given a reference (pointer to pointer) to the head of a
   list and a key, deletes the first occurrence of key in
   linked list */
void deleteNode(struct Node** head_ref, int key)
{
    // Store head node
    struct Node *temp = *head_ref, *prev;
 
    // If head node itself holds the key to be deleted
    if (temp != NULL && temp->data == key) {
        *head_ref = temp->next; // Changed head
        free(temp); // free old head
        return;
    }
 
    // Search for the key to be deleted, keep track of the
    // previous node as we need to change 'prev->next'
    while (temp != NULL && temp->data != key) {
        prev = temp;
        temp = temp->next;
    }
 
    // If key was not present in linked list
    if (temp == NULL)
        return;
 
    // Unlink the node from linked list
    prev->next = temp->next;
 
    free(temp); // Free memory
}

void deleteNodeRecursively(struct Node** head_ref, int key)
{   
    struct Node* headNode = *head_ref;

    if (headNode == NULL) {
        printf("It's an empty list!\n");
        return;
    }

    if (headNode->data == key) {
        *head_ref = (headNode->next);
        free(headNode);
        return;
    }

    struct Node* nextNode = headNode->next;
    
    if (nextNode == NULL) {
        printf("The element %d is not present in the list.\n", key);
        return;
    }

    if (nextNode->data == key) {
        headNode->next = nextNode->next;
        free(nextNode);
        return;
    }

    deleteNodeRecursively(&nextNode, key);
}
 
 
// Driver code
int main()
{
    /* Start with the empty list */
    struct Node* head = NULL;
 
    push(&head, 7);
    push(&head, 1);
    push(&head, 3);
    push(&head, 2);
    push(&head, 6);
    push(&head, 5);
 
    puts("Created Linked List: ");
    printList(head);
    deleteNode(&head, 1);
    puts("\nLinked List after Deletion of 1: ");
    printList(head);
    puts("\nLinked List after Deletion Recursively of 6: ");
    deleteNodeRecursively(&head, 6);
    printList(head);
    puts("\nLinked List after Deletion Recursively of 5: ");
    deleteNodeRecursively(&head, 5);
    printList(head);
    puts("\nLinked List after Deletion Recursively of 7: ");
    deleteNodeRecursively(&head, 7);
    printList(head);
    puts("\nLinked List after Deletion Recursively of 7: ");
    deleteNodeRecursively(&head, 7);
    printList(head);
    puts("\nLinked List after Deletion Recursively of 3: ");
    deleteNodeRecursively(&head, 3);
    printList(head);
    puts("\nLinked List after Deletion Recursively of 2: ");
    deleteNodeRecursively(&head, 2);
    printList(head);
    puts("\nLinked List after Deletion Recursively of 2: ");
    deleteNodeRecursively(&head, 2);
    return 0;
}
```
```output
Created Linked List: 
 5  6  2  3  1  7 
Linked List after Deletion of 1: 
 5  6  2  3  7 
Linked List after Deletion Recursively of 6: 
 5  2  3  7 
Linked List after Deletion Recursively of 5: 
 2  3  7 
Linked List after Deletion Recursively of 7: 
 2  3 
Linked List after Deletion Recursively of 7: 
The element 7 is not present in the list.
 2  3 
Linked List after Deletion Recursively of 3: 
 2 
Linked List after Deletion Recursively of 2: 

Linked List after Deletion Recursively of 2: 
It's an empty list!
```

*Using recursive method can save more memory for the big list.*
```c
int main()
{
    unsigned int i;
    int max_count = 100000000;

    // struct Node* head_i = NULL;
    struct Node* head_r = NULL;

    for (i = 0; i < max_count; i++) {
        // push(&head_i, i);
        push(&head_r, i);
    }

    // clock_t begin_i = clock();
    // deleteNode(&head_i, max_count-1);
    // clock_t end_i =clock();
    // double time_spent_i = (double)(end_i - begin_i) / CLOCKS_PER_SEC;
    // printf("%f\n", time_spent_i);
 
    clock_t begin_r = clock();
    deleteNodeRecursively(&head_r, max_count-1);
    clock_t end_r =clock();
    double time_spent_r = (double)(end_r - begin_r) / CLOCKS_PER_SEC;
    printf("%f\n", time_spent_r);

    return 0;
}
```

## 35.5 Delete a Linked List node at a given position

```c
void deleteNode(struct Node** head_ref, int position)
{
    // If linked list is empty
    if (*head_ref == NULL)
        return;
 
    // Store head node
    struct Node* temp = *head_ref;
 
    // If head needs to be removed
    if (position == 0) {
        *head_ref = temp->next; // Change head
        free(temp); // free old head
        return;
    }
 
    // Find previous node of the node to be deleted
    for (int i = 0; temp != NULL && i < position - 1; i++)
        temp = temp->next;
 
    // If position is more than number of nodes
    if (temp == NULL || temp->next == NULL)
        return;
 
    // Node temp->next is the node to be deleted
    // Store pointer to the next of node to be deleted
    struct Node* next = temp->next->next;
 
    // Unlink the node from linked list
    free(temp->next); // Free memory
 
    temp->next = next; // Unlink the deleted node from list
}
```

## 35.6 Delete the Entire Linked List

```c
void deleteList(struct Node** head_ref)
{
   /* deref head_ref to get the real head */
   struct Node* current = *head_ref;
   struct Node* next;
 
   while (current != NULL)
   {
       next = current->next;
       free(current);
       current = next;
   }
   
   /* deref head_ref to affect the real head back
      in the caller. */
   *head_ref = NULL;
}
```

## 35.7 Find Length of a Linked List

**Iterative Solution**
1) Initialize count as 0 
2) Initialize a node pointer, current = head.
3) Do following while current is not NULL
     a) current = current -> next
     b) count++;
4) Return count 

```c
int getCount(struct Node* head)
{
    int count = 0;  // Initialize count
    struct Node* current = head;  // Initialize current
    while (current != NULL)
    {
        count++;
        current = current->next;
    }
    return count;
}
```

**Recursive Solution**
1) If head is NULL, return 0.
2) Else return 1 + getCount(head->next) 

```c
int getCount(Node* head)
{
    // Base Case
    if (head == NULL) {
        return 0;
    }
    // Count this node plus the rest of the list
    else {
        return 1 + getCount(head->next);
    }
}
```

## 35.8 Search an element in a Linked List

**Iterative Solution**
1) Initialize a node pointer, current = head.
2) Do following while current is not NULL
    a) current->key is equal to the key being searched return true.
    b) current = current->next
3) Return false 

```c
bool search(struct Node* head, int x)
{
    struct Node* current = head;  // Initialize current
    while (current != NULL)
    {
        if (current->key == x)
            return true;
        current = current->next;
    }
    return false;
}
```

**Recursive Solution**
1) If head is NULL, return false.
2) If head's key is same as x, return true;
3) Else return search(head->next, x) 

```c
bool search(struct Node* head, int x)
{
    // Base case
    if (head == NULL)
        return false;
     
    // If key is present in current node, return true
    if (head->key == x)
        return true;
 
    // Recur for remaining list
    return search(head->next, x);
}
```

## 35.9 To get Nth node in a Linked List

**Iterative Solution**
1. Initialize count = 0
2. Loop through the link list
     a. if count is equal to the passed index then return current
         node
     b. Increment count
     c. change current to point to next of the current.

```c
int GetNth(struct Node* head, int index)
{
 
    struct Node* current = head;
 
    // the index of the
    // node we're currently
    // looking at
    int count = 0;
    while (current != NULL) {
        if (count == index)
            return (current->data);
        count++;
        current = current->next;
    }
 
    /* if we get to this line,
       the caller was asking
       for a non-existent element
       so we assert fail */
    assert(0);
}
```

**Recursive Solution**
getnth(node,n)
1. Initialize count = 0
2. if count==n
     return node->data
3. else
    return getnth(node->next,n-1)

```c
int GetNth(struct Node* head, int n)
{
    // if length of the list is less
    // than the given index, return -1
    if (head == NULL)
        return -1;
 
    // if n equal to 0 return node->data
    if (n == 0)
        return head->data;
 
    // increase head to next pointer
    // n - 1: decrease the number of recursions until n = 0
    return GetNth(head->next, n - 1);
}
```


#036 - Shared Memory

*server.c*
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <sys/types.h>
#include <sys/ipc.h>
#include <sys/shm.h>

#define SHSIZE 100

int main(int argc, char *argv[]) 
{
    int shmid;
    key_t key;
    char *shm;
    char *s;

    key = 9876;

    shmid = shmget(key, SHSIZE, IPC_CREAT | 0666);
    if(shmid < 0)
    {
        perror("shmget");
        exit(1);
    }

    shm = shmat(shmid, NULL, 0);

    if(shm == (char *) -1)
    {
        perror("shmat");
        exit(1);
    }

    memcpy(shm, "Hello World", 11);

    s = shm;
    s += 11;

    *s = 0;

    while (*shm != '*')
        sleep(1);

    return 0;
}
```

*client.c*
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <sys/types.h>
#include <sys/ipc.h>
#include <sys/shm.h>

#define SHSIZE 100

int main(int argc, char *argv[]) 
{
    int shmid;
    key_t key;
    char *shm;
    char *s;

    key = 9876;

    shmid = shmget(key, SHSIZE, 0666);
    if(shmid < 0)
    {
        perror("shmget");
        exit(1);
    }

    shm = shmat(shmid, NULL, 0);

    if(shm == (char *) -1)
    {
        perror("shmat");
        exit(1);
    }

    for (s = shm; *s != 0; s++)
        printf("%c", *s);

    printf("\n");

    *shm = '*';

    return 0;
}
```
```output
Hello World
```

```sh
ipcs -m
`=>
------ Shared Memory Segments --------
key        shmid      owner      perms      bytes      nattch     status      
0x00000000 9          lawjune    600        524288     2          dest         
0x00000000 10         lawjune    600        630000     2          dest         
0x00000000 13         lawjune    600        524288     2          dest         
0x00000000 14         lawjune    600        524288     2          dest         
0x00000000 17         lawjune    600        524288     2          dest         
0x00000000 24         lawjune    600        524288     2          dest         
0x00000000 29         lawjune    600        524288     2          dest         
0x00000000 35         lawjune    600        33554432   2          dest         
0x00002694 46         lawjune    666        100        0  
```

```sh
ipcrm -M 9876
ipcs -m
`=>
------ Shared Memory Segments --------
key        shmid      owner      perms      bytes      nattch     status      
0x00000000 9          lawjune    600        524288     2          dest         
0x00000000 10         lawjune    600        630000     2          dest         
0x00000000 13         lawjune    600        524288     2          dest         
0x00000000 14         lawjune    600        524288     2          dest         
0x00000000 17         lawjune    600        524288     2          dest         
0x00000000 24         lawjune    600        524288     2          dest         
0x00000000 29         lawjune    600        524288     2          dest         
0x00000000 35         lawjune    600        33554432   2          dest   
```

***Inter Process Communication** through shared memory is a concept where two or more process can access the common memory. And communication is done via this shared memory where changes made by one process can be viewed by another process.*

*The problem with pipes, fifo and message queue – is that for two process to exchange information. The information has to go through the kernel.*

- Server reads from the input file.
- The server writes this data in a message using either a pipe, fifo or message queue.
- The client reads the data from the IPC channel,again requiring the data to be copied from kernel’s IPC buffer to the client’s buffer.
- Finally the data is copied from the client’s buffer.
*A total of four copies of data are required (2 read and 2 write). So, shared memory provides a way by letting two or more processes share a memory segment. With Shared Memory the data is only copied twice – from input file into shared memory and from shared memory to the output file.*

**SYSTEM CALLS USED ARE:**

- ***ftok():** is use to generate a unique key.*

- ***shmget(): int shmget(key_t,size_tsize,intshmflg); **upon successful completion, shmget() returns an identifier for the shared memory segment.*

- ***shmat():** Before you can use a shared memory segment, you have to attach yourself
to it using shmat(). void *shmat(int shmid ,void *shmaddr ,int shmflg);
shmid is shared memory id. shmaddr specifies specific address to use but we should set
it to zero and OS will automatically choose the address.*

- ***shmdt():** When you’re done with the shared memory segment, your program should
detach itself from it using shmdt(). int shmdt(void *shmaddr);*

- ***shmctl():** when you detach from shared memory,it is not destroyed. So, to destroy
shmctl() is used. shmctl(int shmid,IPC_RMID,NULL);*

*shm_writer.c*
```c
#include <sys/ipc.h>
#include <sys/shm.h>
#include <stdio.h>
  
int main()
{
    // ftok to generate unique key
    key_t key = ftok("shmfile",65);
  
    // shmget returns an identifier in shmid
    int shmid = shmget(key,1024,0666|IPC_CREAT);
  
    // shmat to attach to shared memory
    char *str = (char*) shmat(shmid,(void*)0,0);
  
    puts("Write Data : ");
    gets(str);
  
    printf("Data written in memory: %s\n",str);
      
    //detach from shared memory 
    shmdt(str);
  
    return 0;
}
```

*shm_reader.c*
```c
#include <sys/ipc.h>
#include <sys/shm.h>
#include <stdio.h>
  
int main()
{
    // ftok to generate unique key
    key_t key = ftok("shmfile",65);
  
    // shmget returns an identifier in shmid
    int shmid = shmget(key,1024,0666|IPC_CREAT);
  
    // shmat to attach to shared memory
    char *str = (char*) shmat(shmid,(void*)0,0);
  
    printf("Data read from memory: %s\n",str);
      
    //detach from shared memory 
    shmdt(str);
    
    // destroy the shared memory
    shmctl(shmid,IPC_RMID,NULL);
     
    return 0;
}
```

#037 - pipe() Function

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main(int argc, char *argv[]) 
{
    pid_t pid;
    int mypipefd[2];
    int ret;
    char buf[20];

    ret = pipe(mypipefd);

    if(ret == -1)
    {
        perror("pipe");
        exit(1);
    }

    pid = fork();
    
    if(pid == 0)
    {
        /* Child process */
        // mypipefd[0] - reading
        // mypipefd[1] - writing
        printf("Child process\n");
        close(mypipefd[0]);
        write(mypipefd[1], "Hello there!", 12);

    } else {
        /* Parent process */
        printf("Parent process\n");
        close(mypipefd[1]);
        read(mypipefd[0], buf, 15);
        printf("buf: %s\n", buf);
    }

    return 0;
}
```
```output
Parent process
Child process
buf: Hello there!�U
```
***Try to figure out how to avoid printing unexpected buf!***

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main(int argc, char *argv[]) 
{
    pid_t pid;
    int mypipefd[2];
    int ret;
    char* buf;
    buf = (char *) malloc(20);

    ret = pipe(mypipefd);

    if(ret == -1)
    {
        free(buf);
        perror("pipe");
        exit(1);
    }

    pid = fork();
    
    if(pid == 0)
    {
        /* Child process */
        // mypipefd[0] - reading
        // mypipefd[1] - writing
        printf("Child process\n");
        close(mypipefd[0]);
        write(mypipefd[1], "Hello there!", 12);

    } else {
        /* Parent process */
        printf("Parent process\n");
        close(mypipefd[1]);
        read(mypipefd[0], buf, 15);
        printf("buf: %s\n", buf);
    }

    free(buf);

    return 0;
}
```
```output
Parent process
Child process
buf: Hello there!
```

*Conceptually, a pipe is a connection between two processes, such that the standard output from one process becomes the standard input of the other process. In UNIX Operating System, Pipes are useful for communication between related processes(inter-process communication).*

- *Pipe is one-way communication only i.e we can use a pipe such that One process write to the pipe, and the other process reads from the pipe. It opens a pipe, which is an area of main memory that is treated as a **“virtual file”**.*

- *The pipe can be used by the creating process, as well as all its child processes, for reading and writing. One process can write to this “virtual file” or pipe and another related process can read from it.*

- *If a process tries to read before something is written to the pipe, the process is suspended until something is written.*

- *The pipe system call finds the first two available positions in the process’s open file table and allocates them for the read and write ends of the pipe.*

**Syntax in C language:**
```c
int pipe(int fds[2]);

Parameters :
fd[0] will be the fd(file descriptor) for the 
read end of pipe.
fd[1] will be the fd for the write end of pipe.
Returns : 0 on Success.
-1 on error.
```

*Pipes behave **FIFO**(First in First out), Pipe behave like a queue data structure. Size of read and write don’t have to match here. We can write **512** bytes at a time but we can read only **1** byte at a time in a pipe.*

```c
// C program to illustrate
// pipe system call in C
#include <stdio.h>
#include <unistd.h>
#define MSGSIZE 16
char* msg1 = "hello, world #1";
char* msg2 = "hello, world #2";
char* msg3 = "hello, world #3";
  
int main()
{
    char inbuf[MSGSIZE];
    int p[2], i;
  
    if (pipe(p) < 0)
        exit(1);
  
    /* continued */
    /* write pipe */
  
    write(p[1], msg1, MSGSIZE);
    write(p[1], msg2, MSGSIZE);
    write(p[1], msg3, MSGSIZE);
  
    for (i = 0; i < 3; i++) {
        /* read pipe */
        read(p[0], inbuf, MSGSIZE);
        printf("% s\n", inbuf);
    }
    return 0;
}
```
```output
hello, world #1
hello, world #2
hello, world #3
```

```c
// C program to illustrate
// pipe system call in C
// shared by Parent and Child
#include <stdio.h>
#include <unistd.h>
#define MSGSIZE 16
char* msg1 = "hello, world #1";
char* msg2 = "hello, world #2";
char* msg3 = "hello, world #3";

int main()
{
    char inbuf[MSGSIZE];
    int p[2], pid, nbytes;

    if (pipe(p) < 0)
        exit(1);

    /* continued */
    if ((pid = fork()) > 0) {
        write(p[1], msg1, MSGSIZE);
        write(p[1], msg2, MSGSIZE);
        write(p[1], msg3, MSGSIZE);

        // Adding this line will
        // not hang the program
        // close(p[1]);
        wait(NULL);
    }

    else {
        // Adding this line will
        // not hang the program
        // close(p[1]);
        while ((nbytes = read(p[0], inbuf, MSGSIZE)) > 0)
            printf("% s\n", inbuf);
        if (nbytes != 0)
            exit(2);
        printf("Finished reading\n");
    }
    return 0;
}
```
```output
hello world, #1
hello world, #2
hello world, #3
(hangs)         //program does not terminate but hangs
```

*Here, In this code After finishing reading/writing, both parent and child block instead of terminating the process and that’s why program hangs. This happens because read system call gets as much data it requests or as much data as the pipe has, whichever is less.*

- *If pipe is empty and we call read system call then Reads on the pipe will return **EOF** (return value 0) if no process has the write end open.*
- *If some other process has the pipe open for writing, read will block in anticipation of new data so this code output hangs because here write ends parent process and also child process doesn’t close.*

**C program to demonstrate fork() and pipe():**
*Write Linux C program to create two processes P1 and P2. P1 takes a string and passes it to P2. P2 concatenates the received string with another string without using string function and sends it back to P1 for printing.*

**Examples:**
```
Other string is: forgeeks.org

Input  : www.geeks
Output : www.geeksforgeeks.org
        
Input :  www.practice.geeks
Output : practice.geeksforgeeks.org
```

```c
// C program to demonstrate use of fork() and pipe()
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <unistd.h>

int main()
{
    // We use two pipes
    // First pipe to send input string from parent
    // Second pipe to send concatenated string from child

    int fd1[2]; // Used to store two ends of first pipe
    int fd2[2]; // Used to store two ends of second pipe

    char fixed_str[] = "forgeeks.org";
    char input_str[100];
    pid_t p;

    if (pipe(fd1) == -1) {
        fprintf(stderr, "Pipe Failed");
        return 1;
    }
    if (pipe(fd2) == -1) {
        fprintf(stderr, "Pipe Failed");
        return 1;
    }

    scanf("%s", input_str);
    p = fork();

    if (p < 0) {
        fprintf(stderr, "fork Failed");
        return 1;
    }

    // Parent process
    else if (p > 0) {
        char concat_str[100];

        close(fd1[0]); // Close reading end of first pipe

        // Write input string and close writing end of first
        // pipe.
        write(fd1[1], input_str, strlen(input_str) + 1);
        close(fd1[1]);

        // Wait for child to send a string
        wait(NULL);

        close(fd2[1]); // Close writing end of second pipe

        // Read string from child, print it and close
        // reading end.
        read(fd2[0], concat_str, 100);
        printf("Concatenated string %s\n", concat_str);
        close(fd2[0]);
    }

    // child process
    else {
        close(fd1[1]); // Close writing end of first pipe

        // Read a string using first pipe
        char concat_str[100];
        read(fd1[0], concat_str, 100);

        // Concatenate a fixed string with it
        int k = strlen(concat_str);
        int i;
        for (i = 0; i < strlen(fixed_str); i++)
            concat_str[k++] = fixed_str[i];

        concat_str[k] = '\0'; // string ends with '\0'

        // Close both reading ends
        close(fd1[0]);
        close(fd2[0]);

        // Write concatenated string and close writing end
        write(fd2[1], concat_str, strlen(concat_str) + 1);
        close(fd2[1]);

        exit(0);
    }
}
```

#038 - fopen() fread() fwrite() Functions

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>


int main(int argc, char *argv[]) 
{
    FILE *fs;
    char buf[10];
    size_t sz;

    fs = fopen("mytext.txt", "r");

    if(fs == NULL)
    {
        perror("fopen");
        exit(1);
    }

    while (!feof(fs))
    {
        memset(buf, 0, strlen(buf));
        sz = fread((void *) buf, 9, 1, fs);
        // buf[9] = '\0';
        
        printf("%s", buf);
    }
    
    printf("\n");

    fclose(fs);

    return 0;
}
```
```output
I love t program in C.
```

#039 - mutex pthread

```c
#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>
#include <string.h>

void *myfunc1(void *ptr);
void *myfunc2(void *ptr);

pthread_mutex_t lock;
int a[100];

int main(int argc, char *argv[]) 
{

    pthread_t thrd1, thrd2;
    int thret1, thret2;
    char *msg1 = "First thread";
    char *msg2 = "Second thread";

    memset(a, 0, sizeof(a));
    
    thret1 = pthread_create(&thrd1, NULL, myfunc1, (void *)msg1);
    thret2 = pthread_create(&thrd2, NULL, myfunc2, (void *)msg2);

    pthread_join(thrd1, NULL);
    pthread_join(thrd2, NULL);

    printf("thret1 = %d\n", thret1);
    printf("thret2 = %d\n", thret2);

    return 0;
}

void *myfunc1(void *ptr)
{   
    int i;
    char *msg = (char *) ptr;
    printf("msg: %s\n", msg);

    pthread_mutex_lock(&lock);
    for (i=0; i<100; i++)
    {
        printf("X");
        a[i] = i;
    }
    pthread_mutex_unlock(&lock);
}

void *myfunc2(void *ptr)
{   
    int i;
    char *msg = (char *) ptr;
    printf("msg: %s\n", msg);

    pthread_mutex_lock(&lock);
    for (i=0; i<100; i++)
    {
        printf("%d, ", a[i]);
    }
    pthread_mutex_unlock(&lock);
}
```
```sh
gcc -pthread -o main main.c
```
```output
msg: First thread
XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXmsg: Second thread
XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61, 62, 63, 64, 65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78, 79, 80, 81, 82, 83, 84, 85, 86, 87, 88, 89, 90, 91, 92, 93, 94, 95, 96, 97, 98, 99, thret1 = 0
thret2 = 0
```

***Thread synchronization** is defined as a mechanism which ensures that two or more concurrent processes or threads do not simultaneously execute some particular program segment known as a critical section. Processes’ access to critical section is controlled by using synchronization techniques. When one thread starts executing the critical section (a serialized segment of the program) the other thread should wait until the first thread finishes. If proper synchronization techniques are not applied, it may cause a race condition where the values of variables may be unpredictable and vary depending on the timings of context switches of the processes or threads.*


**Thread Synchronization Problems**
```c
#include <pthread.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>

pthread_t tid[2];
int counter;

void* trythis(void* arg)
{
    unsigned long i = 0;
    counter += 1;
    printf("\n Job %d has started\n", counter);

    for (i = 0; i < (0xFFFFFFFF); i++)
        ;
    printf("\n Job %d has finished\n", counter);

    return NULL;
}

int main(void)
{
    int i = 0;
    int error;

    while (i < 2) {
        error = pthread_create(&(tid[i]), NULL, &trythis, NULL);
        if (error != 0)
            printf("\nThread can't be created : [%s]", strerror(error));
        i++;
    }

    pthread_join(tid[0], NULL);
    pthread_join(tid[1], NULL);

    return 0;
}
```
```output
Job 1 has started
Job 2 has started
Job 2 has finished
Job 2 has finished
```
***Problem:** From the last two logs, one can see that the log ‘Job 2 has finished’ is repeated twice while no log for ‘Job 1 has finished’ is seen.*

**Why it has occurred ?**
*On observing closely and visualizing the execution of the code, we can see that :
- The log ‘Job 2 has started’ is printed just after ‘Job 1 has Started’ so it can easily be concluded that while thread 1 was processing the scheduler scheduled the thread 2.
- If we take the above assumption true then the value of the ‘counter’ variable got incremented again before job 1 got finished.
- So, when Job 1 actually got finished, then the wrong value of counter produced the log ‘Job 2 has finished’ followed by the ‘Job 2 has finished’ for the actual job 2 or vice versa as it is dependent on scheduler.
- So we see that its not the repetitive log but the wrong value of the ‘counter’ variable that is the problem.
- The actual problem was the usage of the variable ‘counter’ by a second thread when the first thread was using or about to use it.
- In other words, we can say that lack of synchronization between the threads while using the shared resource ‘counter’ caused the problems or in one word we can say that this problem happened due to ‘Synchronization problem’ between two threads.*

**How to solve it ?**

**Mutex**
- A Mutex is a lock that we set before using a shared resource and release after using it.
- When the lock is set, no other thread can access the locked region of code.
- So we see that even if thread 2 is scheduled while thread 1 was not done accessing the shared resource and the code is locked by thread 1 using mutexes then thread 2 cannot even access that region of code.
- So this ensures synchronized access of shared resources in the code.

The most popular way of achieving thread synchronization is by using Mutexes.

**Working of a mutex**

1. Suppose one thread has locked a region of code using mutex and is executing that piece of code.
2. Now if scheduler decides to do a context switch, then all the other threads which are ready to execute the same region are unblocked.
3. Only one of all the threads would make it to the execution but if this thread tries to execute the same region of code that is already locked then it will again go to sleep.
4. Context switch will take place again and again but no thread would be able to execute the locked region of code until the mutex lock over it is released.
5. Mutex lock will only be released by the thread who locked it.
6. So this ensures that once a thread has locked a piece of code then no other thread can execute the same region until it is unlocked by the thread who locked it.

**A mutex is initialized and then a lock is achieved by calling the following two functions :** The first function initializes a mutex and through second function any critical region in the code can be locked.

1. **`int pthread_mutex_init(pthread_mutex_t *restrict mutex, const pthread_mutexattr_t *restrict attr)` :** Creates a mutex, referenced by mutex, with attributes specified by attr. If attr is NULL, the default mutex attribute (NONRECURSIVE) is used.
**Returned value**
If successful, pthread_mutex_init() returns 0, and the state of the mutex becomes initialized and unlocked.
If unsuccessful, pthread_mutex_init() returns -1.

2. **`int pthread_mutex_lock(pthread_mutex_t *mutex)`** : Locks a mutex object, which identifies a mutex. If the mutex is already locked by another thread, the thread waits for the mutex to become available. The thread that has locked a mutex becomes its current owner and remains the owner until the same thread has unlocked it. When the mutex has the attribute of recursive, the use of the lock may be different. When this kind of mutex is locked multiple times by the same thread, then a count is incremented and no waiting thread is posted. The owning thread must call pthread_mutex_unlock() the same number of times to decrement the count to zero.
**Returned value**
If successful, pthread_mutex_lock() returns 0.
If unsuccessful, pthread_mutex_lock() returns -1.

**The mutex can be unlocked and destroyed by calling following two functions :** The first function releases the lock and the second function destroys the lock so that it cannot be used anywhere in future.

1. **`int pthread_mutex_unlock(pthread_mutex_t *mutex)` :** Releases a mutex object. If one or more threads are waiting to lock the mutex, pthread_mutex_unlock() causes one of those threads to return from pthread_mutex_lock() with the mutex object acquired. If no threads are waiting for the mutex, the mutex unlocks with no current owner. When the mutex has the attribute of recursive the use of the lock may be different. When this kind of mutex is locked multiple times by the same thread, then unlock will decrement the count and no waiting thread is posted to continue running with the lock. If the count is decremented to zero, then the mutex is released and if any thread is waiting for it is posted.
**Returned value**
If successful, pthread_mutex_unlock() returns 0.
If unsuccessful, pthread_mutex_unlock() returns -1

2. **`int pthread_mutex_destroy(pthread_mutex_t *mutex)` :** Deletes a mutex object, which identifies a mutex. Mutexes are used to protect shared resources. mutex is set to an invalid value, but can be reinitialized using pthread_mutex_init().
Returned value
If successful, pthread_mutex_destroy() returns 0.
If unsuccessful, pthread_mutex_destroy() returns -1.

**An example to show how mutexes are used for thread synchronization**

```c
#include <pthread.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
  
pthread_t tid[2];
int counter;
pthread_mutex_t lock;
  
void* trythis(void* arg)
{
    pthread_mutex_lock(&lock);
  
    unsigned long i = 0;
    counter += 1;
    printf("\n Job %d has started\n", counter);
  
    for (i = 0; i < (0xFFFFFFFF); i++)
        ;
  
    printf("\n Job %d has finished\n", counter);
  
    pthread_mutex_unlock(&lock);
  
    return NULL;
}
  
int main(void)
{
    int i = 0;
    int error;
  
    if (pthread_mutex_init(&lock, NULL) != 0) {
        printf("\n mutex init has failed\n");
        return 1;
    }
  
    while (i < 2) {
        error = pthread_create(&(tid[i]),
                               NULL,
                               &trythis, NULL);
        if (error != 0)
            printf("\nThread can't be created :[%s]",
                   strerror(error));
        i++;
    }
  
    pthread_join(tid[0], NULL);
    pthread_join(tid[1], NULL);
    pthread_mutex_destroy(&lock);
  
    return 0;
}
```
```output
Job 1 started
Job 1 finished
Job 2 started
Job 2 finished
```

#040 - Dynamic Shared Libraries

*add.c*
```c
#include <stdio.h>

int addnumbers(int a, int b)
{
    int sum;
    sum = a + b;
    return sum;
}
```
```sh
gcc -shared -o libadd.so add.c
file libadd.so
`=>
libadd.so: ELF 64-bit LSB shared object, x86-64, version 1 (SYSV), dynamically linked, BuildID[sha1]=25d4d164ba1b70c5387d8da4817f0aeb8e74b205, not stripped
```

*main.c*
```c
#include <stdio.h>

int main(int argc, char *argv[]) 
{

    int total;
    total = addnumers(6, 7);

    printf("total = %d\n", total);

    return 0;
}
```

```sh
gcc -o main main.c -L. -ladd
./main
`=>
./main: error while loading shared libraries: libadd.so: cannot open shared object file: No such file or directory
```

```sh
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH
```
=>
```sh
export LD_LIBRARY_PATH=.
./main 
`=>
total = 13
```

```sh
ldd main
`=>
        linux-vdso.so.1 (0x00007ffe12199000)
        libadd.so => ./libadd.so (0x00007f5af475a000)
        libc.so.6 => /lib/x86_64-linux-gnu/libc.so.6 (0x00007f5af4556000)
        /lib64/ld-linux-x86-64.so.2 (0x00007f5af4766000)
```

- The file VDSO is fast implementation of system call interface and some other stuff, it is not our focus (on some older systems you may see different file name in liue of *.vsdo.*). Ignore this file. We have interest in the other two files. 

-The file libc.so.6 is C implementation of various standard functions. It is the file where we see printf definition needed for our printing. It is the shared library needed to be loaded into memory to run our main program. 

- The file /lib64/ld-linux-x86-64.so.2 is infact an executable that runs when an application is invoked. When we invoke the program on bash terminal, typically the bash forks itself and replaces its address space with image of program to run (so called fork-exec pair). The kernel verifies whether the libc.so.6 resides in the memory. If not, it will load the file into memory and does the relocation of libc.so.6 symbols. It then invokes the dynamic linker (/lib64/ld-linux-x86-64.so.2) to resolve unresolved symbols of application code (printf in the present case). Then the control transfers to our program main. (I have intentionally omitted many details in the process, our focus is to understand basic details). 

#041 - Static Shared Libraries

```sh
gcc -c add.c
ls
`=>
add.c add.o libadd.so ...
```

```sh
ar -cvq libadd.a add.o
`=>
a - add.o
```
```sh
ls
`=>
add.c add.o libadd.a libadd.so ...
```

```sh
 nm libadd.a
`=>
add.o:
0000000000000000 T addnumbers
```

```sh
ranlib libadd.a
```
```sh
gcc -o main main.c libadd.a
./main 
`=>
total = 13
```

```sh
ldd main
`=>
        linux-vdso.so.1 (0x00007ffe759a6000)
        libc.so.6 => /lib/x86_64-linux-gnu/libc.so.6 (0x00007f81059d6000)
        /lib64/ld-linux-x86-64.so.2 (0x00007f8105be1000)
```
```sh
nm main
`=>
000000000000118b T addnumbers
0000000000004010 B __bss_start
0000000000004010 b completed.8060
                 w __cxa_finalize@@GLIBC_2.2.5
0000000000004000 D __data_start
0000000000004000 W data_start
0000000000001090 t deregister_tm_clones
0000000000001100 t __do_global_dtors_aux
0000000000003dc0 d __do_global_dtors_aux_fini_array_entry
0000000000004008 D __dso_handle
0000000000003dc8 d _DYNAMIC
0000000000004010 D _edata
0000000000004018 B _end
0000000000001228 T _fini
0000000000001140 t frame_dummy
0000000000003db8 d __frame_dummy_init_array_entry
0000000000002184 r __FRAME_END__
0000000000003fb8 d _GLOBAL_OFFSET_TABLE_
                 w __gmon_start__
0000000000002010 r __GNU_EH_FRAME_HDR
0000000000001000 t _init
0000000000003dc0 d __init_array_end
0000000000003db8 d __init_array_start
0000000000002000 R _IO_stdin_used
                 w _ITM_deregisterTMCloneTable
                 w _ITM_registerTMCloneTable
0000000000001220 T __libc_csu_fini
00000000000011b0 T __libc_csu_init
                 U __libc_start_main@@GLIBC_2.2.5
0000000000001149 T main
                 U printf@@GLIBC_2.2.5
00000000000010c0 t register_tm_clones
0000000000001060 T _start
0000000000004010 D __TMC_END__
```
https://www.geeksforgeeks.org/working-with-shared-libraries-set-1/?ref=gcse
https://www.geeksforgeeks.org/working-with-shared-libraries-set-2/

#042 - Static Variables

*main.c*
```c
#include <stdio.h>

int num;
int myfunc();

int main(int argc, char *argv[]) 
{   
    num = 6;
    myfunc();
    return 0;
}
```

*static_var.c*
```c
#include <stdio.h>

extern int num;

int myfunc() 
{
    printf("extern num = %d\n", num);
    return 0;
}
```

```sh
gcc -o main main.c static_var.c
```
```output
extern num = 6
```

```c
static int num
```
*=> will make the varibale num as private of the source file of main.c.*

```c
#include <stdio.h>

int myfunc()
{
    int i = 0;
    i += 2;
    printf("i = %d\n", i);
    i += 2;
    printf("i = %d\n", i);
    return 0;
}

int main(int argc, char *argv[]) 
{   
    myfunc();
    myfunc();
    return 0;
}
```
```output
i = 2
i = 4
i = 2
i = 4
```

```c
#include <stdio.h>

int myfunc()
{
    static int i = 0;
    i += 2;
    printf("i = %d\n", i);
    i += 2;
    printf("i = %d\n", i);
    return 0;
}

int main(int argc, char *argv[]) 
{   
    myfunc();
    myfunc();
    return 0;
}
```
```output
i = 2
i = 4
i = 6
i = 8
```

*Following are some interesting facts about static variables in C.
1) A static int variable remains in memory while the program is running. A normal or auto variable is destroyed when a function call where the variable was declared is over. 
2) Static variables are allocated memory in data segment, not stack segment. 
3) Static variables (like global variables) are initialized as 0 if not initialized explicitly.
4) In C, static variables can only be initialized using constant literals. For example, following program fails in compilation.
```c
#include<stdio.h>
int initializer(void)
{
    return 50;
}
  
int main()
{
    static int i = initializer();
    printf(" value of i = %d", i);
    getchar();
    return 0;
}
```
```output
In function 'main':
9:5: error: initializer element is not constant
     static int i = initializer();
     ^
```
5) Static global variables and functions are also possible in C/C++. The purpose of these is to limit scope of a variable or function to a file. 
6) Static variables should not be declared inside structure. The reason is C compiler requires the entire structure elements to be placed together (i.e.) memory allocation for structure members should be contiguous. It is possible to declare structure inside the function (stack segment) or allocate memory dynamically(heap segment) or it can be even global (BSS or data segment). Whatever might be the case, all structure members should reside in the same memory segment because the value for the structure element is fetched by counting the offset of the element from the beginning address of the structure. Separating out one member alone to data segment defeats the purpose of static variable and it is possible to have an entire structure as static.*

https://www.geeksforgeeks.org/memory-layout-of-c-program/


#043 - String to Integer Conversion

```c
#include <stdio.h>
#include <stdlib.h>

int main(int argc, char *argv[]) 
{   
    char *strint = "5782";
    char *strdbl = "5927.4578";

    int a;
    double b;

    a = atoi(strint);
    b = atof(strdbl);

    printf("a = %d\n", a);
    printf("b = %f\n", b);

    return 0;
}
```
```output
a = 5782
b = 5927.457800
```

#044 - Time Functions

## 44.1 Basic Usage
```c
#include <stdio.h>
#include <time.h>

int main(int argc, char *argv[]) 
{   

    time_t mytime;
    struct tm *mytm;
    mytime = time(NULL);

    printf("%s\n", ctime(&mytime));

    mytm = localtime(&mytime);
    printf("%s\n", asctime(mytm));
    printf("Year: %d\n", 1900 + mytm->tm_year);
    printf("Month: %d\n", 1 + mytm->tm_mon);
    printf("Day of Month: %d\n", mytm->tm_mday);
    printf("DST: %d\n", mytm->tm_isdst);

    return 0;
}
```
```output
Wed Jan 12 13:23:13 2022

Wed Jan 12 13:23:13 2022

Year: 2021
Month: 12
Day of Month: 24
DST: 0
```

## 44.2 How to measure time taken by a function in C
*To calculate time taken by a process, we can use clock() function which is available time.h. We can call the clock function at the beginning and end of the code for which we measure time, subtract the values, and then divide by CLOCKS_PER_SEC (the number of clock ticks per second) to get processor time, like following.*
```c
     #include <time.h>
     
     clock_t start, end;
     double cpu_time_used;
     
     start = clock();
     ... /* Do the work. */
     end = clock();
     cpu_time_used = ((double) (end - start)) / CLOCKS_PER_SEC;
```

#045 - toupper() tolower() Functions

```c
#include <stdio.h>
#include <ctype.h>

int main(int argc, char *argv[]) 
{   
    char mystr[] = "Hello World!";
    char *p;
    int i;

    printf("%s\n", mystr);

    p = mystr;
    while (*p != '\0')
    {
        *p = (char) toupper((char) *p);
        p++;
    }
    printf("%s\n", mystr);

    i = 0;
    while (mystr[i] != '\0')
    {
        mystr[i] = (char) tolower((char) mystr[i]);
        i++;
    }
    printf("%s\n", mystr);

    return 0;
}
```
```output
Hello World!
HELLO WORLD!
hello world!
```

#046 - Semaphore pthread

```c
#include <stdio.h>
#include <pthread.h>
#include <semaphore.h>

void *myfunc1(void *ptr);
void *myfunc2(void *ptr);

char buf[24]; // 24 bytes
sem_t mutex;

int main(int argc, char *argv[]) 
{

    pthread_t thread1;
    pthread_t thread2;
    char *msg1 = "Thread 1";
    char *msg2 = "Thread 2";

    sem_init(&mutex, 0, 1);
    pthread_create(&thread1, NULL, (void *) myfunc1, (void *)msg1);
    pthread_create(&thread2, NULL, (void *) myfunc2, (void *)msg2);

    pthread_join(thread1, NULL);
    pthread_join(thread2, NULL);

    sem_destroy(&mutex);

    return 0;
}

void *myfunc1(void *ptr)
{   

    char *msg = (char *) ptr;
    printf("msg: %s\n", msg);
    sem_wait(&mutex);
    printf("Writing buf...\n");
    sprintf(buf, "%s", "Hello there!");
    sem_post(&mutex);
    pthread_exit(0);
}

void *myfunc2(void *ptr)
{   
    char *msg = (char *) ptr;
    printf("msg: %s\n", msg);
    sem_wait(&mutex);
    printf("Reading buf...\n");
    printf("%s\n", buf);
    sem_post(&mutex);
    pthread_exit(0);
}
```
```output
msg: Thread 1
Writing buf...
msg: Thread 2
Reading buf...
Hello there!
```

*A mutex is a **locking mechanism** used to synchronize access to a resource. Only one task (can be a thread or process based on OS abstraction) can acquire the mutex. It means there is ownership associated with a mutex, and only the owner can release the lock (mutex).* 

*Semaphore is **signaling mechanism** (“I am done, you can carry on” kind of signal). For example, if you are listening to songs (assume it as one task) on your mobile phone and at the same time, your friend calls you, an interrupt is triggered upon which an interrupt service routine (ISR) signals the call processing task to wakeup.* 

*Semaphore was proposed by Dijkstra in 1965 which is a very significant technique to manage concurrent processes by using a simple integer value, which is known as a semaphore. Semaphore is simply an integer variable that is shared between threads. This variable is used to solve the critical section problem and to achieve process synchronization in the multiprocessing environment. 
Semaphores are of two types:*

1. **Binary Semaphore** – 
    *This is also known as mutex lock. It can have only two values – 0 and 1. Its value is initialized to 1. It is used to implement the solution of critical section problems with multiple processes.*
2. **Counting Semaphore** – 
    *Its value can range over an unrestricted domain. It is used to control access to a resource that has multiple instances.*

*First, look at two operations that can be used to access and change the value of the semaphore variable.*

```c
P(Semaphore s) {
    // Note that there is semicolon after while.
    // The code gets stuck here while s is 0.
    while(s == 0); /* wait until s=0 */
}

V(Semaphore s) {
    s = s+1;
}
```

***Some point regarding P and V operation:***

1. *P operation is also called wait, sleep, or down operation, and V operation is also called signal, wake-up, or up operation.*

2. *Both operations are atomic and semaphore(s) is always initialized to one. Here atomic means that variable on which read, modify and update happens at the same time/moment with no pre-emption i.e. in-between read, modify and update no other operation is performed that may change the variable.*

3. *A critical section is surrounded by both operations to implement process synchronization. See the below image. The critical section of Process P is in between P and V operation.*

```c
// Process P
    // Some code
    P(s);
    // Critical section
    V(s);
    // Remainder section
```


```state_1
process_1 -> Executing in non-critical section
s=1
process_2 -> Executing in non-critical section
```

```state_2
process_1 -> Executing critical section updates s=0
s=0
process_2 -> Executing in non-critical section
```

```state_3
process_1 -> Executing critical section updates s=0
s=0
process_2 -> Wants to enter critical section but can't as s = 0
```

```state_4
process_1 -> Exits critical section and updates s=1
s=1
process_2 -> Enters critical section as s=1 and updates s=0
```

#047 - system() Function

```c
#include <stdio.h>
#include <stdlib.h>

int main(int argc, char *argv[]) 
{
    int ret;
    printf("Call system...\n");
    
    ret = system("ls -l");

    printf("Existing system... ret = %d\n", ret);

    return 0;
}
```
```output
Call system...
total 112
-rw-rw-r-- 1 lawjune lawjune    98 12月 23 07:28 add.c
-rw-rw-r-- 1 lawjune lawjune  1392 12月 23 07:41 add.o
-rwxrwxr-x 1 lawjune lawjune 16872 12月 21 07:38 client
-rw-rw-r-- 1 lawjune lawjune   596 12月 21 07:36 client.c
-rw-rw-r-- 1 lawjune lawjune  1540 12月 23 07:45 libadd.a
-rwxrwxr-x 1 lawjune lawjune 15640 12月 23 07:29 libadd.so
-rwxrwxr-x 1 lawjune lawjune 16784 12月 28 07:31 main
-rw-rw-r-- 1 lawjune lawjune   221 12月 28 07:30 main.c
-rw-rw-r-- 1 lawjune lawjune  3024 12月 17 07:48 main.o
-rw-rw-r-- 1 lawjune lawjune    22 12月 22 07:31 mytext.txt
-rwxrwxr-x 1 lawjune lawjune 16912 12月 21 07:37 server
-rw-rw-r-- 1 lawjune lawjune   633 12月 21 07:39 server.c
-rw-rw-r-- 1 lawjune lawjune   106 12月 24 07:24 static_var.c
Existing system... ret = 0
```

#048 - setenv() Function

*main.c*
```c
#include <stdio.h>
#include <stdlib.h>

int main(int argc, char *argv[]) 
{
    char *p;

    p = getenv("MYENV");

    printf("p = %s\n", p);

    return 0;
}
```
*myenv.c*
```c
#include <stdio.h>
#include <stdlib.h>

int main(int agrc, char *argv[])
{
    int ret;

    ret = 0

    ret = system("./main");
    perror("system");
    printf("ret = %d\n", ret);

    return 0;
}
```
```output
p = (null)
system: Success
ret = 0
```
=>
```c
#include <stdio.h>
#include <stdlib.h>

int main(int agrc, char *argv[])
{
    int ret;

    ret = putenv("MYENV=hello");
    if(ret == -1)
    {
        perror("putenv");
        printf("ret = %d\n", ret);
    }

    ret = system("./main");
    perror("system");
    printf("ret = %d\n", ret);

    return 0;
}
```
```output
p = hello
system: Success
ret = 0
```
=> Same result.
```c
#include <stdio.h>
#include <stdlib.h>

int main(int agrc, char *argv[])
{
    int ret;

    // ret = putenv("MYENV=hello");
    ret = setenv("MYENV", "hello", 0);
    if(ret == -1)
    {
        perror("putenv");
        printf("ret = %d\n", ret);
    }

    ret = system("./main");
    perror("system");
    printf("ret = %d\n", ret);

    return 0;
}
```
```sh
export MYENV=nice
./main
`=>
p = nice
```
```sh
unset MYENV
./main
`=>
p = (null)
```

#049 - Bit Shift Operation

```c
#include <stdio.h>

int main(int agrc, char *argv[])
{
    char bits;
    bits = 1;
    printf("%d\n", bits);
    bits = bits << 1;
    printf("%d\n", bits);

    return 0;
}
```
```output
1
2
```
```c
#include <stdio.h>

int main(int agrc, char *argv[])
{
    char bits;
    bits = 16;
    printf("%d\n", bits);
    bits = bits >> 1;
    printf("%d\n", bits);

    return 0;
}
```
```output
16
4
```
```output >>
7
3
```

#050 - Macro Functions

```c
#include <stdio.h>

#define addnum(x, y) x+y

int sumnum(int x, int y)
{
    int total;
    total = x + y;
    return total;
}

int main(int agrc, char *argv[])
{
    int a, b;
    int sum;

    a = 3;
    b = 4;

    sum = addnum(a, b);
    printf("sum = %d\n", sum);

    sum = sumnum(a, b);
    printf("sum = %d\n", sum);

    return 0;
}
```
```output
sum = 7
sum = 7
```
```sh
gcc -E main.c
`=>
...
...
...

# 5 "main.c"
int sumnum(int x, int y)
{
    int total;
    total = x + y;
    return total;
}

int main(int agrc, char *argv[])
{
    int a, b;
    int sum;

    a = 3;
    b = 4;

    sum = a+b;
    printf("sum = %d\n", sum);

    sum = sumnum(a, b);
    printf("sum = %d\n", sum);

    return 0;
}
```

# 50.1 Classic Usage - Seconds of A Year

*Essence is the `UL` unsigned long*
```c
#define SEC_YEAR  (365*24*60*60)UL
```

# 50.2 Classic Usage - Return the Less Value

```c
#define MIN(a,b)  ((a)<=(b)?(a):(b))
```

*How to eleminate the side-effenct of `least = MIN(*p++, b);`*
```c
#include <stdio.h>
#define min_i(x,y)      ((x)<=(y)?(x):(y))     
#define min_t(type,x,y) ({  type _x = x;\  
                            type _y = y;\
                            _x<_y?_x:_y;\
                        })
#define min(x,y)        ({  const typeof(x) _x = (x);\  
                            const typeof(y) _y = (y);\
                            int *__x = &_x;\
                            (void)(__x=&_y);\    
                             _x<_y?_x:_y;\  
                        })

int main()
{
    int a = 10;
    int b = 20;
    printf("min_i(a++,b++)=%d\n",min_i(a++,b++));  //11
    printf("a=%d\n",a);  //12
    printf("b=%d\n",b);  //21

    a=10;
    b=20;
    printf("min_t(int,a++,b++)=%d\n",min_t(int,a++,b++));  //10
    printf("a=%d\n",a);  //11
    printf("b=%d\n",b);  //21

    a=10;
    b=20;
    printf("min(a++,b++)=%d\n",min(a++,b++));  //10
    printf("a=%d\n",a);  //11
    printf("b=%d\n",b);  //21
  
}
```
```output
min_i(a++,b++)=11
a=12
b=21
min_t(int,a++,b++)=10
a=11
b=21
min(a++,b++)=10
a=11
b=21
```

# 50.3 Classic Usage - #error

```c
#ifdef XXX
...
#error "XXX has been defined"
#else

#endif
```

#051 - Double Pointer

```c
#include <stdio.h>

void swapptr(int **a, int **b)
{
    int *tmp;
    tmp = *a;
    *a = *b;
    *b = tmp;
}

int main(int agrc, char *argv[])
{
    int x, y;
    int *m, *n;

    x = 6;
    y = 7;

    m = &x;
    n = &y;
    
    printf("&x = %x\n", &x);
    printf("&y = %x\n", &y);
    printf("*m = %d\n", *m);
    printf("*n = %d\n", *n);
    printf("m = %x\n", m);
    printf("n = %x\n", n);
    printf("SWapping\n");

    swapptr(&m, &n);

    printf("*m = %d\n", *m);
    printf("*n = %d\n", *n);
    printf("m = %x\n", m);
    printf("n = %x\n", n);
    printf("x = %d\n", x);
    printf("y = %d\n", y);
    printf("&x = %x\n", &x);
    printf("&y = %x\n", &y);

    return 0;
}
```
```output
&x = 124a81c0
&y = 124a81c4
*m = 6
*n = 7
m = 124a81c0
n = 124a81c4
SWapping
*m = 7
*n = 6
m = 124a81c4
n = 124a81c0
x = 6
y = 7
&x = 124a81c0
&y = 124a81c4
```

#052 - Two Dimensional Array Variable

```c
#include <stdio.h>

int main(int argc, char *argv[]) 
{
    int a[3][3] = { {11, 12, 13},
                    {21, 22, 23},
                    {31, 32, 33} };
    
    int i, j;

    for (i = 0; i < 3; i++) {
        for (j = 0; j < 3; j++) {
            printf("a[%d][%d] = %d\n", i, j, a[i][j]);
        }
    }

    return 0;
}
```
```output
a[0][0] = 11
a[0][1] = 12
a[0][2] = 13
a[1][0] = 21
a[1][1] = 22
a[1][2] = 23
a[2][0] = 31
a[2][1] = 32
a[2][2] = 33
```

#053 - Scope

#054 - Enum Type

```c
#include <stdio.h>

enum day {
    Sunday = 10,
    Monday,
    Tuesday,
    Wednesday,
    Thursday,
    Friday,
    Saturday
};

int main(int argc, char *argv[]) 
{
    enum day myday;

    printf("Sunday = %d\n", Sunday);
    printf("Monday = %d\n", Monday);
    printf("Tuesday = %d\n", Tuesday);
    printf("Wednesday = %d\n", Wednesday);
    printf("Thursday = %d\n", Thursday);
    printf("Friday = %d\n", Friday);
    printf("Saturday = %d\n", Saturday);
    printf("\n");
    
    myday = Wednesday;
    printf("myday = %d\n", myday);

    return 0;
}
```
```output
Sunday = 10
Monday = 11
Tuesday = 12
Wednesday = 13
Thursday = 14
Friday = 15
Saturday = 16

myday = 13
```

**Interesting facts about initialization of enum.**

1. *Two enum names can have same value. For example, in the following C program both ‘Failed’ and ‘Freezed’ have same value 0.*

```c
enum State {Working = 1, Failed = 0, Freezed = 0};
  
int main()
{
   printf("%d, %d, %d", Working, Failed, Freezed);
   return 0;
}
```
```output
1, 0, 0
```

2. *If we do not explicitly assign values to enum names, the compiler by default assigns values starting from 0. For example, in the following C program, sunday gets value 0, monday gets 1, and so on.*

```c
#include <stdio.h>
enum day {sunday, monday, tuesday, wednesday, thursday, friday, saturday};
  
int main()
{
    enum day d = thursday;
    printf("The day number stored in d is %d", d);
    return 0;
}
```
```output
4
```

3. *We can assign values to some name in any order. All unassigned names get value as value of previous name plus one.*

```c
#include <stdio.h>
enum day {sunday = 1, monday, tuesday = 5,
          wednesday, thursday = 10, friday, saturday};
  
int main()
{
    printf("%d %d %d %d %d %d %d", sunday, monday, tuesday,
            wednesday, thursday, friday, saturday);
    return 0;
}
```
```output
1 2 5 6 10 11 12
```

4. *The value assigned to enum names must be some integral constant, i.e., the value must be in range from minimum possible integer value to maximum possible integer value.*

5. All enum constants must be unique in their scope. For example, the following program fails in compilation.

#055 - Signals

```c
#include <stdio.h>
#include <signal.h>

void myhandle(int mysignal)
{
    printf("myhandle with signal %d\n", mysignal);
}

int main(int argc, char *argv[]) 
{
    int i = 0;
    signal(SIGTERM, myhandle);

    while(1) {
        printf("i = %d\n", i);
        i++;
        sleep(1);
    }

    return 0;
}
```
```sh
ps -aux | grep main
`=>
...
...
lawjune   211005  0.0  0.0   2496   588 pts/3    S+   07:52   0:00 ./main
lawjune   214393  0.0  0.0  12116  2796 pts/1    S+   07:56   0:00 grep --color=auto main
```
```sh
kill -15 211005
kill -15 211005
```
```output
...
...
i = 32
i = 33
myhandle with signal 15
i = 34
i = 35
i = 36
i = 37
i = 38
i = 39
i = 40
i = 41
myhandle with signal 15
i = 42
i = 43
i = 44
...
...
```
*In this post, the communication between child and parent processes is done using kill() and signal(), fork() system call.*

- *fork() creates the child process from the parent. The pid can be checked to decide whether it is the child (if pid == 0) or the parent (pid = child process id).*
- *The parent can then send messages to child using the pid and kill().*
- *The child picks up these signals with signal() and calls appropriate functions.*
```c
// C program to implement sighup(), sigint()
// and sigquit() signal functions
#include <signal.h>
#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <unistd.h>
  
// function declaration
void sighup();
void sigint();
void sigquit();
  
// driver code
void main()
{
    int pid;
  
    /* get child process */
    if ((pid = fork()) < 0) {
        perror("fork");
        exit(1);
    }
  
    if (pid == 0) { /* child */
        signal(SIGHUP, sighup);
        signal(SIGINT, sigint);
        signal(SIGQUIT, sigquit);
        for (;;)
            ; /* loop for ever */
    }
  
    else /* parent */
    { /* pid hold id of child */
        printf("\nPARENT: sending SIGHUP\n\n");
        kill(pid, SIGHUP);
  
        sleep(3); /* pause for 3 secs */
        printf("\nPARENT: sending SIGINT\n\n");
        kill(pid, SIGINT);
  
        sleep(3); /* pause for 3 secs */
        printf("\nPARENT: sending SIGQUIT\n\n");
        kill(pid, SIGQUIT);
        sleep(3);
    }
}
  
// sighup() function definition
void sighup()
  
{
    signal(SIGHUP, sighup); /* reset signal */
    printf("CHILD: I have received a SIGHUP\n");
}
  
// sigint() function definition
void sigint()
  
{
    signal(SIGINT, sigint); /* reset signal */
    printf("CHILD: I have received a SIGINT\n");
}
  
// sigquit() function definition
void sigquit()
{
    printf("My DADDY has Killed me!!!\n");
    exit(0);
}
```
```output

PARENT: sending SIGHUP

CHILD: I have received a SIGHUP

PARENT: sending SIGINT

CHILD: I have received a SIGINT

PARENT: sending SIGQUIT

My DADDY has Killed me!!!
```

#056 - GDB debugger (1/2)

```c
#include <stdio.h>

int main(int argc, char *argv[]) 
{
    int i;
    char *day[7] = {
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thursday",
        "Friday",
        "Saturday",
        "Sunday"
    };

    // Introduce a bug with 10 
    for (i = 0; i < 10; i++) {
        printf("day[%d] = %s\n", i, day[i]);
    }

    return 0;
}
```
```sh
gcc -g -o main main.c
gdb main
`=>
GNU gdb (Ubuntu 9.2-0ubuntu1~20.04) 9.2
Copyright (C) 2020 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.
Type "show copying" and "show warranty" for details.
This GDB was configured as "x86_64-linux-gnu".
Type "show configuration" for configuration details.
For bug reporting instructions, please see:
<http://www.gnu.org/software/gdb/bugs/>.
Find the GDB manual and other documentation resources online at:
    <http://www.gnu.org/software/gdb/documentation/>.

For help, type "help".
Type "apropos word" to search for commands related to "word"...
Reading symbols from main...
(gdb) run
Starting program: /home/lawjune/Projects/justc/main 
day[0] = Monday
day[1] = Tuesday
day[2] = Wednesday
day[3] = Thursday
day[4] = Friday
day[5] = Saturday
day[6] = Sunday

Program received signal SIGSEGV, Segmentation fault.
__strlen_sse2 () at ../sysdeps/x86_64/multiarch/../strlen.S:120
120 ../sysdeps/x86_64/multiarch/../strlen.S: No such file or directory.
(gdb) where
#0  __strlen_sse2 () at ../sysdeps/x86_64/multiarch/../strlen.S:120
#1  0x00007ffff7e3ae95 in __vfprintf_internal (s=0x7ffff7fab6a0 <_IO_2_1_stdout_>, 
    format=0x55555555603d "day[%d] = %s\n", ap=ap@entry=0x7fffffffdba0, mode_flags=mode_flags@entry=0)
    at vfprintf-internal.c:1688
#2  0x00007ffff7e23ebf in __printf (format=<optimized out>) at printf.c:33
#3  0x0000555555555201 in main (argc=1, argv=0x7fffffffddd8) at main.c:18
(gdb) up
#1  0x00007ffff7e3ae95 in __vfprintf_internal (s=0x7ffff7fab6a0 <_IO_2_1_stdout_>, 
    format=0x55555555603d "day[%d] = %s\n", ap=ap@entry=0x7fffffffdba0, mode_flags=mode_flags@entry=0)
    at vfprintf-internal.c:1688
1688    vfprintf-internal.c: No such file or directory.
(gdb) up
#2  0x00007ffff7e23ebf in __printf (format=<optimized out>) at printf.c:33
33  printf.c: No such file or directory.
(gdb) list
28  in printf.c
(gdb) up
#3  0x0000555555555201 in main (argc=1, argv=0x7fffffffddd8) at main.c:18
18          printf("day[%d] = %s\n", i, day[i]);
(gdb) list
13          "Sunday"
14      };
15  
16      // Introduce a bug with 10 
17      for (i = 0; i < 10; i++) {
18          printf("day[%d] = %s\n", i, day[i]);
19      }
20  
21      return 0;
22  }
(gdb) print i
$1 = 7
(gdb) print day[i]
$2 = 0xe6e3b345c63f0200 <error: Cannot access memory at address 0xe6e3b345c63f0200>
(gdb) 
```

#057 - GDB debugger (2/2)

```c
#include <stdio.h>

int addnum(int a, int b)
{
    int total;
    total = a + b;
    return total;
}

int main(int argc, char *argv[])
{
    int a, b;
    int sum;

    a = 4;
    b = 7;

    sum = addnum(a, b);
    printf("sum = %d\n", sum);
    return 0;
}
```

```sh
gcc -g -o main main.c
gdb main
`=>
GNU gdb (Ubuntu 9.2-0ubuntu1~20.04) 9.2
Copyright (C) 2020 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.
Type "show copying" and "show warranty" for details.
This GDB was configured as "x86_64-linux-gnu".
Type "show configuration" for configuration details.
For bug reporting instructions, please see:
<http://www.gnu.org/software/gdb/bugs/>.
Find the GDB manual and other documentation resources online at:
    <http://www.gnu.org/software/gdb/documentation/>.

For help, type "help".
Type "apropos word" to search for commands related to "word"...
Reading symbols from main...
(gdb) b 16
Breakpoint 1 at 0x1181: file main.c, line 16.
(gdb) run
Starting program: /home/lawjune/Projects/justc/main 

Breakpoint 1, main (argc=1, argv=0x7fffffffdd88) at main.c:16
16      b = 7;
(gdb) list
11  {
12      int a, b;
13      int sum;
14  
15      a = 4;
16      b = 7;
17  
18      sum = addnum(a, b);
19      printf("sum = %d\n", sum);
20      return 0;
(gdb) print a
$1 = 4
(gdb) print b
$2 = 0
(gdb) next
18      sum = addnum(a, b);
(gdb) print b
$3 = 7
(gdb) step
addnum (a=32767, b=-9097) at main.c:4
4   {
(gdb) print a
$4 = 32767
(gdb) print b
$5 = -9097
(gdb) next
6       total = a + b;
(gdb) step
7       return total;
(gdb) print a
$6 = 4
(gdb) print b
$7 = 7
(gdb) print total
$8 = 11
(gdb) print sum
No symbol "sum" in current context.
(gdb) next
8   }
(gdb) next
main (argc=1, argv=0x7fffffffdd88) at main.c:19
19      printf("sum = %d\n", sum);
(gdb) print sum
$9 = 11
(gdb) next
sum = 11
20      return 0;
(gdb) next
21  }
(gdb) next
__libc_start_main (main=0x555555555167 <main>, argc=1, argv=0x7fffffffdd88, 
    init=<optimized out>, fini=<optimized out>, rtld_fini=<optimized out>, 
    stack_end=0x7fffffffdd78) at ../csu/libc-start.c:342
342 ../csu/libc-start.c: No such file or directory.
(gdb) next
[Inferior 1 (process 6078) exited normally]
(gdb) run
Starting program: /home/lawjune/Projects/justc/main 

Breakpoint 1, main (argc=1, argv=0x7fffffffdd88) at main.c:16
16      b = 7;
(gdb) next
18      sum = addnum(a, b);
(gdb) step
addnum (a=32767, b=-9097) at main.c:4
4   {
(gdb) fin
Run till exit from #0  addnum (a=32767, b=-9097) at main.c:4
0x0000555555555197 in main (argc=1, argv=0x7fffffffdd88) at main.c:18
18      sum = addnum(a, b);
Value returned is $10 = 11
(gdb) print sum
$11 = 0
(gdb) next
19      printf("sum = %d\n", sum);
(gdb) print sum
$12 = 11
(gdb) cont
Continuing.
sum = 11
[Inferior 1 (process 7664) exited normally]
(gdb) help
List of classes of commands:

aliases -- Aliases of other commands.
breakpoints -- Making program stop at certain points.
data -- Examining data.
files -- Specifying and examining files.
internals -- Maintenance commands.
obscure -- Obscure features.
running -- Running the program.
stack -- Examining the stack.
status -- Status inquiries.
support -- Support facilities.
tracepoints -- Tracing of program execution without stopping the program.
user-defined -- User-defined commands.

Type "help" followed by a class name for a list of commands in that class.
Type "help all" for the list of all commands.
Type "help" followed by command name for full documentation.
Type "apropos word" to search for commands related to "word".
Type "apropos -v word" for full documentation of commands related to "word".
Command name abbreviations are allowed if unambiguous.
(gdb) helo running
Undefined command: "helo".  Try "help".
(gdb) help running
Running the program.

List of commands:

advance -- Continue the program up to the given location (same form as args for break command).
attach -- Attach to a process or file outside of GDB.
continue -- Continue program being debugged, after signal or breakpoint.
detach -- Detach a process or file previously attached.
detach checkpoint -- Detach from a checkpoint (experimental).
detach inferiors -- Detach from inferior ID (or list of IDS).
disconnect -- Disconnect from a target.
finish -- Execute until selected stack frame returns.
handle -- Specify how to handle signals.
inferior -- Use this command to switch between inferiors.
interrupt -- Interrupt the execution of the debugged program.
jump -- Continue program being debugged at specified line or address.
kill -- Kill execution of program being debugged.
kill inferiors -- Kill inferior ID (or list of IDs).
next -- Step program, proceeding through subroutine calls.
nexti -- Step one instruction, but proceed through subroutine calls.
queue-signal -- Queue a signal to be delivered to the current thread when it is resumed.
--Type <RET> for more, q to quit, c to continue without paging--q\q
Quit
(gdb) 
```

#058 - Code Optimization

https://www.rapidtables.com/code/linux/gcc/gcc-o.html

*From https://stackoverflow.com/questions/1778538/how-many-gcc-optimization-levels-are-there*
```
From the man page:

-O (Same as -O1)
-O0 (do no optimization, the default if no optimization level is specified)
-O1 (optimize minimally)
-O2 (optimize more)
-O3 (optimize even more)
-Ofast (optimize very aggressively to the point of breaking standard compliance)
-Og (Optimize debugging experience. -Og enables optimizations that do not interfere with debugging. It should be the optimization level of choice for the standard edit-compile-debug cycle, offering a reasonable level of optimization while maintaining fast compilation and a good debugging experience.)
-Os (Optimize for size. -Os enables all -O2 optimizations that do not typically increase code size. It also performs further optimizations designed to reduce code size. -Os disables the following optimization flags: -falign-functions -falign-jumps -falign-loops -falign-labels -freorder-blocks -freorder-blocks-and-partition -fprefetch-loop-arrays -ftree-vect-loop-version)
```

#059 - Code Instrumentation

```c
#include <stdio.h>

int addnum(int a, int b)
{
    int sum;

#ifdef INSTDDEBUG
    printf("Debug: Entering addnum %s %d\n", __FILE__, __LINE__);
    printf("Debug: a = %d\n", a);
    printf("Debug: b = %d\n", b);
#endif

    sum = a + b;

#ifdef INSTDDEBUG
    printf("Debug: sum = %d\n", sum);
    printf("Debug: Leaving addnum %s %d\n", __FILE__, __LINE__);
#endif

    return sum;
}

int main(int argc, char *argv[])
{
    int a, b;
    int total;

    a = 4;
    b = 7;

    total = addnum(a, b);
    printf("total = %d\n", total);
    return 0;
}
```

```sh
gcc -DINSTDDEBUG -o main main.c
./main
`=> 
Debug: Entering addnum main.c 8
Debug: a = 4
Debug: b = 7
Debug: sum = 11
Debug: Leaving addnum main.c 17
total = 11
```

#060 - (Part 1/2) getopt() Function

```c
#include <stdio.h>
#include <unistd.h>

int main(int argc, char *argv[])
{
    int c;
    int xflg = 0, yflg = 0, zflg = 0;

    while ((c = getopt(argc, argv, "x:yz:")) != -1)
    {
        switch (c)
        {
        case 'x':
            xflg = 1;
            break;
        case 'y':
            yflg = 1;
            break;
        case 'z':
            zflg = 1;
            break;
        case '?':
            if(optopt == 'x' || optopt == 'z')
                fprintf(stderr, "Option -%c needs argument\n", optopt);
            else
                fprintf(stderr, "Unknown option -%c needs argument\n", optopt);
            fprintf(stderr, "Unknown option -%c. \n", optopt);
            break;
        
        default:
            fprintf(stderr, "getopt");
            break;
        }
    }
     
    printf("xflg = %d, yflg = %d, zflg = %d\n", xflg, yflg, zflg);

    return 0;
}
```

```sh
./main -x 2 -y -z rt
`=>
xflg = 1, yflg = 1, zflg = 1
```

```sh
./main -x 2 -y -z
`=>
./main: option requires an argument -- 'z'
Option -z needs argument
Unknown option -z. 
xflg = 1, yflg = 1, zflg = 0
```

#060 - (Part 2/2) getopt() Function

```c
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>

int main(int argc, char *argv[])
{
    int c;
    int xflg = 0, yflg = 0, zflg = 0;

    while ((c = getopt(argc, argv, "x:yz:")) != -1)
    {
        switch (c)
        {
        case 'x':
            xflg = 1;
            printf("optarg = %s\n", optarg);
            printf("optarg in int = %d\n", atoi(optarg));
            break;
        case 'y':
            yflg = 1;
            printf("optarg = %s\n", optarg);
            if(optarg != NULL)
                printf("optarg in int = %d\n", atoi(optarg));
            break;
        case 'z':
            zflg = 1;
            printf("optarg = %s\n", optarg);
            printf("optarg in int = %d\n", atoi(optarg));
            break;
        case '?':
            if(optopt == 'x' || optopt == 'z')
                fprintf(stderr, "Option -%c needs argument\n", optopt);
            else
                fprintf(stderr, "Unknown option -%c needs argument\n", optopt);
            fprintf(stderr, "Unknown option -%c. \n", optopt);
            break;
        
        default:
            fprintf(stderr, "getopt");
            break;
        }
    }
     
    printf("xflg = %d, yflg = %d, zflg = %d\n", xflg, yflg, zflg);

    return 0;
}
```

```sh
./main -x 2 -y -z rt
`=>
optarg = 2
optarg in int = 2
optarg = (null)
optarg = rt
optarg in int = 0
xflg = 1, yflg = 1, zflg = 1
```

#061 - Math Library

```math
F = ma/cos(angle in radians)
```

```c
#include <stdio.h>
#include <math.h>

int main()
{
    double Force, masss, accel;
    double angle; /* in angle */

    printf("Enter mass (kg): ");
    scanf("%lf", &masss);

    printf("Enter acceleration (m/s^2): ");
    scanf("%lf", &accel);

    printf("Enter angle (degrees): ");
    scanf("%lf", &angle);

    Force = (masss * accel)/cos(angle * M_PI/180.0);
    printf("Force = %lf Newtons\n", Force);

    return 0;
}
```
```sh
gcc -o main main.c -lm
./main
`=>
Enter mass (kg): 10
Enter acceleration (m/s^2): 2
Enter angle (degrees): 30
Force = 23.094011 Newtons
```

#062 - Binary Search Tree

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct mynode_tag {
    int data;
    struct mynode_tag *left; 
    struct mynode_tag *right;
} mynode;

void insert(mynode **rt, int num)
{
    mynode *tmp;

    if(*rt == NULL) {
        tmp = (mynode *) malloc(sizeof(mynode));
        if (tmp == NULL) {
            fprintf(stderr, "Unable to allocate mynode\n");
            exit(1);
        }

        tmp->data = num;
        *rt = tmp;
    } else {
        if(num > (*rt)->data)
            insert(&(*rt)->right, num);
        else
            insert(&(*rt)->left, num);
    }
}

void print_nodes(mynode *root)
{

    if(root == NULL)
        return;

    /* Go to the left/less first */
    if(root->left != NULL)
        print_nodes(root->left);
    printf("data = %d\n", root->data);

    /* Go to the right/greater then */
    if(root->right != NULL)
        print_nodes(root->right);
}

int main(int argc, char *argv[])
{
    int numbers[14] = { 19, 6, 85, 2, 25, 90, 41, 23, 11, 7, 99, 82, 48, 32 };
    int i;
    mynode *root = NULL;

    for (i = 0; i < 14; i++) {
        insert(&root, numbers[i]);
    }

    print_nodes(root);

    return 0;
}
```
```output
data = 2
data = 6
data = 7
data = 11
data = 19
data = 23
data = 25
data = 32
data = 41
data = 48
data = 82
data = 85
data = 90
data = 99
```