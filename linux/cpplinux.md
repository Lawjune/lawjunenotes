# C++ Tutorial for Beginners

## Ep#1 - Setup, Intro, & Visual Studio Code

```sh
sudo apt install build-essential
```

\*Install vscode plugins:

- C/C++ IntelliSense
- Code Runner\*

```cpp
#include <iostream>
using namespace std;

int main() {
    cout << "Hello World!";
    return 0;
}
```

https://www.onlinegdb.com/online_c++_compiler

## Ep#2 - Main() Function and Hello World!

```cpp
int main(int argc, char *argv[]) {
    return 0;
}
```

```cpp
#include <iostream>
// using namespace std;

int main() {
    std::cout << "Hello World!";
    return 0;
}
```

## Ep#3 - Basic Data Types Explained

**int
integer 1,2,3... -1,-2,-3...
4 bytes = 32 bits**

**char
character A,B,C...1,2,3...<,>,!...
1 byte = 8 bits**

**bool
boolean 0/1 True/False
1 byte = 8 bits**

**float
floating point number 1.0,2.0,-1.0,-2.0
4 bytes = 32 bits**

**double
double floating point number
8 bytes = 64 bits**

**void
valueless
2/4/8 bytes depending on the platform**

**string**

## Ep#4 - Declare and Assign Variables

```cpp
#include <iostream>
using namespace std;

int main() {

    // datatype variable_name;
    // datatype variable_name = iniital_value;

    int var1 = 1;
    float var2 = 1.0;
    char var3 = 'C';
    bool result = true;

    cout << var1 << endl << var2 << endl << var3 << endl << result << endl;

    cout << "Reassign variables..." << endl;

    var1 = 2;
    var2 = 2.4;
    var3 = 'D';
    result = false;

        cout << var1 << endl << var2 << endl << var3 << endl << result << endl;

    return 0;
}
```

## Review #1 - Character ASCII Table, Size and Limits of Data Types

https://code.visualstudio.com/docs/cpp/config-linux

```cpp
cout << sizeof(char) << " bytes"<< endl;
```

\*1 byte = 8 bits -> 2^8 = 256
256/2 = 128 -> 127 postive numbers we can fill

-

https://www.asciitable.com/

## Ep#5 - Arithmetic, Relational, Logical, and Bitwise Operators- SavvyNik

```cpp
#include <iostream>
#include <vector>
#include <string>

using namespace std;

int main()
{
    // Arithemtic
    // +, -, *, /, %, ++, --

    float value1 = 2.0;
    float value2 = 4.0;
    int value3 = 2;
    int value4 = 4;

    cout << "*****" << "Arithemtic" << "*****" << endl;
    cout << value1 + value2 << endl; // 6
    cout << value1 - value2 << endl; // -2
    cout << value1 * value2 << endl; // 8
    cout << value1 / value2 << endl; // 0.5
    cout << value3 % value4 << endl; // 2
    cout << value1++ << endl; // 2
    cout << ++value1 << endl; // 4
    cout << value2-- << endl; // 4
    cout << --value2 << endl; // 2

    // Comparison
    // <, >, >=, <=, ==, !=

    cout << "*****" << "Comparison" << "*****" << endl;
    cout << (value3 < value4) << endl; // true
    cout << (value3 > value4) << endl; // false
    cout << (value3 >= 2) << endl; // true
    cout << (value3 <= 4) << endl; // true
    cout << (value4 == 4) << endl; //true
    cout << (value4 != 4) << endl; // false

    // Logical
    // &&, ||, !

    bool result1 = true;
    bool result2 = false;
    cout << "*****" << "Logical" << "*****" << endl;
    cout << (result1 && result2) << endl; // 0
    cout << (result1 || result2) << endl; // 1
    cout << (!result2) << endl; // 0

    // Bitwise
    // bitwise &, bitwise |, <<, >>

}
```

## Ep#6 - iostream - cout, cin, cerr, clog basic input/output

_cout -> character output_

```cpp
#include <iostream>
using namespace std;

int main()
{
    int value1 = 1;
    int value2 = 2;

    cout << "JunLuo" << endl << "was here." << endl;
    cout << value1 + value2 << endl;

    cout << "Please supply two numbers:" << endl;
    cin >> value1;
    cin >> value2;
    cout << value1 + value2 << endl;

    cerr << "An error occured." << endl;
    clog << "A new log statement." << endl;

    return 0;
}
```

