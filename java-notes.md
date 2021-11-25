# Fundamentals

1. What is the difference between a class and an object? 
- A class is a blueprint or template for creating objects. 
- An object is an instance of a class. 

2. What does instantiating mean? 
- Instantiating means creating an instance of a class: ***new Customer()***

3. What is the difference between stack and heap memory? How are
they managed? 
- Stack is used for storing primitive types (numbers, boolean and
character).
- Variables that store references to objects in the heap.
- Variables stored in the stack are immediately cleared when they go out
of scope (eg when a method finishes execution). 
- Objects stored in the heap get removed later on when they’re no longer references.
- This is done by Java’s garbage collector. 

4. What are the problems of procedural code? How does object-oriented programming help solve these problems?
- Big classes with several unrelated methods focusing on different concerns and responsibilities. These methods often have several prameters. You often see the same group of parameters repeated across these methods. All you see is procedures calling each other passing arguments around. 
- By applying object-oriented programming techniques, we extract these repetitive parameters and declare them as fields in our classes. Our
classes will then encapsulate both the data and the operations on the data (methods). As a result, our methods will have fewer parameters and our code will be cleaner and more reusable

5. What is encapsulation?
- Encapsulation is the first principle of object-oriented programming.
- It suggests that we should bundle the data and operations on the data inside a single unit (class). 

6. Why should we declare fields as private? 
- How we store data in an object is considered an implementation detail. 
- We may change how we store the data internally. 
- Plus, we don’t want our objects to go into a bad state (hold bad data). 
- That’s why we should declare fields as private and provide getters and or setters only if required. 
- These setters can ensure our objects don’t go into a bad state by validating the values that are passed to them. 

7. What is abstraction? 
- Abstraction is the second principle of object-oriented programming.
- It suggests that we should reduce complexity by hiding the unnecessary implementation details. 
- As a metaphor, think of the remote control of your TV. All the complexity inside the remote control is hidden from you. 
- It’s abstracted away. You just work with a simple interface to control your TV. We want our objects to be like our remote controls.

8. What is coupling?
- Coupling represents the level of dependency between software entities (eg classes). 
- The more our classes are dependent on each other, the harder it is to change them. 
- Changing one class may result in several cascading and breaking changes.

9. How does the abstraction principle help reduce coupling? 
- By hiding the implementation details, we prevent other classes from getting affected when we change these details. 
- For example, if the logic board and transistors inside a remote control change from one model to another, we’re not affected. We still use the same interface to work with our TV. 
- Also, reducing these details and exposing fewer methods makes our classes easier to use. 
- For example, remote controls with fewer buttons are easier to use. 

10. What are constructors? 
- Constructors are called when we instantiate our class. 
- We use them to initialize our objects. 
- Initialization means putting an object into an early or initial state (eg giving it initial values). 

11. What is method overloading? 
- Method overloading means declaring a method with the same name but with different signatures. 
- The number, type and order of its parameters will be different. 

12. What are static methods? 
- Static methods are accessible via classes, not objects. 



# Part 1 Fundamental 

## Types

### Variables and Constants

We use variables to temporarily store data in computer's memory.

### Primitives and Reference Types

- Primitive: For storing simple values
- Reference: For storing complex object

* Primitive:
** byte: 1 Byte, [-128, 127]
** short: 2 Bytes, [-32k, 32k]
** int: 4 Bytes, [-2B, 2B]
** long: 8 Bytes
** float: 4 Bytes
** double: 8 Bytes
** char: 2 Bytes
** boolean: 1 Byte

```Java
package com.lawjune;

public class Main {

    public static void main(String[] args) {
        byte age = 30;
        // int viewsCount = 3_123_456_789;
        long viewsCount = 3_123_456_789L;
        float price = 10.99F;
        char letter = 'A';
        boolean isEligible = true;
    }
}
```

* Reference:
** date
** mail message

```Java
package com.lawjune;

import java.util.Date;

public class Main {

    public static void main(String[] args) {
        byte age = 30;
        Date now = new Date();
        System.out.println(now);
    }
}
```

Memory Management of Reference - Copied by their "reference" against Primitive copied by their values which are completely indepent of each other
```Java
package com.lawjune;

import java.awt.*;

public class Main {

    public static void main(String[] args) {
        Point point1 = new Point();
        Point point2 = point1;
        System.out.println(point2);
        point1.setLocation(1 , 2);
        System.out.println(point2);
    }
}
```

### Strings 

```Java
package com.lawjune;


public class Main {

    public static void main(String[] args) {
        String message = "Hello World";

        System.out.println(message + "!!");
        System.out.println(message.endsWith("d"));
        System.out.println(message.length());
        System.out.println(message.indexOf("W"));
        System.out.println(message.indexOf("sky"));

        System.out.println(message.replace("World", "Jun"));
        // Java String is immutable, any modification in the String will return a new String

        System.out.println(message.toLowerCase());
        System.out.println(message.toUpperCase());
        
        message = "  " + "Hello World";
        System.out.println(message.trim()); // Get rit of these white spaces
    }
}
```

### Escape Sequences
```Java
String message = "Hello \"Jun\"";
```
```Java
// C:\Windows\...
String message = "c:\\Window\\...";
```

"\n" => new line
"\t" => tab

### Arrays
```Java
package com.lawjune;


import java.util.Arrays;

public class Main {

    public static void main(String[] args) {
        int[] numbers = new int[5];
        numbers[0] = 1;
        numbers[1] = 2;
        System.out.println(numbers);
        System.out.println(Arrays.toString(numbers));

    }
}
```

Initialize the pre-defined-value array
```Java
package com.lawjune;

import java.util.Arrays;

public class Main {

    public static void main(String[] args) {
        int[] numbers = { 2, 3, 5, 1, 4 };
        System.out.println(numbers.length);
        System.out.println(Arrays.toString(numbers));
        Arrays.sort(numbers);
        System.out.println(Arrays.toString(numbers));
    }
}
```

### Multi-dimensional Arrays
```Java
package com.lawjune;

import java.util.Arrays;

public class Main {

    public static void main(String[] args) {
        int[][] numbers = new int[2][3];
        numbers[0][0] = 1;
        System.out.println(Arrays.deepToString(numbers));
    }
}
```

```Java
        int[][] numbers = {{1, 2, 3}, {4, 5, 6}};
        System.out.println(Arrays.deepToString(numbers));
 ```

### Constants

```Java
final float PI = 3.14F
```

### Arithmetic Expressions

```Java
package com.lawjune;

import java.util.Arrays;

public class Main {

    public static void main(String[] args) {
        int int_result = 10 / 3;
        System.out.println(int_result);

        double float_result = (double)10 / (double)3;
        System.out.println(float_result);

        int x = 1;
        x++;
        System.out.println(x);
        ++x;
        System.out.println(x);
    }
}
```

### Order of Operations
```Java
package com.lawjune;

public class Main {

    public static void main(String[] args) {
        int x = 10 + 3 * 2;
        int y = (10 + 3) * 2;
        System.out.println(x);
        System.out.println(y);
    }
}
```

()
* /
+ -

### Casting

*Implicit Casting* => Bigger Casting 
byte -> short -> int -> long -> float -> double
```Java
package com.lawjune;

public class Main {

    public static void main(String[] args) {
        short x = 1;
        int y = x + 2;
        System.out.println(y);
        // short -> 2 bytes
        // int -> 4 bytes
        // First Java looks at the value it's 1
        // It's going to allocate another variable
        // An anonymous variable somewhere in memory we don;t know where that is
        // That variable is gonna be an integer
        // Then Java is gonna copy the value of x into that memory space
        // Then it will add these two numbers together
    }
}

```Java
package com.lawjune;

public class Main {

    public static void main(String[] args) {
        double x = 1.1;
        double y = x + 2; // 2.0
        System.out.println(y);
        // An integer is less precise than a double
        // Java is going to automatically cast this integer to a double
        // So that will be 2.0 to be added 1.1
    }
}
```

*Explicit Casting* 

```Java
package com.lawjune;

public class Main {

    public static void main(String[] args) {
        double x = 1.1;
        int y = (int)x + 2; // 2.0
        System.out.println(y);
    }
}
```

```Java
package com.lawjune;

public class Main {

    public static void main(String[] args) {
        String x = "1.1";
        // Integer.parseInt(x)
        double y = Double.parseDouble(x) + 2; // 2.0
        System.out.println(y);
    }
}
```

### The Math Class
```Java
package com.lawjune;

public class Main {

    public static void main(String[] args) {
        int round = Math.round(1.1F);
        System.out.println("round: " + round);

        int ceil = (int)Math.ceil(1.1F);
        System.out.println("ceil: " + ceil);

        int floor = (int)Math.floor(1.1F);
        System.out.println("floor: " + floor);

        float max = Math.max(1.1F, 2.3F);
        System.out.println("max: " + max);

        float min = Math.min(1.1F, 2.3F);
        System.out.println("min: " + min);

        double random = Math.random();
        System.out.println("random: " + random);

        int intRandom = (int) (Math.random() * 100);
        System.out.println("intRandom: " + intRandom);

        int roundRandom = (int) Math.round(Math.random() * 100);
        System.out.println("roundRandom: " + roundRandom);
    }
}
```

### Formatting Numbers
```Java
package com.lawjune;

import java.text.NumberFormat;

public class Main {

    public static void main(String[] args) {
        // $1, 234, 567
        NumberFormat currency =  NumberFormat.getCurrencyInstance();
        String currencyResult = currency.format(1234567.891);
        System.out.println("currencyResult " + currencyResult);
        // 10%
        // NumberFormat percent =  NumberFormat.getPercentInstance();
        String percentResult = NumberFormat.getPercentInstance().format(0.425);
        System.out.println("percentResult " + percentResult);
    }
}
```

### Reading Input 
```Java
package com.lawjune;

import java.util.Scanner;

public class Main {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Name: ");
        String name = scanner.nextLine().trim(); //     Jun Luo
        System.out.println("Your name " + name);

        System.out.print("Age: ");
        byte age = scanner.nextByte();
        System.out.println("Your age " + age);
    }
}
```

### Project: Mortgage Calculator
```Java
package com.lawjune;

import java.text.NumberFormat;
import java.util.Scanner;

public class Main {

    public static void main(String[] args) {
        final byte MONTHS_IN_YEAR = 12;
        final byte PERCENT = 100;
        Scanner scanner = new Scanner(System.in);

        System.out.print("Principal: ");
        int principal = scanner.nextInt();
        System.out.print("Annual Interest Rate: ");
        float monthlyInterest = scanner.nextFloat() / PERCENT / MONTHS_IN_YEAR;
        System.out.print("Period (Years): ");
        byte years = scanner.nextByte();
        int numberOfPayments = years * MONTHS_IN_YEAR;

        double mortgage = principal
                * (monthlyInterest * Math.pow(1 + monthlyInterest, numberOfPayments))
                / (Math.pow(1 + monthlyInterest, numberOfPayments) - 1);

        String mortgageFormatted = NumberFormat.getCurrencyInstance().format(mortgage);
        System.out.println("Mortgage: " + mortgageFormatted);

    }
}
```

## Control Flow

### Comparison Operators
==, >, <, >=, <=

### Logical Operators
&&, ||, !

### If Statement
### Simplify If Statement
```Java
package com.lawjune;

public class Main {

    public static void main(String[] args) {
        int income = 120_000;
//        boolean hasHighIncome = false;
//        if (income > 100_000)
//            hasHighIncome = true;
        boolean hasHighIncome = (income > 100_000);
    }
}
```

### The Ternary Opeartor
```Java
        int income = 120_000;
        String className = income > 100_000 ? "First" : "Economy";
```

### Switch Statement
```Java
package com.lawjune;

public class Main {

    public static void main(String[] args) {
        String role = "admin";

        switch (role) {
            case "admin":
                System.out.println("You are an admin");
                break;
            case "moderator":
                System.out.println("You are a moderator");
                break;
            default:
                System.out.println("You are a guest");
        }
}
}
```

### Exercise: FizzBuzz
```Java
package com.lawjune;

import java.util.Scanner;

public class Main {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Number: ");
        int number = scanner.nextInt();
        if (number % 5 == 0 && number % 3 == 0)
            System.out.println("FizzBuzz");
        else if (number % 3 == 0)
            System.out.println("Buzz");
        else if (number % 5 == 0)
            System.out.println("Fizz");
        else
            System.out.println(number);
}
}
```

### For Loops
```Java
package com.lawjune;

public class Main {

    public static void main(String[] args) {
        for (int i = 0; i < 5; i ++)
            System.out.println("Hello World");
    }
}
```

### While Loops
```Java
package com.lawjune;

import java.util.Scanner;

public class Main {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String input = "";
        while (!input.equals("quit")) {
            System.out.print("Input: ");

            input = scanner.next().toLowerCase();
        }
    }
}
```

### Do..While Loops
```Java
        do {
            System.out.print("Input: ");
            input = scanner.next().toLowerCase();
        } while (!input.equals("quit"));
```

### Break and Continue
```Java
package com.lawjune;

import java.util.Scanner;

public class Main {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String input = "";
        while (true) {
            System.out.print("Input: ");
            input = scanner.next().toLowerCase();
            if (input.equals("pass"))
                continue;
            if (input.equals("quit"))
                break;
            System.out.println(input);
        }
    }
}
```

### For Each
```Java
package com.lawjune;

import java.util.Scanner;

public class Main {

    public static void main(String[] args) {

        String[] fruits = { "Apple", "Mango", "Orange"};
        for (int i = 0; i < fruits.length; i++)
            System.out.println(fruits[i]);

        for (String fruit : fruits)
            System.out.println(fruit);
    }
}
```

### Project: Mortgate Calculator
```Java
package com.lawjune;

import java.text.NumberFormat;
import java.util.Scanner;

public class Main {

