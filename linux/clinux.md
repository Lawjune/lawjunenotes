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