```sh
g++ helloworld.cpp -o iostream
```

```sh
./iostream
`=>
JunLuo
was here.
3
Please supply two numbers:
3
4
7
An error occured.
A new log statement.
```

```sh
./iostream 2> errorlog.txt
`=>
JunLuo
was here.
3
Please supply two numbers:
3
4
7
```

```sh
cat errorlog.txt
`=>
An error occured.
A new log statement.
```

## Review #2 - iostream, formatting, and more operators

https://doc.bccnsoft.com/docs/cppreference_en/io_flags.html

```cpp
#include <iostream>
using namespace std;

int main()
{
    cout.flags( ios::hex | ios::showbase | ios::boolalpha );

    int value1, value2, value3;
    cout << "Please put in 2 values" << endl;

    cin >> value1;
    cin >> value2;

    value3 = value1;
    value3 += value2;
    cout << value3 << endl;
    cout << (value3 == (value1 + value2)) << endl; // true

    return 0;
}
```

## Ep#7 - if | else | else if statements (Conditional Statements)

```cpp
#include <iostream>
using namespace std;

int main()
{
    int x;
    cin >> x;
    if (x > 0)
        cout << "x is positive";
    else if (x < 0)
        cout << "x is negative";
    else
        cout << "x is 0";

    return 0;
}
```

## Ep#8 - Constants & Literals

https://www.cplusplus.com/doc/tutorial/constants/

**#define identifier replacement**

\*After this directive, any occurrence of identifier in the code is interpreted as replacement, where replacement is any sequence of characters (until the end of the line). This replacement is performed by the preprocessor, and happens before the program is compiled, thus causing a sort of blind replacement: the validity of the types or syntax involved is not checked in any way.

-

```cpp
#include <iostream>
using namespace std;

#define PI 3.14159
#define NEWLINE '\n'

int main ()
{
  double r=5.0;               // radius
  double circle;

  circle = 2 * PI * r;
  cout << circle;
  cout << NEWLINE;

}
```

## Ep#9 - Switch Case

**SWITCH
switch (expression)
{
case constant1:
group-of-statements-1;
break;
case constant2:
group-of-statements-2;
break;
.
.
.
default:
default-group-of-statements
}
**

```cpp
#include <iostream>
using namespace std;

int main()
{
    int x;
    cin >> x;
    switch (x) {
        case 1:
        case 2:
        case 3:
            cout << "x is 1, 2 or 3";
            break;
        default:
            cout << "x is not 1, 2 nor 3";
    }

    return 0;
}
```

## Ep#10 - #define Macros and Macro Functions

**#define macro <some function/value>**

```cpp
#include <iostream>
using namespace std;

#define PI 3.14159
#define NEWLINE '\n'
#define CIRC(d) (PI*d)
#define DEBUG

int main()
{
    #ifdef DEBUG
    cout << "Please supply a diameter " << NEWLINE;
    #endif

    int d;

    cin >> d;
    cout << "PI: " << PI << NEWLINE;
    cout << CIRC(d) << NEWLINE;
    return 0;
}
```

## Review #4 for Beginners - Macros & Switch Case | Find the Perimeter Program

```cpp
#include <iostream>
using namespace std;

#define PI 3.14

#define SQUARE(s) (4*s)
#define RECT(l,w) (2*(l+w))
#define TRG(S1, s2, s3) (s1+s2+s3)
#define CIRC(r) (2*PI*r)
#define HEX(h) (6*h)