    public static void main(String[] args) {
        final byte MONTHS_IN_YEAR = 12;
        final byte PERCENT = 100;
        int principal;
        float monthlyInterest;
        byte years;

        Scanner scanner = new Scanner(System.in);


        while (true) {
            System.out.print("Principal: ");
            principal = scanner.nextInt();
            if (principal >= 1000 && principal < 1_000_000)
                break;
            System.out.println("Enter a value between 1k to 1m!");
        }

        while (true) {
            System.out.print("Annual Interest Rate: ");
            monthlyInterest = scanner.nextFloat() / PERCENT / MONTHS_IN_YEAR;
            if ( monthlyInterest > 0 && monthlyInterest <= 30)
                break;
            System.out.println("Enter a value between 0 and 30");
        }

        while (true) {
            System.out.print("Period (Years): ");
            years = scanner.nextByte();
            if ( years >= 5 && years <= 40)
                break;
            System.out.println("Enter a value between 5 to 40");
        }
        int numberOfPayments = years * MONTHS_IN_YEAR;

        double mortgage = principal
                * (monthlyInterest * Math.pow(1 + monthlyInterest, numberOfPayments))
                / (Math.pow(1 + monthlyInterest, numberOfPayments) - 1);

        String mortgageFormatted = NumberFormat.getCurrencyInstance().format(mortgage);
        System.out.println("Mortgage: " + mortgageFormatted);

    }
}
```

## Clean Coding

"Any fool can write code that computers can understand. Good programers write code that humans can understand."
      ------Martin Fowler

### Creating Methods
```Java
package com.lawjune;

public class Main {

    public static void main(String[] args) {
        greetUser("Jun", "Luo");
    }

    public static void greetUser(String firstName, String lastName) {
        System.out.println("Hello " + firstName + " " + lastName);
    }
}
```

### Refactoring
Changing the structure of the code without changing its behavior.

- The lines of code that always go together.
- Repetitive patterns in your code.

#### Extracting Methods
```java
package com.lawjune;

import java.text.NumberFormat;
import java.util.Scanner;

public class Main {

    public static void main(String[] args) {

        int principal;
        float annualInterest;
        byte years;

        Scanner scanner = new Scanner(System.in);


        while (true) {
            System.out.print("Principal: ");
            principal = scanner.nextInt();
            if (principal >= 1000 && principal < 1_000_000)
                break;
            System.out.println("Enter a value between 1k to 1m!");
        }

        while (true) {
            System.out.print("Annual Interest Rate: ");
            annualInterest = scanner.nextFloat();

            if ( annualInterest >= 1 && annualInterest <= 30)
                break;
            System.out.println("Enter a value between 1 and 30");
        }

        while (true) {
            System.out.print("Period (Years): ");
            years = scanner.nextByte();
            if ( years >= 5 && years <= 40)
                break;
            System.out.println("Enter a value between 5 to 40");
        }

        double mortgage = calculateMortgagte(principal, annualInterest, years);

        String mortgageFormatted = NumberFormat.getCurrencyInstance().format(mortgage);
        System.out.println("Mortgage: " + mortgageFormatted);

    }

    public static double calculateMortgagte(
            int principal,
            float annualInterest,
            byte years) {

        final byte MONTHS_IN_YEAR = 12;
        final byte PERCENT = 100;
        double mortgage = 0;

        float monthlyInterest = annualInterest / PERCENT / MONTHS_IN_YEAR;

        float numberOfPayments = years * MONTHS_IN_YEAR;
        mortgage = principal
                * (monthlyInterest * Math.pow(1 + monthlyInterest, numberOfPayments))
                / (Math.pow(1 + monthlyInterest, numberOfPayments) - 1);

        return mortgage;
    }
}
```

#### Refactoring Repetitive Patterns
```java
package com.lawjune;

import java.text.NumberFormat;
import java.util.Scanner;

public class Main {

    public static void main(String[] args) {
        
        int principal = (int)readNumber("Principal: ", 1000, 1_000_000);

        float annualInterest = (float) readNumber("Annual Interest Rate: ", 1, 30);
        byte years = (byte) readNumber("Period (Years): ", 5, 40);

        double mortgage = calculateMortgagte(principal, annualInterest, years);

        String mortgageFormatted = NumberFormat.getCurrencyInstance().format(mortgage);
        System.out.println("Mortgage: " + mortgageFormatted);

    }

    public static double readNumber(
            String prompt,
            double min,
            double max) {
        Scanner scanner = new Scanner(System.in);
        double value;
        while (true) {
            System.out.print(prompt);
            value = scanner.nextFloat();

            if ( value >= min && value <= max)
                break;
            System.out.println("Enter a value between " + min + "and " + max);
        }
        return value;
    }

    public static double calculateMortgagte(
            int principal,
            float annualInterest,
            byte years) {

        final byte MONTHS_IN_YEAR = 12;
        final byte PERCENT = 100;
        double mortgage;

        float monthlyInterest = annualInterest / PERCENT / MONTHS_IN_YEAR;

        float numberOfPayments = years * MONTHS_IN_YEAR;
        mortgage = principal
                * (monthlyInterest * Math.pow(1 + monthlyInterest, numberOfPayments))
                / (Math.pow(1 + monthlyInterest, numberOfPayments) - 1);

        return mortgage;
    }
}
```

### Project - Payment Schedule
https://www.mtgprofessor.com/formulas.htm
$$ 
B = L[(1 + c).pow(n) - (1 + c).pow(p)] / [(1 +c).pow(n) - 1]
$$

#### Solution
```java
package com.lawjune;

import java.text.NumberFormat;
import java.util.Scanner;

public class Main {

    final static byte MONTHS_IN_YEAR = 12;
    final static byte PERCENT = 100;

    public static void main(String[] args) {

        int principal = (int)readNumber("Principal: ", 1000, 1_000_000);

        float annualInterest = (float) readNumber("Annual Interest Rate: ", 1, 30);
        byte years = (byte) readNumber("Period (Years): ", 5, 40);

        double mortgage = calculateMortgage(principal, annualInterest, years);

        String mortgageFormatted = NumberFormat.getCurrencyInstance().format(mortgage);
        System.out.println();
        System.out.println("MORTGAGE");
        System.out.println("--------");
        System.out.println("Monthly Payments: "  + mortgageFormatted);
//        System.out.println("Mortgage: " + mortgageFormatted);

        System.out.println();
        System.out.println("PAYMENT SCHEDULE");
        System.out.println("----------------");
        for (short month = 1; month <= years * MONTHS_IN_YEAR; month++) {
            double balance = calculateBalance(principal, annualInterest, years, month);
            System.out.println(NumberFormat.getCurrencyInstance().format(balance));
        }
    }

    public static double readNumber(
            String prompt,
            double min,
            double max) {
        Scanner scanner = new Scanner(System.in);
        double value;
        while (true) {
            System.out.print(prompt);
            value = scanner.nextFloat();

            if ( value >= min && value <= max)
                break;
            System.out.println("Enter a value between " + min + "and " + max);
        }
        return value;
    }

    public static double calculateBalance(
            int principal,
            float annualInterest,
            byte years,
            short numberOfPaymentsMade
    ) {


        float monthlyInterest = annualInterest / PERCENT / MONTHS_IN_YEAR;
        float numberOfPayments = years * MONTHS_IN_YEAR;

        double balance = principal
                * (Math.pow(1 + monthlyInterest, numberOfPayments) - Math.pow(1 + monthlyInterest, numberOfPaymentsMade))
                / (Math.pow(1 + monthlyInterest, numberOfPayments) - 1);

        return balance;
    }

    public static double calculateMortgage(
            int principal,
            float annualInterest,
            byte years) {

        double mortgage;

        float monthlyInterest = annualInterest / PERCENT / MONTHS_IN_YEAR;
        float numberOfPayments = years * MONTHS_IN_YEAR;
        mortgage = principal
                * (monthlyInterest * Math.pow(1 + monthlyInterest, numberOfPayments))
                / (Math.pow(1 + monthlyInterest, numberOfPayments) - 1);

        return mortgage;
    }
}
```

#### Refactoring the Code
```Java
package com.lawjune;

import java.text.NumberFormat;
import java.util.Scanner;

public class Main {

    final static byte MONTHS_IN_YEAR = 12;
    final static byte PERCENT = 100;

    public static void main(String[] args) {

        int principal = (int)readNumber("Principal: ", 1000, 1_000_000);

        float annualInterest = (float) readNumber("Annual Interest Rate: ", 1, 30);
        byte years = (byte) readNumber("Period (Years): ", 5, 40);

        printMortgage(principal, annualInterest, years);
//        System.out.println("Mortgage: " + mortgageFormatted);
        printPaymentSchedule(principal, annualInterest, years);
    }

    private static void printMortgage(int principal, float annualInterest, byte years) {
        double mortgage = calculateMortgage(principal, annualInterest, years);

        String mortgageFormatted = NumberFormat.getCurrencyInstance().format(mortgage);
        System.out.println();
        System.out.println("MORTGAGE");
        System.out.println("--------");
        System.out.println("Monthly Payments: "  + mortgageFormatted);
    }

    private static void printPaymentSchedule(int principal, float annualInterest, byte years) {
        System.out.println();
        System.out.println("PAYMENT SCHEDULE");
        System.out.println("----------------");
        for (short month = 1; month <= years * MONTHS_IN_YEAR; month++) {
            double balance = calculateBalance(principal, annualInterest, years, month);
            System.out.println(NumberFormat.getCurrencyInstance().format(balance));
        }
    }

    public static double readNumber(
            String prompt,
            double min,
            double max) {
        Scanner scanner = new Scanner(System.in);
        double value;
        while (true) {
            System.out.print(prompt);
            value = scanner.nextFloat();

            if ( value >= min && value <= max)
                break;
            System.out.println("Enter a value between " + min + "and " + max);
        }
        return value;
    }

    public static double calculateBalance(
            int principal,
            float annualInterest,
            byte years,
            short numberOfPaymentsMade
    ) {


        float monthlyInterest = annualInterest / PERCENT / MONTHS_IN_YEAR;
        float numberOfPayments = years * MONTHS_IN_YEAR;

        double balance = principal
                * (Math.pow(1 + monthlyInterest, numberOfPayments) - Math.pow(1 + monthlyInterest, numberOfPaymentsMade))
                / (Math.pow(1 + monthlyInterest, numberOfPayments) - 1);

        return balance;
    }

    public static double calculateMortgage(
            int principal,
            float annualInterest,
            byte years) {

        double mortgage;

        float monthlyInterest = annualInterest / PERCENT / MONTHS_IN_YEAR;
        float numberOfPayments = years * MONTHS_IN_YEAR;
        mortgage = principal
                * (monthlyInterest * Math.pow(1 + monthlyInterest, numberOfPayments))
                / (Math.pow(1 + monthlyInterest, numberOfPayments) - 1);

        return mortgage;
    }
}
```

### Summary
- Keep your methods short => <= 20 lines of code
- Extract repetitive patterns 
- Extract highly related statements 

## Debugging and Packaging Java Application

### Types of Errors

- Compile-time Errors = Syntax Errors
- Run-time Errors => Debugger

### Common Syntax Errors

### Debugging 
**Debugging is finding and removing errors in a program**
`ctrl + F8` to add/remove break-point
```java
package com.lawjune;

import java.text.NumberFormat;
import java.util.Scanner;

public class Main {

    public static void main(String[] args) {
        System.out.println("Start");
        printNumbers(4);
        System.out.println("Finish");
    }

    public static void printNumbers(int limit) {
        for (int i = 0; i < limit; i +=2)
            System.out.println(i);
    }

}
```

### Packaging Java Applications
---
Build Artifacts...


# Part 2: Object-Oriented Progamming 

## Programming Paradigms 
- Procedural
- Functional 
- Object-oriented
- Event-driven
- Logic
- Aspect-oriented 

Signle Paradigm:
- SmallTalk(OOP)

Multi Paradigm:
- Python
- Ruby
- Java
- JavaScript

### Object-oriented Programing Benefits 

- Reduced Complexity
- Easier Maintenance
- Code Reuse
- Faster Development

## Classes
- Encapsulation
- Abstraction
- Constuctors 
- Getters / Setters
- Method Overloading

### Classes and Objects

| **Class** | A blueprint for creating objects
| **Object** | An instance of a class

### Creating Classes

*The static method usually called in the main method*

```java
package com.lawjune;

public class TextBox {
    public String text; // Field

// The static method usually called in the main method
    public void setText(String text) {
        this.text = text;
    }

// The static method usually called in the main method   
    public void clear() {
        text = "";
    }
}
```

### Creating Objects
```java
package com.lawjune;

public class Main {

    public static void main(String[] args) {
        TextBox textBox1 = new TextBox();
        textBox1.setText("Box 1");
        System.out.println(textBox1.text);
    }
}
```

***DANGEROUS TO MAKE FIELD PUBLIC***
```Java
package com.lawjune;

public class Main {

    public static void main(String[] args) {
        TextBox textBox1 = new TextBox();
//        textBox1.setText("Box 1");
        System.out.println(textBox1.text.toUpperCase());
    }
}
```

```Java
Exception in thread "main" java.lang.NullPointerException
	at com.lawjune.Main.main(Main.java:8)
```

### Memory Allocation
Java manages two different areas of the memory:
- **HEAP**: Objects
- **STACK**: Primitives and short-lived variables

Primitives -> Objects

```Java
package com.lawjune;

public class Main {

    public static void main(String[] args) {
        TextBox textBox1 = new TextBox();
        textBox1.setText("Box 1");
        System.out.println(textBox1.text.toUpperCase());

        TextBox textBox2 = textBox1; // Referencing to the same object in the heap
        textBox2.setText("Box 2");
        System.out.println(textBox1.text);
    }
}

