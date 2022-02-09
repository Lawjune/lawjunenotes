# 1 Get Started 

## 1.1 Writing a Simple C++ Program

------------------------------------------------------------------------------
**KEY CONCEPT: TYPES**
- *Types are one of the most fundamental concepts in programming and a concept that we will come back to over and over in this Primer.*
- *A type defines both the contents of a data element and the operations that are possible on those data.*
- *The data our programs manipulate are stored in variables and every variable has a type.*
------------------------------------------------------------------------------

### 1.1.1 Compiling and Executing Our Program

```sh
g++ -o prog1 prog1.cc
```

***Exercise 1.1***
*Review the documentation for your compiler and determine what file naming convention it uses. Compile and run the main program from page 2.*

**GCC and File Extensions**

**.h**	*C header file (not to be compiled or linked).*
**.c**	*C source code which must be preprocessed.*
**.i**	*C source code which should not be preprocessed.*
**.ii**	*C++ source code which should not be preprocessed.*
**.cc, .cp, .cxx, .cpp, .c++, .C**	*C++ source code which must be preprocessed.*
**.f, .for, .FOR**	*Fortran source code which should not be preprocessed.*
**.F, .fpp, .FPP**	*Fortran source code which must be preprocessed (with the traditional preprocessor).*
**.r**	*Fortran source code which must be preprocessed with a RATFOR preprocessor (not included with GCC).*
**.s**	*Assembler code.*
**.S**	*Assembler code which must be preprocessed.*
other	An object file to be fed straight into linking. Any file name with no recognized suffix is treated this way.

***Exercise 1.2***
*Change the program to return -1. A return value of -1 is often treated as an indicator that the program failed. Recompile and rerun your program to see how your system treats a failure indicator from main.*

## 1.2 A First Look at Input/Output

**Standard Input and Output Objects**
- cin
- cout
- cerr
- clog

**A Program That Uses the IO Library**
```cpp
#include <iostream>
int main()
{
    std::cout << "Enter two numbers:" << std::endl;
    int v1 = 0, v2 = 0;
    std::cin >> v1 >> v2;
    std::cout << "The sum of " << v1 << " and " << v2
    << " is " << v1 + v2 << std::endl;
    return 0;
}
```
```output
Enter two numbers:
4 7
The sum of 4 and 7 is 11
```

([**ostream object**] << [**a value to print**]) returns an [**ostream object**] 
```cpp
(std::cout << "Enter two numbers:") << std::endl;
```
=
```cpp
std::cout << "Enter two numbers:";
std::cout << std::endl;
```

***Warning***
*Programmers often add print statements during debugging. Such statements should always flush the stream. Otherwise, if the program crashes, output may be left in the buffer, leading to incorrect inferences about where the program crashed.*

**Using Names from the Standard Library** -> 3.1

**Reading from a Stream**

```cpp
(std::cin >> v1) >> v2;
```
= 
```cpp
std:cin >> v1;
std:cin >> c2;
```

**Completing the Program**

***Exercise 1.3***
*Write a program to print Hello, World on the standard output.*
```cpp
#include <iostream>

int main()
{
    std::cout << "Hello, World" << std::endl;
    return 0;
}
```

***Exercise 1.4***
*Our program used the addition operator, +, to add two numbers. Write a program that uses the multiplication operator, *, to print the product instead.*
```cpp
#include <iostream>
int main()
{
    std::cout << "Enter two numbers:" << std::endl;
    int v1 = 0, v2 = 0;
    std::cin >> v1 >> v2;
    std::cout << "The product of " << v1 << " and " << v2
    << " is " << v1 * v2 << std::endl;
    return 0;
}
```
```output
Enter two numbers:
4 7
The product of 4 and 7 is 28
```

***Exercise 1.5***
*We wrote the output in one large statement. Rewrite the program to use a separate statement to print each operand.*
```cpp
#include <iostream>
int main()
{
    std::cout << "Enter two numbers:";
    std::cout << std::endl;
    int v1 = 0, v2 = 0;
    std::cin >> v1;
    std::cin >> v2;
    std::cout << "The product of ";
    std::cout << v1;
    std::cout << " and ";
    std::cout << v2;
    std::cout << " is ";
    std::cout << v1 * v2;
    std::cout << std::endl;
    return 0;
}
```

