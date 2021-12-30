
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
    printf("Year: %d\n", 1900 + mytm->tm_year);
    printf("Month: %d\n", 1 + mytm->tm_mon);
    printf("Day of Month: %d\n", mytm->tm_mday);
    printf("DST: %d\n", mytm->tm_isdst);

    return 0;
}
```
```output
Fri Dec 24 07:46:05 2021

Year: 2021
Month: 12
Day of Month: 24
DST: 0
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
    sprintf(buf, "%s", "Hello there!");
    sem_post(&mutex);
    pthread_exit(0);
}

void *myfunc2(void *ptr)
{   
    char *msg = (char *) ptr;
    printf("msg: %s\n", msg);
    sem_wait(&mutex);
    printf("%s\n", buf);
    sem_post(&mutex);
    pthread_exit(0);
}
```
```output
msg: Thread 1
msg: Thread 2
Hello there!
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