// Output: 
// BOX 1
// Box 2
```

***Memory Deallocation*** => ***Garbage Collection***
When we exit, a method, Java runtime will immediately remove all the variables that are stored in the stack.

Then there are no references for the objects in the heap, so if there is another process in the background, it is watching these objects on the heap. If it becomes unused for a certain period of time, that process is going to automatically remove that object on the heap. 


### Procedural Programming 
*The symptoms of code written in procedural sytle, you will end up with methods that have so many parameters.*

```Java
package com.lawjune;

public class Main {

    public static void main(String[] args) {
        int baseSalary = 50_000;
        int extraHours = 10;
        int hourlyRate = 20;

        int wage = calculateWage(baseSalary, extraHours, hourlyRate);
        System.out.println(wage);
    }

    public static  int calculateWage(
            int baseSalary,
            int extraHours,
            int hourlyRatae
    ) {
        return baseSalary + (extraHours * hourlyRatae);
    }
}
```

### Encapsulation
***Bundle the data and method operate on the data in a signe unit***

```Java
package com.lawjune;

public class Employee {
    public int baseSalary;
    public int hourlyRate;
//    public int extraHours; // Changed every month

    // The static method usually called in the main method
    public int calculateWage(int extraHours) {
        return baseSalary + (hourlyRate * extraHours);
    }
}
```
```Java
package com.lawjune;

public class Employee {
    public int baseSalary;
    public int hourlyRate;
//    public int extraHours; // Changed every month

    // The static method usually called in the main method
    public int calculateWage(int extraHours) {
        return baseSalary + (hourlyRate * extraHours);
    }
}
```

### Getters and Setters
```Java
package com.lawjune;

public class Main {

    public static void main(String[] args) {

        Employee employee = new Employee();
        if (baseSalary <= 0) ---> Encapsulate this mehod in the Employee class
        employee.baseSalary = -1; // Error Number!!!
        employee.hourlyRate = 20;
        int wage = employee.calculateWage(10);

        System.out.println(wage);
    }
}
```

```Java
package com.lawjune;

public class Main {

    public static void main(String[] args) {

        Employee employee = new Employee();
        employee.setBaseSalary(-1);
        employee.setHourlyRate(20);
        int wage = employee.calculateWage(10);

        System.out.println(wage);
    }
}
```

***Old way to manually create Getters & Setters***
```Java
package com.lawjune;

public class Employee {
    private int baseSalary;
    private int hourlyRate;

    public int calculateWage(int extraHours) {
        return baseSalary + (hourlyRate * extraHours);
    }

    public void setBaseSalary(int baseSalary) {
        if (baseSalary <= 0)
            throw new IllegalArgumentException("Salary can not be 0 or less");
        this.baseSalary = baseSalary;
    }

    public int getBaseSalary() {
        return baseSalary;
    }

    public void setHourlyRate(int hourlyRate) {
        if (hourlyRate <= 0)
            throw new IllegalArgumentException("Hourly Rate can not be 0 or less");
        this.hourlyRate = hourlyRate;
    }

    public int getHourlyRate() {
        return hourlyRate;
    }

}
```

***Trick to ask Intellij to automatically create Getters & Setters*** -> ***Encapsulate the public field***

### Abstraction
***Reduce complexity by hiding unnecessary details***

### Coupling
***The level of dependency between classes***

*If you are playing your phone more than 5 hours per day, or your are using your phone in most of your daily life, which means you are highly depended on your phone.*

*If you have 5 apps in your phone, you have 5 coupling points with your phone. If you have 100 apps in your phone, then you have 100 coupling points with your phone.*

4 coupling points as below Main class depended on Employee class. Less public methods of Employee class, less coupling points in the future.
```Java
package com.lawjune;

public class Main {

    public static void main(String[] args) {

        Employee employee = new Employee();
        employee.setBaseSalary(50_000);
        employee.setHourlyRate(20);
        int wage = employee.calculateWage(10);

        System.out.println(wage);
    }
}
```

### Reducing Coupling
```Java
package com.lawjune;

public class Browser {
    public void navigate(String address) {
        String ip = findIpAddress(address);
        String html = sendHttpRequest(ip);
        System.out.println(html);
    }

    private String sendHttpRequest(String ip) {
        return "<html></html>";
    }

    private String findIpAddress(String address) {
        return "127.0.0.1";
    }
}
```
```Java
package com.lawjune;

public class Main {

    public static void main(String[] args) {
        Browser browser = new Browser();
        browser.navigate("test");
    }
}
```

### Constructors
```Java
package com.lawjune;

public class Main {

    public static void main(String[] args) {
        Employee employee = new Employee();
        // Forget to set the fields!
//        employee.setBaseSalary(50_000);
//        employee.setHourlyRate(20);
        int wage = employee.calculateWage(10);

        System.out.println(wage);
    }
}
```

```Java
package com.lawjune;

public class Employee {
    private int baseSalary;
    private int hourlyRate;

    public Employee(int baseSalary, int hourlyRate) {
        setBaseSalary(baseSalary);
        setHourlyRate(hourlyRate);
    }

    public int calculateWage(int extraHours) {
        return baseSalary + (getHourlyRate() * extraHours);
    }

    private void setBaseSalary(int baseSalary) {
        if (baseSalary <= 0)
            throw new IllegalArgumentException("Salary can not be 0 or less");
        this.baseSalary = baseSalary;
    }

    public int getBaseSalary() {
        return baseSalary;
    }

    public int getHourlyRate() {
        return hourlyRate;
    }

    private void setHourlyRate(int hourlyRate) {
        this.hourlyRate = hourlyRate;
    }

}
```
```Java
package com.lawjune;

public class Main {

    public static void main(String[] args) {
        Employee employee = new Employee(50_000, 20);
        int wage = employee.calculateWage(10);
        System.out.println(wage);
    }
}
```

### Method Overloading

***NOT SUGGESTED DUE TO TINY BENEFIT***
```Java
package com.lawjune;

public class Employee {
    private int baseSalary;
    private int hourlyRate;

    public Employee(int baseSalary, int hourlyRate) {
        setBaseSalary(baseSalary);
        setHourlyRate(hourlyRate);
    }

    public int calculateWage(int extraHours) {
        return baseSalary + (getHourlyRate() * extraHours);
    }

    public int calculateWage() {
        return calculateWage(0);
    }

    private void setBaseSalary(int baseSalary) {
        if (baseSalary <= 0)
            throw new IllegalArgumentException("Salary can not be 0 or less");
        this.baseSalary = baseSalary;
    }

    public int getBaseSalary() {
        return baseSalary;
    }

    public int getHourlyRate() {
        return hourlyRate;
    }

    private void setHourlyRate(int hourlyRate) {
        this.hourlyRate = hourlyRate;
    }

}
```

### Constructor Overloading
```Java
package com.lawjune;

public class Employee {
    private int baseSalary;
    private int hourlyRate;

    public Employee(int baseSalary) {
        this(baseSalary, 0);
    }

    public Employee(int baseSalary, int hourlyRate) {
        setBaseSalary(baseSalary);
        setHourlyRate(hourlyRate);
    }

    public int calculateWage(int extraHours) {
        return baseSalary + (getHourlyRate() * extraHours);
    }

    public int calculateWage() {
        return calculateWage(0);
    }

    private void setBaseSalary(int baseSalary) {
        if (baseSalary <= 0)
            throw new IllegalArgumentException("Salary can not be 0 or less");
        this.baseSalary = baseSalary;
    }

    public int getBaseSalary() {
        return baseSalary;
    }

    public int getHourlyRate() {
        return hourlyRate;
    }

    private void setHourlyRate(int hourlyRate) {
        if (hourlyRate < 0)
            throw new IllegalArgumentException("Hourly Rate can not less than 0!");
        this.hourlyRate = hourlyRate;
    }

}
```

### Static Methods

***Instance Members VS Static Members*** 

We use the static methods in situation where present a concept that should be in a single place.

```Java
package com.lawjune;

public class Employee {
    private int baseSalary;
    private int hourlyRate;

    public static int numberOfEmployees;

    public static void printNumberOfEmployees() {
        System.out.println(numberOfEmployees);
    }

    public Employee(int baseSalary) {
        this(baseSalary, 0);
    }

    public Employee(int baseSalary, int hourlyRate) {
        setBaseSalary(baseSalary);
        setHourlyRate(hourlyRate);
        numberOfEmployees++;
    }

    public int calculateWage(int extraHours) {
        return baseSalary + (getHourlyRate() * extraHours);
    }

    public int calculateWage() {
        return calculateWage(0);
    }

    private void setBaseSalary(int baseSalary) {
        if (baseSalary <= 0)
            throw new IllegalArgumentException("Salary can not be 0 or less");
        this.baseSalary = baseSalary;
    }

    public int getBaseSalary() {
        return baseSalary;
    }

    public int getHourlyRate() {
        return hourlyRate;
    }

    private void setHourlyRate(int hourlyRate) {
        if (hourlyRate < 0)
            throw new IllegalArgumentException("Hourly Rate can not less than 0!");
        this.hourlyRate = hourlyRate;
    }

}
```


## Refactoring to an Object-oriented Design

### What class do we need? - Assign by responsibilities

A `Console` class for the interaction with console
```Java
        int principal = (int)readNumber("Principal: ", 1000, 1_000_000);
        float annualInterest = (float) readNumber("Annual Interest Rate: ", 1, 30);
        byte years = (byte) readNumber("Period (Years): ", 5, 40);
```

A class kind of `MortgageReport`
```Java
    private static void printMortgage(int principal, float annualInterest, byte years) {
        double mortgage = calculateMortgage(principal, annualInterest, years);

        String mortgageFormatted = NumberFormat.getCurrencyInstance().format(mortgage);
        System.out.println();
        System.out.println("MORTGAGE");
        System.out.println("--------");
        System.out.println("Monthly Payments: "  + mortgageFormatted);
    }

    private static void printPaymentSchedule(int principal, float annualInterest, byte years) {
        System.out.println();
        System.out.println("PAYMENT SCHEDULE");
        System.out.println("----------------");
        for (short month = 1; month <= years * MONTHS_IN_YEAR; month++) {
            double balance = calculateBalance(principal, annualInterest, years, month);
            System.out.println(NumberFormat.getCurrencyInstance().format(balance));
        }
    }
```

***Each class should have single responsibility***

### Extracting Console

***Safe refactoring way in Intellij***

Automatically genenated and modified the corresponding interfaces in Main class:
```Java
package com.lawjune;

import java.util.Scanner;

public class Console {
    public static double readNumber(
            String prompt,
            double min,
            double max) {
        Scanner scanner = new Scanner(System.in);
        double value;
        while (true) {
            System.out.print(prompt);
            value = scanner.nextFloat();

            if ( value >= min && value <= max)
                break;
            System.out.println("Enter a value between " + min + "and " + max);
        }
        return value;
    }
}
```

### Overloading Methods
```Java
package com.lawjune;

import java.util.Scanner;

public class Console {

    private static Scanner scanner = new Scanner(System.in);

    public static double readNumber(String prompt) {
        return scanner.nextDouble();
    }

    public static double readNumber(
            String prompt,
            double min,
            double max) {
//        Scanner scanner = new Scanner(System.in);
        double value;
        while (true) {
            System.out.print(prompt);
            value = scanner.nextFloat();

            if ( value >= min && value <= max)
                break;
            System.out.println("Enter a value between " + min + "and " + max);
        }
        return value;
    }
}
```

### Etracting the MortgageReport Class

***Safe refactoring way in Intellij***

```Java
package com.lawjune;

import java.text.NumberFormat;

public class MortgageReport {
    public static void printMortgage(int principal, float annualInterest, byte years) {
        double mortgage = Main.calculateMortgage(principal, annualInterest, years);

        String mortgageFormatted = NumberFormat.getCurrencyInstance().format(mortgage);
        System.out.println();
        System.out.println("MORTGAGE");
        System.out.println("--------");
        System.out.println("Monthly Payments: "  + mortgageFormatted);
    }

    public static void printPaymentSchedule(int principal, float annualInterest, byte years) {
        System.out.println();
        System.out.println("PAYMENT SCHEDULE");
        System.out.println("----------------");
        for (short month = 1; month <= years * Main.MONTHS_IN_YEAR; month++) {
            double balance = Main.calculateBalance(principal, annualInterest, years, month);
            System.out.println(NumberFormat.getCurrencyInstance().format(balance));
        }
    }
}
```


### Etracting the MortgageCalculator Class

***Safe refactoring way in Intellij***
***Several refactoring skills in Intellij***
```Java
package com.lawjune;

public class MortgageCalculator {

    private int principal;
    private float annualInterest;
    private byte years;
//    private short numberOfPaymentsMade;


    public MortgageCalculator(int principal, float annualInterest, byte years) {
        this.principal = principal;
        this.annualInterest = annualInterest;
        this.years = years;
    }

    public double calculateBalance(short numberOfPaymentsMade) {

        float monthlyInterest = annualInterest / Main.PERCENT / Main.MONTHS_IN_YEAR;
        float numberOfPayments = years * Main.MONTHS_IN_YEAR;

        double balance = principal
                * (Math.pow(1 + monthlyInterest, numberOfPayments) - Math.pow(1 + monthlyInterest, numberOfPaymentsMade))
                / (Math.pow(1 + monthlyInterest, numberOfPayments) - 1);

        return balance;
    }

    public double calculateMortgage() {

        double mortgage;

        float monthlyInterest = annualInterest / Main.PERCENT / Main.MONTHS_IN_YEAR;
        float numberOfPayments = years * Main.MONTHS_IN_YEAR;
        mortgage = principal
                * (monthlyInterest * Math.pow(1 + monthlyInterest, numberOfPayments))
                / (Math.pow(1 + monthlyInterest, numberOfPayments) - 1);

        return mortgage;
    }
}
```

```Java
package com.lawjune;

import java.text.NumberFormat;

public class MortgageReport {

    private static MortgageCalculator calculator;