***Exercise 1.6***
*Explain whether the following program fragment is legal.*
Fixed:
```cpp
std::cout << "The sum of " << v1 << " and " << v2 << " is " << v1 + v2 << std::endl;
```

## 1.3 A Word about Comments

```cpp
#include <iostream>
/*
* Simple main function:
* Read two numbers and write their sum
*/
int main()
{
    // Prompt user to enter two numbers
    std::cout << "Enter two numbers:" << std::endl;
    int v1 = 0, v2 = 0; // variables to hold the input we read 
    std::cin >> v1 >> v2; // real input
    std::cout << "The product of " << v1 << " and " << v2
              << " is " << v1 * v2 << std::endl;
    return 0;
}
```

***Exercise 1.7***
*Compile a program that has incorrectly nested comments.*
```cpp
/*
* comment pairs /* */ cannot nest.
* ''cannot nest'' is considered source code,
* as is the rest of the program
*/
int main()
{
    return 0;
}
```

***Exercise 1.8***
*Indicate which, if any, of the following output statements are legal:*
```cpp
std::cout << "/*";
std::cout << "*/";
std::cout << /* "*/" */;
std::cout << /* "*/" /* "/*" */;
```

Corrected.
```cpp
std::cout << "/*";
std::cout << "*/";
std::cout << /* "*/" */";
std::cout << /* "*/" /* "/*" */;
```
```output
/**/ */ /* 
```

## 1.4 Flow of Control

### 1.4.1 The `while` Statement

```cpp
#include <iostream>
int main()
{
    int sum = 0, val = 1;
    // keep executing the while as long as val is less than or equal to 10
    while (val <= 10) {
        sum += val; // assigns sum + val to sum
        ++val;
        // add 1 to val
    }
    std::cout << "Sum of 1 to 10 inclusive is "
              << sum << std::endl;
    return 0;
}
```
```output
Sum of 1 to 10 inclusive is 55
```

***Exercise 1.9***
*Write a program that uses a while to sum the numbers from 50 to 100.*
```cpp
#include <iostream>
int main()
{
    int sum = 0, val = 50;
    // keep executing the while as long as val is less than or equal to 10
    while (val <= 100) {
        sum += val; // assigns sum + val to sum
        ++val;
        // add 1 to val
    }
    std::cout << "Sum of 50 to 100 inclusive is "
              << sum << std::endl;
    return 0;
}
```
```output
Sum of 50 to 100 inclusive is 3825
```

***Exercise 1.10***
*In addition to the ++ operator that adds 1 to its operand, there is a decrement operator (--) that subtracts 1. Use the decrement operator to write a while that prints the numbers from ten down to zero.*

```cpp
#include <iostream>
int main()
{
    int i = 10;
    while (i >= 0) {
        std::cout << i << std::endl;
        i--;
    }

    return 0;
}
```

***Exercise 1.11***
*Write a program that prompts the user for two integers. Print each number in the range specified by those two integers.*

```cpp
#include <iostream>

void print_range(int min, int max) 
{
    while (min >= max) {
        std::cout << "Please input two integers: " << std::endl;
        std::cin >> min >> max;
        if (min >= max) {
            std::cout << "The last number must be greater than the previous number!" << std::endl;
            std::cout << "Please input again!" << std::endl;
            continue;
        } 
        while (min <= max) {
            std::cout << min << " ";
            min++;
        }
        std::cout << std::endl;
    }
}


int main()
{
    int min = 0, max = 0;

    print_range(min, max);

    return 0;
}
```

*Master Piece*
```cpp
// Print each number in the range specified by two integers.

#include <iostream>

using std::cout;
using std::cin;

void print_range(int lo, int hi)
{
    if (lo > hi)
    {
        print_range(hi, lo);
        return;
    }
    for (int i = lo; i != hi; ++i)
        cout << i << " ";
}

int main()
{
    int low = 0, high = 0;
    cout << "please input two integers:\n";
    cin >> low >> high;
    print_range(low, high);
    return 0;
}
```