int main()
{
    cout << "Finding the Perimeter of a Shape.." << endl;

    cout << "1 - Square" << endl;
    cout << "2 - Rectangle" << endl;
    cout << "3 - Triangle" << endl;
    cout << "4 - Circle" << endl;
    cout << "5 - Hexagon" << endl;

    int selection;

    cin >> selection;

    switch (selection)
    {
    case 1:
        float s;
        cout << "Please input the length of your Square:" << endl;
        cin >> s;
        cout << "The perimeter is equal to -> " << SQUARE(s) << endl;
        break;
    case 2:
        float l, w;
        cout << "Please input the length and width of your Rectangle:" << endl;
        cin >> l >> w;
        cout << "The perimeter is equal to -> " << RECT(l,w) << endl;
        break;
    case 3:
        float s1, s2, s3;
        cout << "Please input the sides of your Triangle:" << endl;
        cin >> s1 >> s2 >> s3;
        cout << "The perimeter is equal to -> " << TRG(S1, s2, s3) << endl;
        break;
    case 4:
        float r;
        cout << "Please input the radius of your Circle:" << endl;
        cin >> r;
        cout << "The perimeter is equal to -> " << CIRC(r) << endl;
        break;
    case 5:
        float h;
        cin >> h;
        cout << "Please input the height of your Hexagon:" << endl;
        break;
        cout << "The perimeter is equal to -> " << HEX(h) << endl;
    default:
        cout << "Sorry that's not an option." << endl;
        break;
    }
}
```

## Ep#11 - For Loops

```cpp
#include <iostream>
using namespace std;

int main() {
    int num;
    cout << "Please enter in a number." << endl;
    cin >> num;
    for (int i=0; i < num; i++) {
        cout << i << endl;
    }

    return 0;
}
```

## Ep#12 - While & Do While Loops

```cpp
#include <iostream>
using namespace std;

int main() {

    bool exit = false;
    // while(exit == false) {
    //     cout << "Do you want t keep executing?" << endl;
    //     cout << "0 - Keep Executing / 1 - Quiting Executing." << endl;
    //     cin >> exit;
    // }

    do {
        cout << "Do you want t keep executing?" << endl;
        cout << "0 - Keep Executing / 1 - Quiting Executing." << endl;
        cin >> exit;
    }
    while(exit == false);
}
```

```cpp
#include <iostream>
using namespace std;

int main() {

    while (false)
    {
        cout << "While loop executed" << endl;
    }

    do {
        cout << "Do While - Do loop executed" << endl;
    }
    while (false);

}

// Do While - Do loop executed
```

## Ep#13 - Single & Multi-line Comments

## Ep#14 - Variable Scope

## Ep#15 - Break, Continue, and Goto

\*\*Definitions

- break: that ends or "breaks" out of a loop
- continue: that skips or "continues" on to the next iteration
  \*\*

**_Never use `goto`_**

## Highlight - Limits for Basic Data Types (numeric_limits)

```cpp
#include <iostream>
#include <limits>

using namespace std;

int main() {

    cout << sizeof(char) << " byte" << endl;
    cout << sizeof(int) << " byte" << endl;
    cout << sizeof(float) << " byte" << endl;
    cout << sizeof(double) << " byte" << endl;
    cout << sizeof(void*) << " byte" << endl;

    cout << "int min Value: " << numeric_limits<int>::min() << endl;
    cout << "float min Value: " << numeric_limits<float>::min() << endl;
    cout << "void* min Value: " << numeric_limits<void*>::min() << endl;
    cout << "int max Value: " << numeric_limits<int>::max() << endl;
    cout << "float max Value: " << numeric_limits<float>::max() << endl;
    cout << "void* max Value: " << numeric_limits<void*>::max() << endl;
    cout << "char min Value: " << int(numeric_limits<char>::min()) << endl;
    cout << "char max Value: " << int(numeric_limits<char>::max()) << endl;
    cout << "unsigned char min Value: " << int(numeric_limits<unsigned char>::min()) << endl;
    cout << "unsigned char max Value: " << int(numeric_limits<unsigned char>::max()) << endl;

    return 0;
}

```

```output
1 byte
4 byte
4 byte
8 byte
8 byte
int min Value: -2147483648
float min Value: 1.17549e-38
void* min Value: 0
int max Value: 2147483647
float max Value: 3.40282e+38
void* max Value: 0
char min Value: -128
char max Value: 127
unsigned char min Value: 0
unsigned char max Value: 255
```

## Ep#16 - Arrays Introduction for Beginners

```cpp
<datatype> <array name>[size of array] = { <initialize our array elements }
```

```cpp
int array[4] = {0, 1, 2, 3};
int array[] = {0, 1, 2, 3};
int array[4]
```

```cpp
#include <iostream>

using namespace std;