    public static void printMortgage(int principal, float annualInterest, byte years) {
        calculator = new MortgageCalculator(principal, annualInterest, years);
        double mortgage = calculator.calculateMortgage();

        String mortgageFormatted = NumberFormat.getCurrencyInstance().format(mortgage);
        System.out.println();
        System.out.println("MORTGAGE");
        System.out.println("--------");
        System.out.println("Monthly Payments: "  + mortgageFormatted);
    }

    public static void printPaymentSchedule(int principal, float annualInterest, byte years) {
        calculator = new MortgageCalculator(principal, annualInterest, years);
        System.out.println();
        System.out.println("PAYMENT SCHEDULE");
        System.out.println("----------------");
        for (short month = 1; month <= years * Main.MONTHS_IN_YEAR; month++) {
            double balance = calculator.calculateBalance(month);
            System.out.println(NumberFormat.getCurrencyInstance().format(balance));
        }
    }
}
```

### Moving Away from Static Members
***We should use the static method in a single place***
```Java
package com.lawjune;

import java.text.NumberFormat;

public class MortgageReport {

    private MortgageCalculator calculator;

    public MortgageReport(MortgageCalculator calculator) {
        this.calculator = calculator;
    }

    public void printPaymentSchedule() {
        System.out.println();
        System.out.println("PAYMENT SCHEDULE");
        System.out.println("----------------");
        for (short month = 1; month <= calculator.getYears() * Main.MONTHS_IN_YEAR; month++) {
            double balance = calculator.calculateBalance(month);
            System.out.println(NumberFormat.getCurrencyInstance().format(balance));
        }
    }

    public void printMortgage() {
        double mortgage = calculator.calculateMortgage();

        String mortgageFormatted = NumberFormat.getCurrencyInstance().format(mortgage);
        System.out.println();
        System.out.println("MORTGAGE");
        System.out.println("--------");
        System.out.println("Monthly Payments: "  + mortgageFormatted);
    }
}
```

```Java
package com.lawjune;

public class Main {

    final static byte MONTHS_IN_YEAR = 12;
    final static byte PERCENT = 100;

    public static void main(String[] args) {

        int principal = (int) Console.readNumber("Principal: ", 1000, 1_000_000);

        float annualInterest = (float) Console.readNumber("Annual Interest Rate: ", 1, 30);
        byte years = (byte) Console.readNumber("Period (Years): ", 5, 40);

        MortgageCalculator calculator = new MortgageCalculator(principal, annualInterest, years);
        MortgageReport report = new MortgageReport(calculator);
        report.printMortgage();
        report.printPaymentSchedule();
    }

}
```

### Moving Static Fields
```Java
package com.lawjune;

public class MortgageCalculator {

    public final static byte MONTHS_IN_YEAR = 12;
    public final static byte PERCENT = 100;
    private int principal;
    private float annualInterest;
    private byte years;
//    private short numberOfPaymentsMade;


    public MortgageCalculator(int principal, float annualInterest, byte years) {
        this.principal = principal;
        this.annualInterest = annualInterest;
        this.years = years;
    }

    public double calculateBalance(short numberOfPaymentsMade) {

        float monthlyInterest = annualInterest / PERCENT / MONTHS_IN_YEAR;
        float numberOfPayments = years * MONTHS_IN_YEAR;

        double balance = principal
                * (Math.pow(1 + monthlyInterest, numberOfPayments) - Math.pow(1 + monthlyInterest, numberOfPaymentsMade))
                / (Math.pow(1 + monthlyInterest, numberOfPayments) - 1);

        return balance;
    }

    public double calculateMortgage() {

        double mortgage;

        float monthlyInterest = annualInterest / PERCENT / MONTHS_IN_YEAR;
        float numberOfPayments = years * MONTHS_IN_YEAR;
        mortgage = principal
                * (monthlyInterest * Math.pow(1 + monthlyInterest, numberOfPayments))
                / (Math.pow(1 + monthlyInterest, numberOfPayments) - 1);

        return mortgage;
    }

    public short getYears() {
        return years;
    }
}
```

### Extracting Duplicate Logic

***Refactor -> Extract Method -> Replace All***

```Java
package com.lawjune;

public class MortgageCalculator {

    public final static byte MONTHS_IN_YEAR = 12;
    public final static byte PERCENT = 100;
    private int principal;
    private float annualInterest;
    private byte years;
//    private short numberOfPaymentsMade;


    public MortgageCalculator(int principal, float annualInterest, byte years) {
        this.principal = principal;
        this.annualInterest = annualInterest;
        this.years = years;
    }

    public double calculateBalance(short numberOfPaymentsMade) {

        float monthlyInterest = getMonthlyInterest();
        float numberOfPayments = getNumberOfPayments();

        double balance = principal
                * (Math.pow(1 + monthlyInterest, numberOfPayments) - Math.pow(1 + monthlyInterest, numberOfPaymentsMade))
                / (Math.pow(1 + monthlyInterest, numberOfPayments) - 1);

        return balance;
    }

    public double calculateMortgage() {

        double mortgage;

        float monthlyInterest = getMonthlyInterest();
        float numberOfPayments = getNumberOfPayments();
        mortgage = principal
                * (monthlyInterest * Math.pow(1 + monthlyInterest, numberOfPayments))
                / (Math.pow(1 + monthlyInterest, numberOfPayments) - 1);

        return mortgage;
    }

    private int getNumberOfPayments() {
        return years * MONTHS_IN_YEAR;
    }

    private float getMonthlyInterest() {
        return annualInterest / PERCENT / MONTHS_IN_YEAR;
    }

    public short getYears() {
        return years;
    }
}
```

### Extracting getRemainingBalances - Separating Calculation from Presentation Logics

```Java
package com.lawjune;

import java.text.NumberFormat;

public class MortgageReport {

    private MortgageCalculator calculator;

    public MortgageReport(MortgageCalculator calculator) {
        this.calculator = calculator;
    }

    public void printPaymentSchedule() {
        System.out.println();
        System.out.println("PAYMENT SCHEDULE");
        System.out.println("----------------");
        for(double balance : calculator.getRemainingBalances())
            System.out.println(NumberFormat.getCurrencyInstance().format(balance));
//        for (short month = 1; month <= calculator.getYears() * MortgageCalculator.MONTHS_IN_YEAR; month++) {
//            double balance = calculator.calculateBalance(month);
//            System.out.println(NumberFormat.getCurrencyInstance().format(balance));
//        }
    }

    public void printMortgage() {
        double mortgage = calculator.calculateMortgage();

        String mortgageFormatted = NumberFormat.getCurrencyInstance().format(mortgage);
        System.out.println();
        System.out.println("MORTGAGE");
        System.out.println("--------");
        System.out.println("Monthly Payments: "  + mortgageFormatted);
    }
}
```

```Java
package com.lawjune;

public class MortgageCalculator {

    private final static byte MONTHS_IN_YEAR = 12;
    private final static byte PERCENT = 100;
    private int principal;
    private float annualInterest;
    private byte years;
//    private short numberOfPaymentsMade;


    public MortgageCalculator(int principal, float annualInterest, byte years) {
        this.principal = principal;
        this.annualInterest = annualInterest;
        this.years = years;
    }

    public double calculateBalance(short numberOfPaymentsMade) {

        float monthlyInterest = getMonthlyInterest();
        float numberOfPayments = getNumberOfPayments();

        double balance = principal
                * (Math.pow(1 + monthlyInterest, numberOfPayments) - Math.pow(1 + monthlyInterest, numberOfPaymentsMade))
                / (Math.pow(1 + monthlyInterest, numberOfPayments) - 1);

        return balance;
    }

    public double calculateMortgage() {

        double mortgage;

        float monthlyInterest = getMonthlyInterest();
        float numberOfPayments = getNumberOfPayments();
        mortgage = principal
                * (monthlyInterest * Math.pow(1 + monthlyInterest, numberOfPayments))
                / (Math.pow(1 + monthlyInterest, numberOfPayments) - 1);

        return mortgage;
    }

    public double[] getRemainingBalances() {
        double[] balances = new double[getNumberOfPayments()];
        for (short month = 1; month <= balances.length; month++)
            balances[month - 1] = calculateBalance(month);

        return balances;
    }

    private int getNumberOfPayments() {
        return years * MONTHS_IN_YEAR;
    }

    private float getMonthlyInterest() {
        return annualInterest / PERCENT / MONTHS_IN_YEAR;
    }
}
```

### One Last Touch

```Java
package com.lawjune;

import java.text.NumberFormat;

public class MortgageReport {

    private final NumberFormat currency;
    private MortgageCalculator calculator;

    public MortgageReport(MortgageCalculator calculator) {
        this.calculator = calculator;
        currency = NumberFormat.getCurrencyInstance();
    }

    public void printPaymentSchedule() {
        System.out.println();
        System.out.println("PAYMENT SCHEDULE");
        System.out.println("----------------");
        for(double balance : calculator.getRemainingBalances())
            System.out.println(currency.format(balance));
//        for (short month = 1; month <= calculator.getYears() * MortgageCalculator.MONTHS_IN_YEAR; month++) {
//            double balance = calculator.calculateBalance(month);
//            System.out.println(NumberFormat.getCurrencyInstance().format(balance));
//        }
    }

    public void printMortgage() {
        double mortgage = calculator.calculateMortgage();

        String mortgageFormatted = currency.format(mortgage);
        System.out.println();
        System.out.println("MORTGAGE");
        System.out.println("--------");
        System.out.println("Monthly Payments: "  + mortgageFormatted);
    }
}
```

## Inheritance 

### The Object Class

### Constructors and Inheritance

### Access Modifier

Avoiding `protected` and default access, just declare with `private` and `public`.

### Overriding Methods

Don't confuse this with `method overloading`, `method overloading` means declaring a method multiple times but with different signatures, different parameters. 

```Java
package com.lawjune;

public class Main {

    public static void main(String[] args) {
        TextBox textBox = new TextBox();
        textBox.setText("Hello World");
        System.out.println(textBox);
    }

}
```
The print-line method automatically calls the two string method automatically on any object that we pass here.

### Upcasting and Downcasting

- **Upcasting:** Casting an object to one of its **super** types

- **Downcasting:** Casting an onject to one of its **sub** types

```Java
package com.lawjune;

public class Main {

    public static void main(String[] args) {

        UIControl control = new UIControl(true);
        TextBox textBox = new TextBox();
        show(textBox);
    }

    public static void show (UIControl control) {

        TextBox textBox = (TextBox)control;
        textBox.setText("Hello World");

        System.out.println(control);
    }

}
```

```Java
package com.lawjune;

public class Main {

    public static void main(String[] args) {

        UIControl control = new UIControl(true);
        TextBox textBox = new TextBox();
        show(control);
    }

    public static void show (UIControl control) {

        if (control instanceof TextBox) {
            TextBox textBox = (TextBox) control;
            textBox.setText("Hello World");
        }

        System.out.println(control);
    }

}
```

### Comparing Objects
```Java
package com.lawjune;

import java.util.Objects;

public class Point {

    private int x;
    private int y;

    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }

    @Override
    public boolean equals(Object o) {
        // return super.equals(o);

        if (this == o)
            return true;

        if (!(o instanceof Point))
            return false;

        Point other = (Point)o;
        return other.x == x && other.y == y;
    }

    @Override
    public int hashCode() {
        // return super.hashCode();
        return Objects.hash(x, y);
    }
}
```

## Polymorphism

Poly-morph-sim
Many-Form

```Java
package com.lawjune;

public class Main {

    public static void main(String[] args) {
        UIControl[] controls = { new TextBox(), new CheckBox()};
        for (UIControl control : controls) {

            // Procedure programing as below will end-up a big fat if statement
            // if control is TextBox
            //    renderTextBox
            // else if it is a CheckBox
            //    renderCheckBox

            control.render();
        }
    }

}
```

### Absctract Classes and Methods

```Java
package com.lawjune;

public abstract class UIControl {

    private boolean isEnabled = true;

    public void enable() {
        isEnabled = true;
    }

//    public UIControl() {
//        System.out.println("UIControl");
//    }

//    public UIControl(boolean isEnabled) {
//        this.isEnabled = isEnabled;
//    }

    public abstract void render();

    public void disable() {
        isEnabled = false;
    }

    public boolean isEnabled() {
        return isEnabled;
    }
}
```

### Final Classes and Methods

We use ***final classes*** in situations where we are 100% sure of the implementation of the class and we want to prevent other classes from extending that class.

***String Class***
Because strings in Java are immutable. So once we create an initialized *String*, we cannot change it's context, if we call any of it's method, like two uppercase or two lowercase, we'll get a new string. 

**People who have implemented the String class have made sure that every method that modifies a string object will in fact return a new instance. That is the reason why they've declared this class as final, so we wouldn't accidently extend this class and wreck this assumption.** 

We use final ***final methods*** in situations where again, we have made certain assumption, they've changing the state of the class in the particular way, we don't want the subclasses to accidentally change this behavior or wreck our assumptions.

### Deep Inheritance Hierachies
*Too many good things are bad things!*
***Don't create deep inheritance hierachies!***
***No more than 3 levels!***

### Multiple Inheritance


## Interfaces

### What are Interfaces?

*We use interface to build loosely-coupled, extensible, testable applications.*

***Abstraction*** => **Hide the implementation details**

An interface is a type similar to a class, but it only includes method declarations, no implementations, it has no code, it only defines the **capabilities** that a class should have. 

Let me give you an analogy, imagine you have a restaurant, you need a chef, you don't care who the chef if as long as they have certain **capabilities**.

Another analogy, your phone needs an input for the charger. This input defines interface. You can use any charger that follows the interface or contract. As long as the size fits, you can use it to charge your phone.

***Interface*** == **What** should be done
- Data compression
- Encryption
- Sorting
- Searching


***Class*** == **How** it should be done

Example: Calculating the tax
- Interface specifies what should be done, which is calculating the tax. 
- (Different) Class will provide different ways for calculating the tax. 

***We use interface to build loosely-coupled, extensible, testable applications.***

### Tightly-coupled Code

```Java
package com.lawjune;