### 1.4.2 The `for` Statement

```cpp
#include <iostream>
int main()
{
    int sum = 0;
    // sum values from 1 through 10 inclusive
    for (int val = 1; val <= 10; ++val)
        sum += val; // equivalent to sum = sum + val
        std::cout << "Sum of 1 to 10 inclusive is "
                  << sum << std::endl;
    return 0;
}
```

***Exercise 1.12***
*What does the following for loop do? What is the final value of sum?*
```cpp
int sum = 0;
for (int i = -100; i <= 100; ++i)
    sum += i;
```
=>
*the loop sums the numbers from -100 to 100. the final value of sum is zero.*

***Exercise 1.13***
*Rewrite the exercises from § 1.4.1 (p. 13) using for loops.*

*Ex1.9*
```cpp
#include <iostream>

int main()
{
    int sum = 0;
    for (int i = 50; i <= 100; ++i) sum += i;
    std::cout << "the sum is: " << sum << std::endl;

    return 0;
}
```

*Ex1.10*
```cpp
#include <iostream>

int main()
{
    for (int i = 10; i >= 0; --i)
        std::cout << i << std::endl;
    return 0;
}
```

*Ex1.11*
```cpp
#include <iostream>

int main()
{
    std::cout << "please input two integers:\n";
    int small = 0, big = 0;
    std::cin >> small >> big;

    if (small > big)
    {
        int tmp = small;
        small = big;
        big = tmp;
    }

    for (int i = small; i != big; ++i)
        std::cout << i << std::endl;

    return 0;
}
```

***Exercise 1.14***
*Compare and contrast the loops that used a for with those using a while. Are there advantages or disadvantages to using either form?*

*A similar question on Stack Overflow:*

A `while` loop will always evaluate the condition first.
```c
while (condition) {
  //gets executed after condition is checked
}
```

A `do/while` loop will always execute the code in the do{} block first and then evaluate the condition.
```c
do {
  //gets executed at least once
} while (condition);
```

A `for` loop allows you to initiate a counter variable, a check condition, and a way to increment your counter all in one line.
```c
for (int x = 0; x < 100; x++) {
   //executed until x >= 100
}
```

**Exercise 1.15**
*Write programs that contain the common errors discussed in the box on page 16. Familiarize yourself with the messages the compiler generates.*

**Syntax Errors:**
```cpp
int main(){
    std::cout << "Hello World!" << std::endl // semicolon missed 
    return 0;
}
```

**Type errors:**
```cpp
int main(){
    char s = "Hello World!"; // Here char should be std::string
    std::cout << s << endl;
    return 0;
}
```

**Declaration errors:**
```cpp
int main(){
    int k = 0;
    std::cout << K << std::endl; // use of undeclared identifier 'K'
    return 0;
}
```

### 1.4.3 Reading an Unknown Number of Inputs

```cpp
#include <iostream>
int main()
{
int sum = 0, value = 0;
    // read until end-of-file, calculating a running total of all values read
    while (std::cin >> value)
        sum += value; // equivalent to sum = sum + value
    std::cout << "Sum is: " << sum << std::endl;
    return 0;
}
```

*An istream becomes invalid when we hit end-of-file or encounter an invalid input, such as reading a value that is not an integer.*


### 1.4.4 The `if` Statement

```cpp
#include <iostream>
int main()
{
// currVal is the number we’re counting; we’ll read new values into val
    int currVal = 0, val = 0;
    // read first number and ensure that we have data to process
    if (std::cin >> currVal) {
        int cnt = 1; // store the count for the current value we’re processing
        while (std::cin >> val) { // read the remaining numbers
            if (val == currVal)
            // if the values are the same
                ++cnt;
            // add 1 to cnt
            else { // otherwise, print the count for the previous value
                std::cout << currVal << " occurs "
                        << cnt << " times" << std::endl;
                currVal = val;
                // remember the new value
                cnt = 1;
                // reset the counter
            }
        } // while loop ends here
    // remember to print the count for the last value in the file
    std::cout << currVal << " occurs "
              << cnt << " times" << std::endl;
    } // outermost if statement ends here
    return 0;
}
```
```output
47 47 47 47 7 7 7 4  4 4247 247 247 247 774 774
47 occurs 4 times
7 occurs 3 times
4 occurs 2 times
4247 occurs 1 times
247 occurs 3 times
```