int main() {

    int array[4] = {10, 11, 12, 13};

    for (int i=0; i < 4; i++)
    cout << array[i] << endl;

    return 0;
}
```

```output
10
11
12
13
```

array 0, 1, 2, 3, ...n
memory [int, int, int, int, ...n]
memory [10, 11, 12, 14, ...n]
addr+0, addr+4byte, addr+8byte, addr+12byte, ...n

## Ep#17 - Functions with Parameters and Examples

<return type> <function name>(<Parameters>) {
...statements or blocks of code
return <result>; //only if there is a return type
}

```cpp
#include <iostream>
using namespace std;

void func1(){
    cout << "Hello World!" << endl;
}

int func2() {
    cout << "func2" << endl;
    return 10;
}

float sum(float a, float b) {
    float c;
    c = a + b;
    cout << "sum func" << endl;
    return c;
}

int main() {
    func1();
    cout << func2() << endl;
    cout << sum(3.5, 4.6) << endl;
    return 0;
}
```

```output
Hello World!
func2
10
sum func
8.1
```

## Ep#18 - Functions Prototypes / Declarations

```cpp
#include <iostream>
using namespace std;

void func1();
int func2();
float sum(float, float);

int main() {
    func1();
    cout << func2() << endl;
    cout << sum(3.5, 4.6) << endl;
    return 0;
}

void func1(){
    cout << "Hello World!" << endl;
}

int func2() {
    cout << "func2" << endl;
    return 10;
}

float sum(float a, float b) {
    float c;
    c = a + b;
    cout << "sum func" << endl;
    return c;
}
```

## Ep#19 - Function Overloading and Examples

```cpp
#include <iostream>
using namespace std;


int func(int, int);
int func(int, int, int);
float func(float, float);
double func(double, double);
char func(int n1, int n2, float n3);

int main() {
    float f1 = 1.0;
    float f2 = 2.0;
    double d1 = 2.0;
    double d2 = 3.0;
    cout << func(1, 2, 3) << endl;
    cout << func(f1, f2) << endl;
    cout << func(d1, d2) << endl;
    cout << func(40, 42, f1) << endl;
    return 0;
}

int func(int n1, int n2) {
    return n1 + n2;
}

int func(int n1, int n2, int n3) {
    return  n3 - (n1 + n2);
}

float func(float n1, float n2) {
    return n1 - n2;
}

double func(double n1, double n2) {
    return n1 * n2;
}

char func(int n1, int n2, float n3) {
    return n1 + n2 + n3;
}
```

```output
0
-1
6
S
```

## Ep#20 - References and Passing by Reference

<datatype>& ref = <somevar>;
_Allow you to modify the <somevar> outside its declaration function scope._

```cpp
#include <iostream>
using namespace std;

int main() {
    int num = 1;
    int& ref = num;
    cout << "ref: " << ref << endl;
    cout << "&ref: " << &ref << endl;
    cout << "&num: " << &num << endl;
    return 0;
}
```

```output
ref: 1
&ref: 0x7fffec7d7e0c
&num: 0x7fffec7d7e0c
```

```cpp
#include <iostream>
using namespace std;

void reference(int& number) {
    number = 3;
}

void notreference(int number) {
    number = 7;
}

int& ref(int& num) {
    num = 6;
    return num;
}

int main() {
    int num = 1;
    reference(num);
    cout << "reference: " << num << endl;
    notreference(num);
    cout << "notreference: " << num << endl;
    int& res = ref(num);
    cout << "result of ref(num): " << res << endl;
    return 0;
}
```

```output
reference: 3
notreference: 3
result of ref(num): 6
```

## Ep#21 - Recursion and Recursive Functions

```cpp
#include <iostream>
using namespace std;

int func() {
    cout << "We're having fun!" << endl;
    func();
    return 0;
}

int main() {
    func();
    return 0;
}
```

```output
We're having fun!
We're having fun!
We're having fun!
...
...
...
We're having fun!
We're having fun!
We're having fun!
Segmentation fault (core dumped)
```

```stack
-func() -> overflow the stack
-func()
-func()
-func()
-func()
...
...
...
-func()
-func()
-func() -> recrusively expect to remove the func() since here
-main()
```

```cpp
#include <iostream>
using namespace std;

int func(int num) {
    if(num != 0) {
        cout << "We're having fun with " << num << "!" << endl;
        func(--num);
    }
    return 0;
}