public class TaxCalculator {

    private double taxableIncome;

    public TaxCalculator(double taxableIncome) {
        this.taxableIncome = taxableIncome;
    }

    public double calculateTax() {
        return taxableIncome * 0.3;
    }
}
```

```Java
package com.lawjune;

public class TaxReport {

    private TaxCalculator calculator;

    public TaxReport() {
        calculator = new TaxCalculator(100_000);
    }

    public void show() {
        double tax = calculator.calculateTax();
        System.out.println(tax);
    }
}
```

### Creating an Interface

```Java
package com.lawjune;

public interface TaxCalculator {
    double calculateTax();
}
```

```Java
package com.lawjune;


public class TaxCalculator2020 implements TaxCalculator {

    private double taxableIncome;

    public TaxCalculator2020(double taxableIncome) {
        this.taxableIncome = taxableIncome;
    }

    @Override
    public double calculateTax() {
        return taxableIncome * 0.4;
    }
}
```

### Dependency Injection

***Our Classes should not instantiate their dependencies.***

- Constructor Injection
- Setter Injection
- Method Injection

#### Constructor Injection
```Java
package com.lawjune;


public class TaxCalculator2020 implements TaxCalculator {

    private double taxableIncome;

    public TaxCalculator2020(double taxableIncome) {
        this.taxableIncome = taxableIncome;
    }

    @Override
    public double calculateTax() {
        return taxableIncome * 0.4;
    }
}
```


```Java
package com.lawjune;

public class Main {

    public static void main(String[] args) {
        TaxCalculator calculator = new TaxCalculator2020(100_000);
        TaxReport report = new TaxReport(calculator);
        report.show();
    }

}
```
The way we inject this dependency here, is waht we call poor mans dependency injection. In this simple program we have only two classes, so we can easily create and inject these dependencies by hand. 

In larger application, you might hundreds of classes, and these classes might have several dependencies. You don't want to create hundreds of objects in your main method and pass them to the constructor of your classes, that's where we use a dependency injection framework. So there are frameworks out there that make it really easy to pass these dependencies to our classes. **Spring** is one of the popular ones. 


### Setter Injection

The benefit is we can change these dependencies throughout the lifetime of our program.


#### Method Injection

```Java
package com.lawjune;

public class TaxReport {

    private TaxCalculator calculator;

//    public TaxReport(TaxCalculator calculator) {
//        this.calculator = calculator;
//    }

    public void show(TaxCalculator calculator) {
        double tax = calculator.calculateTax();
        System.out.println(tax);
    }

//    public void setCalculator(TaxCalculator calculator) {
//        this.calculator = calculator;
//    }
}
```

### Interface Segregation Principle

***Divide big interfaces into smaller ones***

### Don't Use Field of Interface

### Don't Use Static Method of Interface

### Don't Use Private Method of Interface

### Interface vs Abstract Class

- Interface (contracts): To build loosely-coupled extensible, testable applications
- Abstract Class (Partially-completed Class): To share code between a few classes.

### When to Use Interface

- To decouple a class from it's dependencies, and this gives you number of benefits:

1. **Swap Implementation:** You can easily solve one implementation with antoher.

2. **Extend Your Applications:** You can easily extend your applications with minimal impact.

3. **Test Your Application in Isolation** 

***Don't just blindly write code and follow these so called best practices because soomeone told you to do so. For every piece of code you write you need to understand the problem you're tring to solve. If you're not solving any problems, you're just wasting your times, you're not adding any values, in fact your increasing the costs, because the more code you write, the more bugs you're going to create and the maintenance of your applications is going to be more costly.***


# Part 3 Advanced Topics

## Exceptions
- Exceptions
- Types of Exceptions
- Handling Exceptions
- Custom Exceptions
- Chaining Exceptions

### What are Exceptions?

### Types of Exceptions

- **Checked**: Dveloper should anticipate it and handle it appropriately, check by conmplier. 

- **Unchecked**: Run-time exception, not checked by the complier or compling time due to programming errors.
	- NullPointerException
	- ArithmeticException
	- IllegalArgumentException
	- IndexOutOfBoundsException
	- IllegalStateException

- **Error**: 

### Exceptions Hierarchy

To search Java documentation.

### Catching Exceptions

### The finally block

### The try-with-resources Statement

### Throwing Exceptions

### Re-throwing Exceptions

### Custom Exception

### Chaining Exceptions


## Generics

### The Need for Generics
Creating a class for storing a list of integer.

```Java
package com.lawjune.generics;

public class List {
	private int[] items = new int[10]; 
	// Shouldn't hard-coded the length of array here
	// Should make it as a parameter in the constuctor
	private int count;

	public void add(int item) {
		item[count++] = item;
	}

	public int get(int index) {
		return items[index];
	}
}
```

```Java
package com.lawjune;

public class Main {
    public static void main(String[] args) {
    	List list = new List();
    	list.add(1); 
    }
}
```
Let's say tomorrow we need a list of users.
1. Add a new class in the *generics* pacakge.
2. Problem in the **List cCass** which can only store integer items.
3. To create a **UserList Class**.

```Java
package com.lawjune.generics;

public class UserList {
  private User[] items = new User[10];
  private int count;
}
```

***Very bad solution!***


### A Poor Solution 

```Java
package com.lawjune.generics;

public class List {
	private Object[] items = new Object[10]; 
	private int count;

	public void add(Object item) {
		item[count++] = item;
	}

	public Object get(int index) {
		return items[index];
	}
}
```

```Java
package com.lawjune;

public class Main {
    public static void main(String[] args) {
    	List list = new List();
    	list.add(1); // Compiled as below
    	list.add(Integer.valueOf(1));

    	list.add("1");
    	list.add(new User());

    	// The 1st problem
    	int number = (int)list.get(0);

    	// The 2nd problem: invalid variable cast
    	int number = (int)list.get(1); 
    	// Throw ClassCastException 

    }
}
```

### Generic Classes

***<T>*** short for ***Type*** or ***Template***
- It doesn't have to use ***<T>***, but ***<T>*** is the common convension.
- ***<E>*** short for ***Element*** 

The ***<T>*** here will represent the type of objects we are going to store here.

When we instanciate a class of this, we have to specify the argurement of ***<T>***.

```Java
package com.lawjune.generics;

public class GenericList<T> {
	private T[] items = (T[]) new Object[10];
	private int count;

	public void add(T item) {
		items[count++] = item;
	}

	public T get(int index) {
		return items[index];
	}

}
```

```Java
package com.lawjune;

public class Main {
    public static void main(String[] args) {
    GenericList<Integer> list = new GenericList<Integer>()
    list.add(1);
    int number = list.get(0)
    }
}
```

### Generic and Primtive Types

Wrapper class for primitive types:
- int -> Integer
- float -> Float
- boolean -> Boolean

```Java
package com.lawjune;

public class Main {
    public static void main(String[] args) {
    GenericList<Integer> numbers = new GenericList<>()
    numbers.add(1); // Boxing => JVM will automatically put thr primitive int inside the box 
    int number = numbers.get(0); // Unboxing 
    }
}
```

### Constraints
```Java
package com.lawjune.generics;

public class GenericList<T extends Number> {
	private T[] items = (T[]) new Object[10];
	private int count;

	public void add(T item) {
		items[count++] = item;
	}

	public T get(int index) {
		return items[index];
	}

}
```

Search *java number class* for Java documentation to check the wrapper class as **Direct Know Subclasses** of ***Number Class***.


Use interface as contraint
```Java
package com.lawjune.generics;

public class GenericList<T extends Comparable> {
	private T[] items = (T[]) new Object[10];
	private int count;

	public void add(T item) {
		items[count++] = item;
	}

	public T get(int index) {
		return items[index];
	}

}
```

```Java
package com.lawjune.generics;

public class User implements Comparable<User> {
	...
}
```

```Java
package com.lawjune;

public class Main {
    public static void main(String[] args) {
    GenericList<User> users = new GenericList<User>()
    users.add(new User()); // Boxing => JVM will automatically put thr primitive int inside the box 
    User user = users.get(0); // Unboxing 
    }
}
```

### Type Erasure

Per the **Byte-code**, the JVM will replace all of the ***<T>*** with ***Object Class***.

The eventual type of <T> will be specified during the instanciation of runtime. 

If ***<T extends Number>***, the JVM will replace all of the ***<T>*** with ***Number Class***.

If ***<T extends Comparable & Clonable>***, the JVM will replace all of the ***<T>*** with ***Comparable Class*** (the left most one).

### The Comparable Interfacce
A lot of sorting algorithms are based on **Comparing Objects**, the these comparison will be determined what object should come first? 

```Java
package com.lawjune.generics;

public class User implements Comparable<User> {
  private int points;

  public User(int points) {
    this.points = points;
  }

  @Override
  public int compareTo(User other) {

    return points - other.points;
  }

  @Override
  public String toString() {
    return "Points=" + points;
  }

}
```

```Java
package com.lawjune;

public class Main {
    public static void main(String[] args) {
    	User user1 = new User(10);
    	User user2 = new User(20);
    	if (user1.compareTo(user2) < 0)
    		System.out.println("user1 < user2");
    	else if (user1.compareTo(user2) == 0)
    		System.out.println("user1 == user2");
    	else
    		System.out.println("user1 > user2");
}
```

### Generic Methods

```Java
package com.lawjune.generics;

public class Utils {
  public static <T extends Comparable<T>> T max(T first, T second) {
    return (first.compareTo(second) < 0) ? second : first;
  }
}
```

```Java
package com.lawjune;

import com.lawjune.generics.Utils;

public class Main {
    public static void main(String[] args) {
        int max = Utils.max(1, 2);
        System.out.println(max);
    }
}
```

### Multiple Type Parameters
```Java
package com.lawjune.generics;

public class Utils {
  public static <K, V> void print(K key, V value) {
    System.out.println(key + "=" + value);
  }
}
```

```Java
package com.lawjune.generics;

public class KeyValuePair<K, V> {
  private K key;
  private V value;

  public KeyValuePair(K key, V value) {
    this.key = key;
    this.value = value;
  }
}
```

### Generic Classes and Inheritance

```Java
package com.lawjune.generics;

public class Instructor extends User {
  public Instructor(int points) {
    super(points);
  }
}
```

```Java
package com.lawjune.generics;

public class Utils {

  public static void printUser(User user) {
    System.out.println(user);
  }

  public static void printUsers
        (GenericList<User> users) {
  }
}
```

```Java
package com.lawjune;

import com.lawjune.generics.Utils;

public class Main {
    public static void main(String[] args) {
    	var instructors = new GenericList<Instructor>();
    	var users = new GenericList<User>();

    	Utils.printUsers(users); 
    }
}
```

A ***GenericList<Instructor>*** is not a subtype of ***GenericList<User>***.

### Wildcart

When you want to use the ***get()***
```Java
package com.lawjune.generics;

public class Utils {
  public static void printUsers
        (GenericList<? extends User> users) {
    User x = users.get(0);
  }
}
```

When you want to use the ***add()***
```Java
package com.lawjune.generics;

public class Utils {

  // class CAP#1 {}
  public static void printUsers
        (GenericList<? super User> users) {

    // When we changed the "extends" to "super"
	// JVM will see the input user object as 
    GenericList<Object> temp = new GenericList<>();


    Object x = users.get(0);
    users.add()
  }
}
```

## Collections Framework

Iterable
Collection
List|Queue|Set
ArrayList|PriorityQueue|HashSet
LinkedList|

### The Need for Iterables
```Java
package com.lawjune;

import com.lawjune.generics.GenericList;

public class Main {
    public static void main(String[] args) {
        var list = new GenericList<String>();
        list.add("a");
        list.add("b");
        for (var item : list.items) // Have to expose items[] as publick
            System.out.println(item);
    }
}
```

### The Iterable Interface

```Java
package com.lawjune.generics;

import java.util.Iterator;

public class GenericList<T> implements Iterable<T> {
  private T[] items = (T[]) new Object[10];
  private int count;

  public void add(T item) {
    items[count++] = item;
  }

  public T get(int index) {
    return items[index];
  }

  @Override
  public Iterator<T> iterator() {
    return new ListIterator(this);
  }

  private class ListIterator implements Iterator<T> {
    private GenericList<T> list;
    private int index;

    public ListIterator(GenericList<T> list) {
      this.list = list;
    }

    @Override
    public boolean hasNext() {
      return (index < list.count);
    }

    @Override
    public T next() {
      return list.items[index++];
    }
  }
}

```

```Java
package com.lawjune;

import com.lawjune.generics.GenericList;

import java.util.Iterator;

public class Main {
    public static void main(String[] args) {
        GenericList<String> list = new GenericList<>();
        list.add("a");
        list.add("b");

        Iterator<String> iterator = list.iterator();

        while (iterator.hasNext()) {
            String current = iterator.next();
            System.out.println(current);
        }

        for (String item : list)
            System.out.println(item);

    }
}
```

### The Collection Interface 
```Java
package com.lawjune;

import com.lawjune.collections.CollectionDemo;
import com.lawjune.generics.GenericList;

import java.util.ArrayList;
import java.util.Collection;
import java.util.Collections;
import java.util.Iterator;

public class Main {
    public static void main(String[] args) {
        Collection<String> collection = new ArrayList<>();
//        collection.add("a");
//        collection.add("b");
//        collection.add("c");
        Collections.addAll(collection, "a", "b", "c");
        for (String item : collection)
            System.out.println(item);
        collection.remove("a");
        System.out.println(collection);
        System.out.println(collection.contains('a'));
        System.out.println(collection.isEmpty());

        String[] strings = collection.toArray(new String[3]);
        System.out.println(strings[0]);
    }

}
```

### The List Interface

```Java
package com.lawjune.collections;

import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class ListDemo {
  public static void show() {
    List<String> list = new ArrayList<>();
    list.add("a");
    list.add("b");
    list.add("c");

    // Add an item at a given index
    list.add(0, "!");

    // We can add multiple items in one go
    Collections.addAll(list, "a", "b", "c");

    String first = list.get(0);
    list.set(0, "!!");

    list.remove(0);

    int index = list.indexOf("a");
    int lastIndex = list.lastIndexOf("a");

    System.out.println(list.subList(0, 2));
  }
}
```

### The Comparable Interface 
```Java
package com.lawjune.collections;

public class Customer implements Comparable<Customer> {
  private String name;
  private String email;

