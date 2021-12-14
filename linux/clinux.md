# C Programming in Linux Tutorial

## #001 - Hello World

```c
#include <stdio.h>

int main(int argc, char *argv[]) 
{
    printf("Hello World\n");

    return 0;
}
```

## #002 - Data Types: "int" and "char"

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

## #003 - Data Types: "float", "double", and "long int"

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

## #004 - Data Types: strings

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

## #005 - Data Types: pointer

```c
#include <stdio.h>

int main(int argc, char *argv[]) 
{   
    int n;
    int *k;

    n = 25;
    k = &n;

    printf("n = %d\n", n);
    printf("k = %x\n", k);
    printf("*k = %d\n", *k);

    *k = 10;
    printf("k = %x\n", k);
    printf("*k = %d\n", *k);
    
    return 0;
}
```
```output
n = 25
k = 254b274c
*k = 25
k = 254b274c
*k = 10
```

## #006 - Data Types: Array

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

## #007 - If-Then-Else Statement

## #008 - For Loop Statement

## #009 - "while" Loop

## #010 - "struct" Statement

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

## #011 - typedef Statement

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

## #012 - Functions

## #013 - Function Pointers

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

## #014 - Adding Comments in Source Code

## #015 - argc argv

**gcc -o helloc helloc.c

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

## #016 - Multiple Source Files

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
addnum.c  addnum.o  helloworld  helloworld.c  helloworld.o
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

## #017 - String Functions and Operations

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

## #018 - Char Pointer vs Array Char

```c
#include <stdio.h>
#include <string.h>

int main(int argc, char *argv[]) 
{   
    char str[24] = "First string";
    char *ptr = "Second string";

    printf("str = %s\n", str);
    printf("ptr = %s\n", ptr);

    ptr = ptr + 1; 
    printf("ptr = %s\n", ptr);

    // We can't do that
    // str = str + 1;
    // printf("str = %s\n", str);

    return 0;
}
```
```output
str = First string
ptr = Second string
ptr = econd string
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


## #019 - Preprocessor

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

## #020 - Unary and Binary Operations

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

## #021 - Type Casting

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

## #022 - malloc() free()

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

## #023 - Creating Header File

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

## #024 - open() read() write() Functions

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

## #025 - readdir() opendir() Functions

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

## #026 - fork() Function

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

## #027 - Bubble Sort
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

## #028 - Recursion

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

## #029 - pthreads

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

## #030 - scanf() Function

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