***Exercise 1.17***
*What happens in the program presented in this section if the input values are all equal? What if there are no duplicated values?*

- If the input values are all equal, it will print a line which shows the count of the number you input.
- If there are no duplicated values, when different values input, a new line will be printed if you click `Enter`.

***Exercise 1.18***

Compile and run the program from this section giving it only equal values as input. Run it again giving it values in which no number is repeated.

```cpp
#include <iostream>
int main()
{
// currVal is the number we’re counting; we’ll read new values into val
    int currVal = 0, val = 0;
    // read first number and ensure that we have data to process
    if (std::cin >> currVal) {
        int cnt = 1; // store the count for the current value we’re processing
        while (std::cin >> val && val == currVal) { // read the remaining numbers
            if (val == currVal)
            // if the values are the same
                ++cnt;
            // add 1 to cnt
            else { // otherwise, print the count for the previous value
                std::cout << currVal << " occurs "
                        << cnt << " times" << std::endl;
                currVal = val;
                // remember the new value
                cnt = 1;
                // reset the counter
            }
        } // while loop ends here
    // remember to print the count for the last value in the file
    std::cout << currVal << " occurs "
              << cnt << " times" << std::endl;
    } // outermost if statement ends here
    return 0;
}
```
```output
4 7 47
4 occurs 1 times
```

***Exercise 1.19***
Revise the program you wrote for the exercises in § 1.4.1 (p. 13) that printed a range of numbers so that it handles input in which the first number is smaller than the second.

```cpp
// Print each number in the range specified by two integers.

#include <iostream>

int main()
{
    int small = 0, big = 0;
    std::cout << "please input two integers:";
    std::cin >> small >> big;

    if (small > big) {
        int tmp = small;
        small = big;
        big = tmp;
    }

    while (small <= big) {
        std::cout << small << " ";
        ++small;
    }
    std::cout << std::endl;

    return 0;
}
```

## 1.5 Introducing Classes

### 1.5.1 The Sales_item Class

- Call a function named `isbn` to fetch the ISBN from a `Sales_item` object.
- Use the input (>>) and output (<<) operators to read and write objects of type `Sales_item`.
- Use the assignment operator (=) to assign one `Sales_item` object to another.
- Use the addition operator (+) to add two `Sales_item` objects. The two ob-
jects must refer to the same ISBN . The result is a new `Sales_item` object
whose ISBN is that of its operands and whose number sold and revenue are
the sum of the corresponding values in its operands.
- Use the compound assignment operator (+=) to add one Sales_item object
into another.

------------------------------------------------------------------------------
**KEY CONCEPT : CLASSES DEFINE B EHAVIOR**
The important thing to keep in mind when you read these programs is that the author of the `Sales_item` class defines all the actions that can be performed by objects of this class. 

That is, the `Sales_item` class defines what happens when a `Sales_item` object is created and what happens when the assignment, addition, or the input and output operators are applied to Sales_items.

In general, the class author determines all the operations that can be used on objects of the class type. For now, the only operations we know we can perform on `Sales_item` objects are the ones listed in this section.
------------------------------------------------------------------------------

**Reading and Writing Sales_items**

***Exercise 1.20***
*http://www.informit.com/title/032174113 contains a copy of Sales_item.h in the Chapter 1 code directory. Copy that file to your working directory. Use it to write a program that reads a set of book sales transactions, writing each transaction to the standard output.*

```cpp
#include <iostream>
#include "include/Sales_item.h"

using std::cin;
using std::cout;
using std::endl;

int main()
{
    for (Sales_item item; cin >> item; cout << item << endl);
    return 0;
}
```
```output
0-201-70353-X 4 24.99
0-201-70353-X 4 99.96 24.99
0-201-70353-X 7 40               
0-201-70353-X 7 280 40
aaa 4 7
aaa 4 28 7
```