  public Customer(String name, String email) {
    this.name = name;
    this.email = email;
  }

  @Override
  public int compareTo(Customer other) {
    return name.compareTo(other.name);
  }

  @Override
  public String toString() {
    return name;
  }

  public String getEmail() {
    return email;
  }

  public void setEmail(String email) {
    this.email = email;
  }
}
```

### Sorting Data by Comparable Interface
```Java
package com.lawjune.collections;

import java.util.Comparator;

public class EmailComparator implements Comparator<Customer> {
  @Override
  public int compare(Customer o1, Customer o2) {
    return o1.getEmail().compareTo(o2.getEmail());
  }
}
```

```Java
package com.lawjune;

import com.lawjune.collections.Customer;
import com.lawjune.collections.EmailComparator;

import java.util.*;

public class Main {
    public static void main(String[] args) {
        List<Customer> customers = new ArrayList<>();
        customers.add(new Customer("b", "b@163.com"));
        customers.add(new Customer("a", "a@163.com"));
        customers.add(new Customer("c", "c@163.com"));
        customers.sort(new EmailComparator());
        System.out.println(customers);
    }

}
```

### The Queue Interface

```Java
package com.lawjune.collections;

import java.util.ArrayDeque;
import java.util.Queue;

public class QueueDemo {
  public static void show() {
    Queue<String> queue = new ArrayDeque<>();
    queue.add("c");
    queue.add("a");
    queue.add("b");

    String front = queue.remove();
//    String front = queue.peek();

//    front = queue.element();

    System.out.println(front);
    System.out.println(queue);

    // We have alternative methods that don't
    // throw an exception:

    // offer() similar to add()
    // poll() similar to remove()
    // peek() similar to element()
  }
}
```

### The Set Interface 
```Java
package com.lawjune;

import java.util.*;

public class Main {
    public static void main(String[] args) {
        Collection<String> collection = new ArrayList<>();
        Collections.addAll(collection, "a", "b", "c", "c");
        Set<String> set = new HashSet<>(collection);
        System.out.println(set); // [a, b, c]
    }

}
```

```Java
package com.lawjune.collections;

import java.util.*;

public class SetDemo {
  public static void show() {
    Set<String> set1 =
      new HashSet<>(Arrays.asList("a", "b", "c"));

    Set<String> set2 =
      new HashSet<>(Arrays.asList("b", "c", "d"));

    // Union
    set1.addAll(set2);

    // Intersection
    set1.retainAll(set2);

    // Difference
    set1.removeAll(set2);
  }
}
```

### Hash Tables

### The Map Interface

```Java
package com.lawjune.collections;

import java.util.HashMap;
import java.util.Map;

public class MapDemo {
  public static void show() {
    Customer c1 = new Customer("a", "e1");
    Customer c2 = new Customer("b", "e2");

    Map<String, Customer> map = new HashMap<>();
    map.put(c1.getEmail(), c1);
    map.put(c2.getEmail(), c2);

    boolean exists = map.containsKey("e1");

    Customer unknown = new Customer("Unknown", "");
    Customer customer = map.get("e1");
    customer = map.getOrDefault("e1", unknown);

    map.replace("e1", new Customer("a++", "e1"));

    for (Object key : map.keySet())
      System.out.println(key);

    for (Object value : map.values())
      System.out.println(value);

    for (Object entry : map.entrySet())
      System.out.println(entry);
  }
}
```

## Functional Technics

### Functional Interfaces
- An interface with a single abstract method
	- Comparable<T>

```Java
package com.lawjune.lambdas;

public interface Printer {
  void print(String message);
}
```

```Java
package com.lawjune.lambdas;

public class ConsolePrinter implements Printer {
  @Override
  public void print(String message) {
    System.out.println(message);
  }
}
```

```Java
package com.lawjune.lambdas;

public class LambdasDemo {
  public static void show() {
  	greet(new ConsolePrinter());
  }

  public static void greet(Printer printer) {
  	printer.print("Hello World")
  }
}
```

### Anonymous Inner Classes

```Java
package com.lawjune.lambdas;

public class LambdasDemo {
  public static void show() {
  	greet(new Printer() {
  		@Override
  		public void print(String message) {
  			System.out.println(message);
  		}
  	});
  }

  public static void greet(Printer printer) {
  	printer.print("Hello World")
  }
}
```

### Lambda Expression

```Java
package com.lawjune.lambdas;

public class LambdasDemo {
  public static void show() {

  	greet(message -> System.out.println(message));
  }

  public static void greet(Printer printer) {
  	printer.print("Hello World")
  }
}
```

### Variable Capture

### Method Reference 
```Java
package com.lawjune.lambdas;

public class LambdasDemo {
  public static void show() {

  	greet(message -> System.out.println(message));
  	greet(System.out::println);

  	// Class/Object::method
  }

  public static void greet(Printer printer) {
  	printer.print("Hello World")
  }
}
```

```Java
package com.lawjune.lambdas;

public class LambdasDemo {
  public static void print(String message) {}

  public static void show() {

  	greet(message -> print(message));
  	greet(LambdasDemo::println);
  }

  public static void greet(Printer printer) {
  	printer.print("Hello World")
  }
}
```

```Java
package com.lawjune.lambdas;

public class LambdasDemo {
  public LambdasDemo(String message) {}

  public static void show() {

  	greet(message -> new LambdasDemo(message));
  	greet(LambdasDemo::new);
  }

  public static void greet(Printer printer) {
  	printer.print("Hello World")
  }
}
```

### Built-in Functional Interfaces

#### The Consumer Interface 
```Java
package com.lawjune.lambdas;

public class LambdasDemo {

  public static void show() {

  	greet(message -> new LambdasDemo(message));
  	greet(LambdasDemo::new);
  }