int main() {
    int num = 5;
    func(num);
    return 0;
}
```

```output
We're having fun with 5!
We're having fun with 4!
We're having fun with 3!
We're having fun with 2!
We're having fun with 1!
```

```cpp
#include <iostream>
using namespace std;

int sum = 0;

int func(int num) {
    if(num == 0) {
        cout << sum << endl;
    }
    else {
        sum += num;
        num--;
        func(num);
    }
    return 0;
}

int main() {
    int num = 5;
    func(num);
    return 0;
}
```

```output
15
```

## Ep#22 - Enums / Enumerations with Examples

enum <name> {
ConstantName_1,
ConstantName_2,
ConstantName_3,
...
ConstantName_n,
}

```cpp
#include <iostream>
using namespace std;

enum month {
    Jan,
    Feb,
    Mar,
    Apr,
    May,
    Jun,
    Jul,
    Aug,
    Sep,
    Oct,
    Nov,
    Dec
};

int main() {
    month selection;
    selection = Jan;

    // if (selection == Jan) // works as well
    if (selection == 0)
    {
        cout << "January was chosen." << endl;
    }

    return 0;
}
```

```output
January was chosen.
```

### Ep#23 - Structs / Structures with Examples

```cpp
struct <name> {
    // Whatever data types
    int someint1;
    int someint2;
    char char1;
};
```

```cpp
#include <iostream>
using namespace std;

struct location {
    string city;
    string state;
    string province;
    string country;
    int zipcode;
    int latitude;
    int longitude;

    void printloc() {
        cout << city << " ";
        cout << state << " ";
        cout << province << " ";
        cout << country << " ";
        cout << zipcode << " ";
        cout << latitude << " ";
        cout << longitude << endl;
    }

} loc[10];

int main() {

    // location loc[10];

    for(int i=0; i<10; i++) {
        loc[i].city = "New York";
        loc[i].state = "New York";
        loc[i].province = "n/a";
        loc[i].country = "USA";
        loc[i].zipcode = 5555;
        loc[i].latitude = i;
        loc[i].longitude = i + 1;
    }

    for(int i=0; i<10; i++) {
        loc[i].printloc();
    }

    return 0;
}
```

```output
New York New York n/a USA 5555 0 1
New York New York n/a USA 5555 1 2
New York New York n/a USA 5555 2 3
New York New York n/a USA 5555 3 4
New York New York n/a USA 5555 4 5
New York New York n/a USA 5555 5 6
New York New York n/a USA 5555 6 7
New York New York n/a USA 5555 7 8
New York New York n/a USA 5555 8 9
New York New York n/a USA 5555 9 10
```

## Ep#24 - Multidimensional Arrays with (2D/3D) Examples

<datatype> <name>[1_dim][2_dim][3_dim]...[n_dim]

```cpp
#include <iostream>
using namespace std;

int main() {

    int arr[2][2] = {
        {0, 1},
        {2, 3}
    };

    int arr3D[2][2][2];
    int value = 0;
    for(int i=0; i<2; i++) {
        for(int j=0; j<2; j++) {
            for(int k=0; k<2; k++) {
                arr3D[i][j][k] = value;
                value++;
            }
        }
    }

    cout << arr[0][1] << endl;
    cout << arr3D[0][1][0] << endl;

    for(int i=0; i<2; i++) {
        for(int j=0; j<2; j++) {
            for(int k=0; k<2; k++) {
                cout << arr3D[i][j][k] << endl;
            }
        }
    }

    return 0;
}
```

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
#include <string.h>

typedef struct Books {
   char title[50];
   char author[50];
   char subject[100];
   int book_id;
} Book;

int main( ) {

   Book book;

   strcpy( book.title, "C Programming");
   strcpy( book.author, "Nuha Ali");
   strcpy( book.subject, "C Programming Tutorial");
   book.book_id = 6495407;

   printf( "Book title : %s\n", book.title);
   printf( "Book author : %s\n", book.author);
   printf( "Book subject : %s\n", book.subject);
   printf( "Book book_id : %d\n", book.book_id);

   return 0;
}
```

```c
#include <stdio.h>

#define TRUE  1
#define FALSE 0

int main( ) {
   printf( "Value of TRUE : %d\n", TRUE);
   printf( "Value of FALSE : %d\n", FALSE);

   return 0;
}
```