***Exercise 1.21***
*Write a program that reads two Sales_item objects that have the same ISBN and produces their sum.*

```cpp
#include <iostream>
#include "include/Sales_item.h"

int main()
{
    Sales_item item1, item2, item_sum;
    std::cin >> item1 >> item2;
    if (item1.isbn() == item2.isbn()) {
        item_sum = item1 + item2; 
        std::cout << item_sum << std::endl;
    } else {
        std::cerr << "Different ISBN!" << std::endl;
    }

    return 0;
}
```
```output-1
abc 4 40
abc 7 70
abc 11 650 59.0909
```
```output-2
aaa 4 70
bbb 7 40
Different ISBN!
```

***Exercise 1.22***
*Write a program that reads several transactions for the same ISBN. Write the sum of all the transactions that were read.*

```cpp
#include <iostream>
#include "include/Sales_item.h"

int main()
{
    Sales_item total;
    if (std::cin >> total)
    {
        Sales_item trans;
        while (std::cin >> trans)
        {
            if (total.isbn() == trans.isbn())
                total += trans;
            else
            {
                std::cout << total << std::endl;
                total = trans;
            }
        }
        std::cout << total << std::endl;
    }
    else
    {
        std::cerr << "No data?!" << std::endl;
        return -1;
    }

    return 0;
}
```

### 1.5.2 A First Look at Member Functions

```cpp
#include <iostream>
#include "Sales_item.h"
int main()
{
    Sales_item item1, item2;
    std::cin >> item1 >> item2;
    // first check that item1 and item2 represent the same book
    if (item1.isbn() == item2.isbn()) {
        std::cout << item1 + item2 << std::endl;
        return 0;
    // indicate success
    } else {
        std::cerr << "Data must refer to same ISBN"
                  << std::endl;
    return -1; // indicate failure
    }
}
```

***Exercise 1.23***
*Write a program that reads several transactions and counts how many transactions occur for each ISBN.*

*My Solution*
```cpp
#include <iostream>
#include "include/Sales_item.h"
int main()
{
    Sales_item curr_item, item;

    if (std::cin >> curr_item) {
        while (std::cin >> item) {
            if (curr_item.isbn() == item.isbn())
                curr_item += item;
            else {
                std::cout << curr_item << std::endl;
                curr_item = item;
            }
        }

        std::cout << curr_item << std::endl;
    }

    return 0;
}
```

*Master Piece*
```cpp
#include <iostream>
#include "include/Sales_item.h"

int main()
{
    Sales_item currItem, valItem;
    if (std::cin >> currItem)
    {
        int cnt = 1;
        while (std::cin >> valItem)
        {
            if (valItem.isbn() == currItem.isbn())
            {
                ++cnt;
            }
            else
            {
                std::cout << currItem << " occurs " << cnt << " times " << std::endl;
                currItem = valItem;
                cnt = 1;
            }
        }
        std::cout << currItem << " occurs "<< cnt << " times " << std::endl;
    }
    return 0;
}
```

***Exercise 1.24***
*Test the previous program by giving multiple transactions representing multiple ISBNs. The records for each ISBN should be grouped together.*

```cpp
#include <iostream>
#include <fstream>
#include "include/Sales_item.h"


int main()
{
    Sales_item currItem, valItem;
    std::ofstream fout("data/items.txt");
    if (std::cin >> currItem)
    {
        int cnt = 1;
        while (std::cin >> valItem)
        {
            if (valItem.isbn() == currItem.isbn())
            {
                ++cnt;
            }
            else
            {
                std::cout << currItem << " occurs " << cnt << " times " << std::endl;
                fout << currItem;
                fout << " occurs ";
                fout << cnt;
                fout << " times ";
                fout << std::endl;
                currItem = valItem;
                cnt = 1;
            }
        }
        std::cout << currItem << " occurs "<< cnt << " times " << std::endl;
        fout << currItem;
        fout << " occurs ";
        fout << cnt;
        fout << " times ";
        fout << std::endl;
        // fout << std::endl;
    }
    return 0;
}
```