  public static void greet(Printer printer) {
  	printer.print("Hello World")
  }
}
```

```Java
package com.lawjune.lambdas;

import java.util.*;

public class LambdasDemo {
  public static void show() {
    List<Integer> list = new ArrayList<>();
    Collections.addAll(list, 1, 2, 3);

    // Imperative Programing (for, if/else, switch) => How
    for (int item : list)
      System.out.println(item);

    // Declarative Programming => What 
    list.forEach(item -> System.out.println(item));

  }
}
```

#### The Chaining Consumers
```Java
package com.lawjune.lambdas;

import java.util.*;
import java.util.function.Consumer;

public class LambdasDemo {
  public static void show() {
    List<String> list = new ArrayList<>();
    Collections.addAll(list, "a", "b", "c");

    Consumer<String> print = item -> System.out.println(item);
    Consumer<String> printUpperCase = item -> System.out.println(item.toUpperCase());

    list.forEach(print.andThen(printUpperCase));

    //a
    //A
    //b
    //B
    //c
    //C

  }
}
```

#### The Supplier Interface 

```Java
package com.lawjune.lambdas;

import java.util.function.Supplier;

public class LambdasDemo {
  public static void show() {
    Supplier<Double> getRandom = () -> Math.random();
    Double random = getRandom.get();
    System.out.println(random);
  }
}
```

#### The Function Interface 
```Java
package com.lawjune.lambdas;

import java.util.function.Function;

public class LambdasDemo {
  public static void show() {
    Function<String, Integer> map = str -> str.length();
    int length = map.apply("Sky");
    System.out.println(length);
  }
}
```

### Composing Functions 

```Java
package com.lawjune.lambdas;

import java.util.function.Function;

public class LambdasDemo {
  public static void show() {
    // "key:value"
    // first: "key=value"
    // second: "{key=value}"

    Function<String, String> replaceColon = str -> str.replace(":", "=");
    Function<String, String> addBraces = str -> "{" + str + "}";

    // Declarative Programming
    String result = replaceColon
                      .andThen(addBraces)
                      .apply("key:value");
    System.out.println(result);

    String comResult = addBraces.compose(replaceColon).apply("key:value");
    System.out.println(comResult);
  }
}
```

### The Predicate Interface 
```Java
package com.lawjune.lambdas;

import java.util.function.Predicate;

public class LambdasDemo {
  public static void show() {
    Predicate<String> isLongerThan5 = str -> str.length() > 5;
    boolean result = isLongerThan5.test("Sky");
    System.out.println(result);
  }
}
```

### Combining Predicates
```Java
package com.lawjune.lambdas;

import java.util.function.Predicate;

public class LambdasDemo {
  public static void show() {
    Predicate<String> hasLeftBrace = str -> str.startsWith("{");
    Predicate<String> hasRightBrace = str -> str.endsWith("}");

    Predicate<String> hasLeftAndRightBrace = hasLeftBrace.and(hasRightBrace);

    Predicate<String> hasLeftOrRightBrace = hasLeftBrace.or(hasRightBrace);

  }
}
```

### The BinaryOperator Interface 
```Java
package com.lawjune.lambdas;

import java.util.function.BinaryOperator;
import java.util.function.Function;

public class LambdasDemo {
  public static void show() {
    // a, b -> a + b -> square
    BinaryOperator<Integer> add = (a, b) -> a + b;
    Function<Integer, Integer> sqaure = a -> a * a;

    int result = add.andThen(sqaure).apply(1, 2);
    System.out.println(result); // 9
  }
}
```

### The UniaryOperator Interface 
```Java
package com.lawjune.lambdas;

import java.util.function.UnaryOperator;

public class LambdasDemo {
  public static void show() {
    UnaryOperator<Integer> square = n -> n * n;
    UnaryOperator<Integer> increment = n -> n + 1;

    int result = increment.andThen(square).apply(1);
    System.out.println(result);
  }
}
```

## Streams

### Imperative vs Functional Programming 

***Imperative*** -> **How**
***Declarative*** -> **What**

```SQL
SELECT *
FROM movies
WHERE genre = 1
ORDER BY name
```

***Streams*** -> **To process a collection of data in a declarative way**

```Java
package com.lawjune.streams;

import java.util.ArrayList;
import java.util.List;

public class StreamsDemo {
  public static void show() {
    List<Movie> movies = new ArrayList<>();
    movies.add(new Movie("a", 10));
    movies.add(new Movie("b", 15));
    movies.add(new Movie("c", 20));

    // Imperative Programming
    int count = 10;
    for (Movie movie : movies)
      if (movie.getLikes() > 10)
        count++;

    // Declarative (Functional) Programming
    long count2 =  movies.stream()
            .filter(movie -> movie.getLikes() > 10)
            .count();
  }
}
```

### Creating a Stream

- Froam collections 
```Java
	List list = new ArrayList();
```

- From arrays
```Java
	int[] numbers = { 1, 2, 3 };
	Arrays.stream(numbers) // return a stream
			.forEach(n -> System.out.println(n))
```

- From an arbitray number of objects
```Java
	Stream stream = Stream.generate(() -> Math.random())
	stream
		.limit(3)
		.forEach(n -> System.out.println(n))
```

- Infinite/finite streams
```Java
	Stream.Iterate(1, n -> n + 1)
		.limit(10)
		.forEach(n -> System.out.println(n))
```

### Mapping Elements
```Java
package com.lawjune.streams;

import java.util.ArrayList;
import java.util.List;

public class StreamsDemo {
  public static void show() {
    List<Movie> movies = new ArrayList<>();
    movies.add(new Movie("a", 10));
    movies.add(new Movie("b", 15));
    movies.add(new Movie("c", 20));

    movies.stream()
            .map(movie -> movie.getTitle())
            .forEach(name -> System.out.println(name));
  }
}
```

```Java
package com.lawjune.streams;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.Collections;
import java.util.List;
import java.util.stream.Stream;

public class StreamsDemo {
  public static void show() {
    List<Integer> list1 = new ArrayList<>();
    Collections.addAll(list1, 1, 2, 3);

    List<Integer> list2 = new ArrayList<>();
    Collections.addAll(list2, 4, 5, 6);

    Stream stream = Stream.of(list1, list2);
    stream
            .flatMap(list -> list.stream())
            .forEach(n -> System.out.println(n));
  }
}
```

### Filtering Elements

- ***Intermediate*** 
	- map()
	- filter()

- ***Terminal***
	- forEach()

```Java
	package com.lawjune.streams;

import java.util.ArrayList;
import java.util.List;
import java.util.function.Predicate;

public class StreamsDemo {
  public static void show() {
    List<Movie> movies = new ArrayList<>();
    movies.add(new Movie("a", 10));
    movies.add(new Movie("b", 20));
    movies.add(new Movie("c", 30));

    Predicate<Movie> isPopular = m -> m.getLikes() > 10;

    movies.stream()
//            .filter(movie -> movie.getLikes() > 10)
            filter(isPopular)
            .forEach(m -> System.out.println(m.getTitle()));
  }
}
```

### Slicing a Stream

- limit(n)
- skip(n)
- takeWhile(predicate)
- dropWhile(predicate)

```Java
package com.lawjune.streams;

import java.util.ArrayList;
import java.util.List;

public class StreamsDemo {
  public static void show() {
    List<Movie> movies = new ArrayList<>();
    movies.add(new Movie("a", 10));
    movies.add(new Movie("b", 20));
    movies.add(new Movie("c", 30));

    movies.stream()
            .limit(2)
            .forEach(m -> System.out.println(m.getTitle()));
    // a
    // b
  }
}
```

```Java
package com.lawjune.streams;

import java.util.ArrayList;
import java.util.List;

public class StreamsDemo {
  public static void show() {
    List<Movie> movies = new ArrayList<>();
    movies.add(new Movie("a", 10));
    movies.add(new Movie("b", 20));
    movies.add(new Movie("c", 30));

    movies.stream()
            .skip(2)
            .forEach(m -> System.out.println(m.getTitle()));
    // c
  }
}
```

- 1000 movies
- 10 movies per page
- 3rd page
- skip(20) = skip( ( page -1 ) * pageSize)
- limit(10) = limit(pageSize)
```Java
    movies.stream()
            .skip(20)
            .limit(10)
            .forEach(m -> System.out.println(m.getTitle()));
```

```Java
package com.lawjune.streams;

import java.util.ArrayList;
import java.util.List;

public class StreamsDemo {
  public static void show() {

    var movies = List.of(
            new Movie("a", 10),
            new Movie("b", 20),
            new Movie("c", 30)
    );

    movies.stream()
            .takeWhile(m -> m.getLikes() < 30)
            .forEach(m -> System.out.println(m.getTitle()));
  }
}
```

### Sorting Streams
```Java
package com.lawjune.streams;

import java.util.ArrayList;
import java.util.Comparator;
import java.util.List;

public class StreamsDemo {
  public static void show() {

    var movies = List.of(
            new Movie("b", 10),
            new Movie("a", 20),
            new Movie("c", 30)
    );

    movies.stream()
            .sorted(Comparator.comparing(Movie::getTitle).reversed())
            .forEach(m -> System.out.println(m.getTitle()));
  }
}
```

### Getting Distinct Elements
```Java
package com.lawjune.streams;

import java.util.List;

public class StreamsDemo {
  public static void show() {

    var movies = List.of(
            new Movie("a", 10),
            new Movie("a", 10),
            new Movie("b", 20),
            new Movie("c", 30)
    );

    movies.stream()
            .map(Movie::getLikes)
            .distinct()
            .forEach(System.out::println);
  }
}
```

### Peeking Elements
```Java
package com.lawjune.streams;

import java.util.List;

public class StreamsDemo {
  public static void show() {

    var movies = List.of(
            new Movie("a", 10),
            new Movie("b", 20),
            new Movie("c", 30)
    );

    movies.stream()
            .filter(m -> m.getLikes() > 10)
            .peek(m -> System.out.println("filtered: " + m.getTitle()))
            .map(Movie::getTitle)
            .peek(t -> System.out.println("Mapped: " + t))
            .forEach(System.out::println);
  }
}
```

### Simple Reducer

***INTERMEDIATE***
- map() / flatMap()
- filter()
- limit() / skip()
- limit() / skip()
- sorted()
- distinct()
- peek

***REDUCERS***
- count()
- anyMatch(predicate)
- allMatch(predicate)
- noneMatch(predicate)
- findFirst()
- findMax()
- max(comparator)
- min(comparator)

```Java
package com.lawjune.streams;

import java.util.List;

public class StreamsDemo {
  public static void show() {

    var movies = List.of(
            new Movie("a", 10),
            new Movie("b", 20),
            new Movie("c", 30)
    );

    var result = movies.stream()
            .anyMatch(m -> m.getLikes() > 20);
    System.out.println(result);
  }
}
```

```Java
package com.lawjune.streams;

import java.util.List;

public class StreamsDemo {
  public static void show() {

    var movies = List.of(
            new Movie("a", 10),
            new Movie("b", 20),
            new Movie("c", 30)
    );

    var result = movies.stream()
            .findFirst()
            .get()
            .getTitle();
    System.out.println(result);
  }
}
```

```Java
package com.lawjune.streams;

import java.util.Comparator;
import java.util.List;

public class StreamsDemo {
  public static void show() {

    var movies = List.of(
            new Movie("a", 10),
            new Movie("b", 20),
            new Movie("c", 30)
    );

    var result = movies.stream()
            .max(Comparator.comparing(Movie::getLikes))
            .get()
            .getTitle();
    System.out.println(result);
  }
}
```

```Java
package com.lawjune.streams;

import java.util.List;
import java.util.Optional;

public class StreamsDemo {
  public static void show() {

    var movies = List.of(
            new Movie("a", 10),
            new Movie("b", 20),
            new Movie("c", 30)
    );

    // [10, 20, 30]
    // [30, 30]
    // [60]

//    Optional<Integer> sum = movies.stream()
//            .map(m -> m.getLikes())
//            .reduce((a, b) -> a + b);
//    System.out.println(sum.orElse(0));

    Integer sum = movies.stream()
            .map(m -> m.getLikes())
            .reduce(0, Integer::sum);
    System.out.println(sum);

  }
}
```

### Collectors

```Java
package com.lawjune.streams;

import java.util.List;
import java.util.stream.Collectors;

public class StreamsDemo {
  public static void show() {

    var movies = List.of(
            new Movie("a", 10),
            new Movie("b", 20),
            new Movie("c", 30)
    );

    var resultList = movies.stream()
            .filter(m -> m.getLikes() > 10)
            .collect(Collectors.toList());
    System.out.println("resultList: " + resultList);

    var resultSet = movies.stream()
            .filter(m -> m.getLikes() > 10)
            .collect(Collectors.toSet());
    System.out.println("resultSet: " + resultSet);

    var resultMap = movies.stream()
            .filter(m -> m.getLikes() > 10)
            .collect(Collectors.toMap(Movie::getTitle, Movie::getLikes));
    System.out.println("resultMap: " + resultMap);
  }
}
```

```Java
package com.lawjune.streams;

import java.util.List;
import java.util.function.Function;
import java.util.stream.Collectors;

public class StreamsDemo {
  public static void show() {

    var movies = List.of(
            new Movie("a", 10),
            new Movie("b", 20),
            new Movie("c", 30)
    );
    var resultMap = movies.stream()
            .filter(m -> m.getLikes() > 10)
            .collect(Collectors.toMap(Movie::getTitle, Function.identity()));
    System.out.println("resultMap: " + resultMap);

    var resultSumInt = movies.stream()
            .filter(m -> m.getLikes() > 10)
            .collect(Collectors.summarizingInt(Movie::getLikes));
    System.out.println(resultSumInt); // IntSummaryStatistics{count=2, sum=50, min=20, average=25.000000, max=30}

    var resultJoin = movies.stream()
            .filter(m -> m.getLikes() > 10)
            .map(Movie::getTitle)
            .collect(Collectors.joining(","));
    System.out.println(resultJoin); // "b,c"
  }
}
```

### Grouping Elements
```Java
package com.lawjune.streams;

public enum Genre {
  COMEDY,
  ACTION,
  THRILLER
}
```

```Java
package com.lawjune.streams;

import java.util.List;
import java.util.function.Function;
import java.util.stream.Collectors;

public class StreamsDemo {
  public static void show() {

    var movies = List.of(
            new Movie("a", 10, Genre.THRILLER),
            new Movie("b", 20, Genre.ACTION),
            new Movie("c", 30, Genre.ACTION)
    );

   var resGenre = movies.stream()
            .collect(Collectors.groupingBy(
                    Movie::getGenre,
                    Collectors.mapping(Movie::getTitle, Collectors.joining(","))));
   System.out.println(resGenre); //{ACTION=b,c, THRILLER=a}
  }
}
```

### Partitioning Elements

```Java
package com.lawjune.streams;

import java.util.List;
import java.util.function.Function;
import java.util.stream.Collectors;

public class StreamsDemo {
  public static void show() {

    var movies = List.of(
            new Movie("a", 10, Genre.THRILLER),
            new Movie("b", 20, Genre.ACTION),
            new Movie("c", 30, Genre.ACTION)
    );

    var result = movies.stream()
            .collect(Collectors.partitioningBy
                    (m -> m.getLikes() > 20,
                    Collectors.mapping(Movie::getTitle,
                            Collectors.joining(","))));

    System.out.println(result);
  }
}
```

### Primitive Type Streams
- IntStream
- LongSteam
- DoubleStream

```Java
package com.lawjune.streams;
import java.util.stream.IntStream;

public class StreamsDemo {
  public static void show() {
    IntStream.rangeClosed(1, 5)
            .forEach(System.out::println);
  }
}
```

## Concurrency

### Process & Thread
- A Process is an instance of an application. If you launch a application, the system is loading this application inside a process. 
	- A process contains an image of the application code. 
	- It occupies the corresponding memory. 

```Java
package com.lawjune;

public class Main {

    public static void main(String[] args) {
        System.out.println(Thread.activeCount());
        System.out.println(Runtime.getRuntime().availableProcessors());
    }
}
```

### Starting a Thread 
```Java
package com.lawjune.concurrency;

public class ThreadDemo {
  public static void show() {
    System.out.println(Thread.currentThread().getName());

    for (var i = 0; i < 10; i ++) {
      Thread thread = new Thread(new DownloadFileTask(new DownloadStatus()));
      thread.start();
    }
  }
}
```

### Terminating a Tread 

```Java
    try {
      Thread.sleep(10);
    } catch (InterruptedException e) {
      e.printStackTrace();
```

### Joining Threads

```Java
 package com.lawjune.concurrency;

public class ThreadDemo {
  public static void show() {
    System.out.println(Thread.currentThread().getName());

      Thread thread = new Thread(new DownloadFileTask(new DownloadStatus()));
      thread.start();

    try {
      thread.join();
    } catch (InterruptedException e) {
      e.printStackTrace();
    }
    System.out.println("File is ready to be scanned.");

  }
}
```

### Interrupting a Thread

```Java
if (Thread.currentThread().isInterrupted()) return;
```

### Concurrency Issues

***Thread-safe Code***

### Race Condition

```Java
package com.lawjune.concurrency;

import java.util.ArrayList;
import java.util.List;

public class ThreadDemo {
  public static void show() {
    var status = new DownloadStatus();

    List<Thread> threads = new ArrayList<>();

    for (var i = 0; i < 10; i++) {
      var thread = new Thread(new DownloadFileTask(status));
      thread.start();
      threads.add(thread);
    }

    for (var thread : threads) {
      try {
        thread.join();
      } catch (InterruptedException e) {
        e.printStackTrace();
      }
    }

    System.out.println(status.getTotalBytes());
  }
}
```

### Strategies for Thread Safety
- Confinement
- Immutability
- Synchronization 
- Atomic objects
- Partitioning 

### Confinement: Confined by a Modified Shared Object

```Java
package com.lawjune.concurrency;

public class DownloadFileTask implements Runnable {

  private DownloadStatus status;

  public DownloadFileTask() {
    this.status = new DownloadStatus();
  }

  @Override
  public void run() {
    System.out.println("Downloading a file: " + Thread.currentThread().getName());

    for (int i = 0; i < 10_000; i++) {
      if (Thread.currentThread().isInterrupted()) return;
      status.incrementTotalBytes();
    }


    status.done();

    System.out.println("Download complete: " + Thread.currentThread().getName());
  }

  public DownloadStatus getStatus() {
    return status;
  }
}
```

```Java
package com.lawjune.concurrency;

import java.util.ArrayList;
import java.util.List;

public class ThreadDemo {
  public static void show() {

    List<Thread> threads = new ArrayList<>();
    List<DownloadFileTask> tasks = new ArrayList<>();

    for (var i = 0; i < 10; i++) {

      var task = new DownloadFileTask();
      tasks.add(task);

      var thread = new Thread(task);
      thread.start();
      threads.add(thread);
    }

    for (var thread : threads) {
      try {
        thread.join();
      } catch (InterruptedException e) {
        e.printStackTrace();
      }
    }

    var totalBytes = tasks.stream()
            .map(t -> t.getStatus().getTotalBytes())
            .reduce(Integer::sum);

    System.out.println(totalBytes);

  }
}
```

### Locks for Synchronization 

```Java
package com.lawjune.concurrency;

import java.util.concurrent.atomic.LongAdder;

public class DownloadStatus {
  private int totalBytes;
  private Lock lock = new ReentrantLock(); 

  public int getTotalBytes() {
    return totalBytes;
  }

  public void incrementTotalBytes() {
  	lock.lock();
  	try {
  		totalBytes++;
  	}
  	finally {
  		lock.unlock();
  	}
  }
}
```

#### The Synchronised Keyword

```Java
package com.lawjune.concurrency;

import java.util.concurrent.atomic.LongAdder;

public class DownloadStatus {
  private int totalBytes;
  private int totalFiles;

  // Monitoring Objects
  private Object totalByteLock = new Object();
  private Object totalFileLock = new Object();

  public int getTotalBytes() {
    return totalBytes;
  }

    public void incrementTotalFiles() {
  	synchronized (totalFileLock) {
  		totalFiles++;
  	}
  }

  public void incrementTotalBytes() {
  	synchronized (totalByteLock) {
  		totalBytes++;
  	}
  }
}
```

## The volatile Keyword

```Java
package com.lawjune.concurrency;

import java.util.ArrayList;
import java.util.List;

public class ThreadDemo {
  public static void show() {
    var status = new DownloadStatus();

    var thread1 = new Thread(new DownloadFileTask(status));
    var thread2 = new Thread(() -> {
      while (!status.isDone()) {}
      System.out.println(status.getTotalBytes());
    });

    thread1.start();
    thread2.start();
  }
}
```

```Java
package com.lawjune.concurrency;

import java.util.concurrent.atomic.LongAdder;

public class DownloadStatus {
  private volatile boolean isDone;
  private LongAdder totalBytes = new LongAdder();
  private int totalFiles;

  public int getTotalBytes() {
    return totalBytes.intValue();
  }

  public void incrementTotalBytes() {
    totalBytes.increment();
  }

  public void incrementTotalFiles() {
    totalFiles++;
  }

  public int getTotalFiles() {
    return totalFiles;
  }

  public boolean isDone() {
    return isDone;
  }

  public void done() {
    isDone = true;
  }
}
```

### Thread Signaling 

```Java
package com.lawjune.concurrency;

import java.util.ArrayList;
import java.util.List;

public class ThreadDemo {
  public static void show() {
    var status = new DownloadStatus();

    var thread1 = new Thread(new DownloadFileTask(status));
    var thread2 = new Thread(() -> {
      while (!status.isDone()) {

        synchronized (status) {
          try {
            status.wait();
          } catch (InterruptedException e) {
            e.printStackTrace();
          }
        }
      }
      System.out.println(status.getTotalBytes());
    });

    thread1.start();
    thread2.start();
  }
}
```

```Java
package com.lawjune.concurrency;

public class DownloadFileTask implements Runnable {

  private DownloadStatus status;

  public DownloadFileTask(DownloadStatus status) {
    this.status = status;
  }

  @Override
  public void run() {
    System.out.println("Downloading a file: " + Thread.currentThread().getName());

    for (int i = 0; i < 1_000_000; i++) {
      if (Thread.currentThread().isInterrupted()) return;
      status.incrementTotalBytes();
    }

    status.done();

    synchronized (status) {
      status.notifyAll();
    }

    System.out.println("Download complete: " + Thread.currentThread().getName());
  }

}
```

### Atomic Objects

```Java
package com.lawjune.concurrency;

import java.util.concurrent.atomic.LongAdder;

public class DownloadStatus {
  private volatile boolean isDone;
  private AtomicInteger totalBytes = new AtomicInteger();
  private int totalFiles;

  public int getTotalBytes() {
    return totalBytes.get();
  }

  public void incrementTotalBytes() {
    totalBytes.incrementAndGet(); // a++
  }

  public void incrementTotalFiles() {
    totalFiles++;
  }

  public int getTotalFiles() {
    return totalFiles;
  }

  public boolean isDone() {
    return isDone;
  }

  public void done() {
    isDone = true;
  }
}
```

### Adders

```Java
package com.lawjune.concurrency;

import java.util.concurrent.atomic.LongAdder;

public class DownloadStatus {
  private volatile boolean isDone;
  private LongAdder totalBytes = new LongAdder();
  private int totalFiles;

  public int getTotalBytes() {
    return totalBytes.intValue(); // sum()
  }

  public void incrementTotalBytes() {
    totalBytes.increment();
  }

  public void incrementTotalFiles() {
    totalFiles++;
  }

  public int getTotalFiles() {
    return totalFiles;
  }

  public boolean isDone() {
    return isDone;
  }

  public void done() {
    isDone = true;
  }
}
```

### Synchronized Collections

```Java
package com.lawjune.concurrency;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.Collection;
import java.util.Collections;

public class ThreadDemo {
  public static void show() {
    Collection<Integer> collection = Collections.synchronizedCollection(new ArrayList<>());

    var thread1 = new Thread(() -> {
      collection.addAll((Arrays.asList(1, 2, 3)));
    });

    var thread2 = new Thread(() -> {
      collection.addAll((Arrays.asList(4, 5, 6)));
    });

    thread1.start();
    thread2.start();

    try {
      thread1.join();
      thread2.join();
    } catch (InterruptedException e) {
      e.printStackTrace();
    }

    System.out.println(collection);
  }
}
```

### Concurrent Collections - Partitioning Technicis
```Java
package com.lawjune.concurrency;

import java.util.Map;
import java.util.concurrent.ConcurrentHashMap;

public class ThreadDemo {
  public static void show() {
    Map<Integer, String> map = new ConcurrentHashMap<>();
    map.put(1, "a");
    map.get(1);
  }
}
```

## The Executor Framework
- Thread Pools
- Executors 
- Callable and Future interfaces
- Asynchronous Programming
- Completable Futures

### Thread Pools

### Executors - Interaface ExecutorService 
Just help to manipulate the threads, not include the concurrency problem.

### Callables and Futures
```JaVA
package com.lawjune.executors;

import java.util.concurrent.ExecutionException;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;

public class ExecutorsDemo {
  public static void show() {
    ExecutorService executor = Executors.newFixedThreadPool(2);

    try {
      var future = executor.submit(() -> {
        LongTask.simulate();
        return 1;
      });

      System.out.println("Do more work");

      try {
        var result = future.get();
        System.out.println(result);
      } catch (InterruptedException | ExecutionException e) {
        e.printStackTrace();
      }
    }
    finally {
      executor.shutdown();
    }
  }
}
```

### Asynchronous (Non-Blocking) Programming 

### Completable Future 

### Creating a Completable Future
```Java
package com.lawjune.executors;

import java.util.concurrent.CompletableFuture;
import java.util.concurrent.ExecutionException;
import java.util.function.Supplier;

public class CompletableFuturesDemo {
  public static void show() {
      Supplier<Integer> task = () -> 1;
      var future = CompletableFuture.supplyAsync(task);
      try {
          var result = future.get();
          System.out.println(result);

      } catch (InterruptedException e) {
          e.printStackTrace();
      } catch (ExecutionException e) {
          e.printStackTrace();
      }
  }
}
```

### Implementing an Asynchronous API

```Java
package com.lawjune.executors;

import java.util.concurrent.CompletableFuture;

public class MailService {
  public void send() {
    LongTask.simulate();
    System.out.println("Mail was sent.");
  }

  public CompletableFuture<Void> sendAsync() {
    return CompletableFuture.runAsync(() -> send());
  }
}
```

```Java
package com.lawjune;

import com.lawjune.executors.MailService;

public class Main {

    public static void main(String[] args) {
        var service = new MailService();
        service.sendAsync();
        System.out.println("Hello World!");

        try {
            Thread.sleep(5000); // To prove the mail sent
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```

### Running Code on Completion 
```Java
package com.lawjune.executors;

import java.util.concurrent.CompletableFuture;

public class CompletableFuturesDemo {
  public static void show() {
      var future = CompletableFuture.supplyAsync(() -> 1);
      future.thenRunAsync(() -> {
          System.out.println(Thread.currentThread().getName());
          System.out.println("Done");
      });

      future.thenAcceptAsync(result -> {
          System.out.println(Thread.currentThread().getName());
          System.out.println(result);
      });
  }
}
```

### Handling Exceptions
```Java
package com.lawjune.executors;

import java.util.concurrent.CompletableFuture;
import java.util.concurrent.ExecutionException;

public class CompletableFuturesDemo {
  public static void show() {
      var future = CompletableFuture.supplyAsync(() -> {
          System.out.println("Getting the current weather");
          throw  new IllegalArgumentException();
      });

      try {
          var temperature = future.exceptionally(ex -> 3).get();
          System.out.println(temperature);
      } catch (InterruptedException e) {
          e.printStackTrace();
      } catch (ExecutionException e) {
          e.printStackTrace();
      }
  }
}
```

### Transforming Results

```Java
package com.lawjune.executors;

import java.util.concurrent.CompletableFuture;
import java.util.concurrent.ExecutionException;

public class CompletableFuturesDemo {
    public static int toFahrenheit(int celsius) {
        return (int) (celsius * 1.8) + 32;
    }

    public static void show() {
      var future = CompletableFuture.supplyAsync(() -> 20);
      try {
          var result =  future.
                  thenApply(CompletableFuturesDemo::toFahrenheit)
                  .get();
          System.out.println(result);
      } catch (InterruptedException e) {
          e.printStackTrace();
      } catch (ExecutionException e) {
          e.printStackTrace();
      }
  }
}
```

```Java
package com.lawjune.executors;

import java.util.concurrent.CompletableFuture;

public class CompletableFuturesDemo {
    public static int toFahrenheit(int celsius) {
        return (int) (celsius * 1.8) + 32;
    }

    public static void show() {
      var future = CompletableFuture.supplyAsync(() -> 20);

      future.thenApply(CompletableFuturesDemo::toFahrenheit)
              .thenAccept(System.out::println);
  }
}

```

### Composing Completable Futures

```Java
package com.lawjune.executors;

import java.util.concurrent.CompletableFuture;

public class CompletableFuturesDemo {
    public static void show() {
        // id -> email
        // email -> playlist
        var future = CompletableFuture.supplyAsync(() -> "email");
        future.thenCompose(email -> CompletableFuture.supplyAsync(() -> "playlist"))
        .thenAccept(playlist -> System.out.println(playlist));
  }
}
```

```Java
package com.lawjune.executors;


import java.util.concurrent.CompletableFuture;

public class CompletableFuturesDemo {
    public static CompletableFuture<String> getUserEmailAsync() {
        return CompletableFuture.supplyAsync(() -> "email");
    }

    public static CompletableFuture<String> getPlaylistAsync(String email) {
        return CompletableFuture.supplyAsync(() -> "playlist");
    }

    public static void show() {
        getUserEmailAsync()
                .thenCompose(CompletableFuturesDemo::getPlaylistAsync)
                .thenAccept(System.out::println);
  }
}
```

### Combining Completable Futures
```Java
package com.lawjune.executors;

import java.util.concurrent.CompletableFuture;

public class CompletableFuturesDemo {
    public static void show() {
        var first = CompletableFuture.supplyAsync(() -> 20);
        var second = CompletableFuture.supplyAsync(() -> 0.9);

        first.thenCombine(second, (price, exchangeRate) -> price * exchangeRate)
                .thenAccept(result -> System.out.println(result));
  }
}
```

```Java
package com.lawjune.executors;

import java.util.concurrent.CompletableFuture;

public class CompletableFuturesDemo {
    public static void show() {
        var first = CompletableFuture
                .supplyAsync(() -> "20USD")
                .thenApply(str -> {
                    var price = str.replace("USD", "");
                    return Integer.parseInt(price);
                });

        var second = CompletableFuture.supplyAsync(() -> 0.9);

        first.thenCombine(second, (price, exchangeRate) -> price * exchangeRate)
                .thenAccept(result -> System.out.println(result));
  }
}
```

### Waiting for Many Tasks
```Java
package com.lawjune.executors;

import java.util.concurrent.CompletableFuture;
import java.util.concurrent.ExecutionException;

public class CompletableFuturesDemo {
    public static void show() {
        var first = CompletableFuture.supplyAsync(() -> 1);
        var second = CompletableFuture.supplyAsync(() -> 2);
        var third = CompletableFuture.supplyAsync(() -> 3);

        var all = CompletableFuture.allOf(first, second, third);
        all.thenRun(() -> {
            try {
                var firstResult = first.get();
                System.out.println(firstResult);
            } catch (InterruptedException e) {
                e.printStackTrace();
            } catch (ExecutionException e) {
                e.printStackTrace();
            }

            System.out.println("All tasks completed successfully");
        });
  }
}
``` 

### Waiting for the First Task
```Java
package com.lawjune.executors;

import java.util.concurrent.CompletableFuture;
import java.util.concurrent.ExecutionException;

public class CompletableFuturesDemo {
    public static void show() {
        var first = CompletableFuture.supplyAsync(() -> 1);
        var second = CompletableFuture.supplyAsync(() -> 2);
        var third = CompletableFuture.supplyAsync(() -> 3);

        var all = CompletableFuture.allOf(first, second, third);
        all.thenRun(() -> {
            try {
                var firstResult = first.get();
                System.out.println(firstResult);
            } catch (InterruptedException e) {
                e.printStackTrace();
            } catch (ExecutionException e) {
                e.printStackTrace();
            }

            System.out.println("All tasks completed successfully");
        });
  }
}
```

### Handling Timeouts
```Java
package com.lawjune.executors;

import java.util.concurrent.CompletableFuture;
import java.util.concurrent.ExecutionException;
import java.util.concurrent.TimeUnit;

public class CompletableFuturesDemo {
    public static void show() {
        var future = CompletableFuture.supplyAsync(() -> {
            LongTask.simulate();
            return 1;
        });

        try {
            var result = future
                    .completeOnTimeout(1, 1, TimeUnit.SECONDS)
                    .get();
            System.out.println(result);
        } catch (InterruptedException e) {
            e.printStackTrace();
        } catch (ExecutionException e) {
            e.printStackTrace();
        }
    }
}
```

### Project: Best Price Finder
```Java
package com.lawjune.executors;

public class Quote {
  private final String site;
  private final int price;

  public Quote(String site, int price) {
    this.site = site;
    this.price = price;
  }

  public String getSite() {
    return site;
  }

  public int getPrice() {
    return price;
  }

  @Override
  public String toString() {
    return "Quote{" +
            "site='" + site + '\'' +
            ", price=" + price +
            '}';
  }
}
```

```Java
package com.lawjune.executors;

import java.util.List;
import java.util.Random;
import java.util.concurrent.CompletableFuture;
import java.util.stream.Collectors;
import java.util.stream.Stream;

public class FlightService {
  public Stream<CompletableFuture<Quote>> getQuotes() {
    var sites = List.of("site1", "site2", "site3");

    return sites
            .stream()
            .map(this::getQuote);
  }

  public CompletableFuture<Quote> getQuote(String site) {
    return CompletableFuture.supplyAsync(() -> {
      System.out.println("Getting a quote from " + site);

      var random = new Random();

      LongTask.simulate(1_000 + random.nextInt(2_000));

      var price = 100 + random.nextInt(10);

      return new Quote(site, price);
    });
  }
}
```

```Java
package com.lawjune.executors;

import java.time.Duration;
import java.time.LocalTime;
import java.util.concurrent.CompletableFuture;
import java.util.stream.Collectors;

public class CompletableFuturesDemo {
    public static void show() {
        var start = LocalTime.now();

        var service = new FlightService();
        var futures = service.getQuotes()
                .map(future -> future.thenAccept(System.out::println))
                .collect(Collectors.toList());

        CompletableFuture
                .allOf(futures.toArray(new CompletableFuture[0]))
                .thenRun(() -> {
                    var end = LocalTime.now();
                    var duration = Duration.between(start, end);
                    System.out.println("Retrieved all quotes in  " + duration.toMillis() + " msec");
                });

        try {
            Thread.sleep(10_000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```