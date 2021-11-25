# Big O Notation


## What is the Big O?
*Big O notation is a mathematical notation that describes the limiting behavior  of a function when the argument tends towards a particular valule or infinity.*  --- Wiki

**We use Big O to describe the performance of an algorithm** 


## O(1)
```Java
    public void log(int[] numbers) {
        System.out.println(numbers[0]);
    }
```


## O(n)
```Java
    public void log(int[] numbers) {
    	for (int i = 0; i < numbers.length; i++)
    		System.out.println(numbers[i]);
    }
```
- This where the size of the input matters.
- If you have a single item in this array, you're going to have one print operation. 
- If you have a million items, obviously you're going to have a million print operations. 
- So the cost of this algorithm grows ***linearly*** and in **direct correlation** in the size of the input. 
- O(n) - the n presents the size of input. So as n grows, the cost of this algorithm also grows linearly.


## O(n^2)
```Java
    public void log(int[] numbers) {

    	for (int number : numbers) // O(n)
    		System.out.println(number);

    	for (int first : numbers) // O(n^2)
    		for (int second : numbers)
    			System.out.println(first + ", " + second);
    }
```

## O(log n)

***BINARY SEARCH***

## O(2^n)

## Space Complexity
```Java
    public void greet(String[] names) {

        // O(n) space
        String[] copy = new String[names.length];

        // Whatever our input array has 10 or one million items
        // This method will only allocate some additional memory for this loop variable
        // O(1) space
        for (int i = 0; i < names.length; i++)
            System.out.println("Hi " + names[i]);
    }
```

# Arrays

## Understanding of Arrays

The items of "array list" get stored sequentially in memory. 

```Java
int [] intArray = [10, 20, 30, 40, 50]
```

Integers take 4 bytes of memory:
[10] -> address 0x100
[20] -> address 0x104
[30] -> address 0x108

For this very reason, looking up items in an array is super fast. 

We give our array an index and it will figure out where exactly in memory we should access.

### Lookup -> O(1)
**Runtime Complexity** => **O(1)**

**If you need to store the list of items and access them by their index, arrys are the optimal data structures for you.**

### Insert -> O(n)
***Limitation or weakness of arrys***
In Java and many other languages arrys are static which means when we allocate them we should specifiy their size and this size cannot change later on, so we need to know ahead of time how many items we want to store in an arry. 

If the pre-guessing array is too small?
To allocate a larger array and then copy all the items in the old arrary into the new array.
**This opeartion can be costly => O(n)**

### Delete -> O(n)

### Working with Arrays
```Java
package com.lawjune;

import java.util.Arrays;

public class Main {

    public static void main(String[] args) {
        int[] numbers = new int[3];
        System.out.println(Arrays.toString(numbers));

        numbers[0] = 10;
        numbers[1] = 20;
        numbers[2] = 30;
        System.out.println(Arrays.toString(numbers));

        int[] numbersNew = {10, 20, 30};
        System.out.println(Arrays.toString(numbersNew));
        System.out.println(numbersNew.length); // We can not change

    }
}
```

### Exercise: Building an Array
When we add new items to this array, it will automatically grow, and as we remove item it will automatically shrink. 

***Step 1 - constructor & print
```Java
package com.lawjune;

public class Array {
    private int[] items;
    private int count;

    public Array(int length) {
        items = new int[length];
    }

    public void print() {
        for (int i = 0; i < count; i++)
            System.out.println(items[i]);
    }
}
```
***

***Step2 - insert() - O(n)
```Java
package com.lawjune;

public class Array {
    private int[] items;
    private int count;

    public Array(int length) {
        items = new int[length];
    }

    public void insert(int item) {
        // If the array is full, resize it
        if  (items.length == count) {
            // Create a new array (twice the size)
            int[] newItems = new int[count * 2];

            // Copy all the existing items
            for (int i = 0; i < count; i ++)
                newItems[i] = items[i];

            // Set "items" to this new array
            items = newItems;
        }

        // Add the new item at the end
        items[count++] = item;
    }

    public void print() {
        for (int i = 0; i < count; i++)
            System.out.println(items[i]);
    }
}

```
***

***Step3 - removeAt() - O(n)
```Java
******
    public void removeAt(int index) {
        // Validate the index
        if (index < 0 || index > count)
            throw new IllegalArgumentException();

        // Shift the items to the left to fill the hole
        // [10, 20, 30, 40]
        // index: 1 -> 20
        // 1 <- 2; 2 <- 3
        for (int i = index; i < count; i++)
            items[i] = items[i + 1];
        count--;

    }
******
```
***

***Step4 - indexOf() - O(n)
```Java
******
    public int indexOf(int item) {
        // If we find it, return index
        // Otherwise, return -1
        // O(n)
        for (int i = 0; i < count; i++)
            if(items[i] == item)
                return i;
        return -1;
    }
******
```
***

### Dynamic Arrays

***Vector***
- Grow by 100% in size, every time it gets full. 
- All of the classes in Vector are **synchroinized** => Only a single thread can access that method.
- In other words, if you have a multi threaded application where multiple threads are going to work with this collection, then you're not going to be able to use the vector class.

***ArrayList***
- Grow by 50% in size. 

```Java
package com.lawjune;

import java.util.ArrayList;

public class Main {

    public static void main(String[] args) {
        ArrayList<Integer> list = new ArrayList<>();
        list.add(10);
        list.add(20);
        list.add(30);
        System.out.println(list);
        list.remove(2);
        System.out.println(list);
        System.out.println(list.indexOf(20));
        System.out.println(list.contains(10));
        System.out.println(list.toArray());
    }
}
```


# Linked List

## What are Linked Lists?

LOOKUP
- By Value O(n)
- By Index O(n)

INSERT
- At the End  O(1)
- At the Begining O(1)
- In the Middle O(n)

DELETE
- From the Beginning O(1)
- From the End O(n)
	- We can easily get the tail.
	- But we need to know the previous node, so we can have the tail point to that node. 
	- We have to traverse the list from the head all the way to the tail as soon as we get to the node before the last node. 
- From the Middle O(n)

## Working with Linked List
```Java
package com.lawjune;

import java.util.Arrays;
import java.util.LinkedList;

public class Main {

    public static void main(String[] args) {
        LinkedList<Integer> list = new LinkedList<>();
        list.addLast(10);
        list.addLast(20);
        list.addLast(30);
        list.addFirst(5);
        list.removeLast();
        System.out.println(list.contains(10));
        System.out.println(list.indexOf(10));
        System.out.println(list.size());
        System.out.println(Arrays.toString(list.toArray()));
        System.out.println(list);
    }
}
```

## Exercise: Building a Linked List 

***Step1 - addLast
```Java
package com.lawjune;

public class LinkedList {

    private class Node {
        private int value;
        private Node next;

        public Node(int value){
            this.value = value;
        }
    }

    private Node first;
    private Node last;

    public void addLast(int item) {
        var node = new Node(item);

        if (first == null)
            first = last = node;
        else {
            last.next = node;
            last = node;
        }
    }
}
```
***

***Step2 - addLast (Old Implementation)
```Java
******
    public void addFirst(int item) {
        var node = new Node(item);

        if (first == null)
            first = last = node;
        else {
            node.next = first;
            first = node;
        }
    }
******
```
***

***Step2 - addLast (New Implementation)
```Java
******
    public void addFirst(int item) {
        var node = new Node(item);

        if (isEmpty())
            first = last = node;
        else {
            node.next = first;
            first = node;
        }
    }

    private boolean isEmpty() {
        return first == null;
    }
******
```
***

***Step3 - indexOf
```Java
******
    public int indexOf(int item) {
        int index = 0;
        var current = first;
        while (current != null) {
            if (current.value == item) return index;
            current = current.next;
            index++;
        }
        return -1;
    }
******
```
***

***Step4 - contains
```Java
******
    public boolean contains(int item) {
        return indexOf(item) != -1;
    }
******
```
***

***Step5 - removeFirst
```Java
******
    public void removeFirst() {
        // [10 -> 20 -> 30]
        // first -> 20

        if (isEmpty())
            throw new NoSuchElementException();

        if (first == last) {
            first = last = null;
            return;
        }

        var second = first.next;
        first.next = null; // [10  20 -> 30]
        first = second;
    }
******
```
***

***Step6 - removeLast
```Java
******
    public void removeLast() {
        if (isEmpty())
            throw new NoSuchElementException();

        if (first == last) {
            first = last = null;
            return;
        }

        // [10 -> 20 -> 30]
        // last -> 20

        // previous -> 20
        var previous = getPrevious(last);
        last = previous;
        last.next = null;
    }

    private Node getPrevious(Node node) {
        var current = first;
        while (current != null) {
            if (current.next == node) return current;
            current = current.next;
        }
        return null;
    }
******
```
***

***Step7 - size - O(1)
```Java
package com.lawjune;

import java.util.NoSuchElementException;

public class LinkedList {

    private class Node {
        private int value;
        private Node next;

        public Node(int value){
            this.value = value;
        }
    }

    private Node first;
    private Node last;
    private int size;

    public void addLast(int item) {
        var node = new Node(item);

        if (isEmpty())
            first = last = node;
        else {
            last.next = node;
            last = node;
        }

        size++;
    }

    public void addFirst(int item) {
        var node = new Node(item);

        if (isEmpty())
            first = last = node;
        else {
            node.next = first;
            first = node;
        }

        size++;
    }

    private boolean isEmpty() {
        return first == null;
    }

    public int indexOf(int item) {
        int index = 0;
        var current = first;
        while (current != null) {
            if (current.value == item) return index;
            current = current.next;
            index++;
        }
        return -1;
    }

    public boolean contains(int item) {
        return indexOf(item) != -1;
    }

    public void removeFirst() {

        if (isEmpty())
            throw new NoSuchElementException();

        if (first == last)
            first = last = null;
        else {
            var second = first.next;
            first.next = null;
            first = second;
        }

        size--;
    }

    public void removeLast() {
        if (isEmpty())
            throw new NoSuchElementException();

        if (first == last)
            first = last = null;
        else {
            var previous = getPrevious(last);
            last = previous;
            last.next = null;
        }
        size--;
    }

    private Node getPrevious(Node node) {
        var current = first;
        while (current != null) {
            if (current.next == node) return current;
            current = current.next;
        }
        return null;
    }

    public int size() {
        return size;
    }
}
```
***

***Step8 - toArrays
```Java
******
    public int[] toArray() {
        int[] array = new int[size];
        var current = first;
        var index = 0;
        while (current != null) {
            array[index++] = current.value;
            current = current.next;
        }
        return array;
    }
```
***

## Arrays vs Linked Lists

### From the Memory/Space perspective

- Static arrays have a fixed size 
- Dynamic arrays grow by 50%-100%
- Linked lists don't waste memory
- Use arrays if you know the number of items to store
- new ArrayList(100)

### From the Runtime Performance Perspective

	| **ARRAYS** | **LINKED LISTS** | 

**Lokkup**
|By Index | O(1) | O(n) |
|By Value | O(n) | O(n) |

**Insert**
|Beginning/End| O(n) | O(1) |
|Middle   | O(n) | O(n) |

**Delete**
|Beginning| O(n) | O(1) |
|Middle   |	O(n) | O(n) |
|End|     |	O(n) | O(n) |


## Types of Linked Lists

### SINGLE

[node] -> [node] -> [node]


### DOUBLY

[node] <-> [node] <-> [node]
Delete from the End -> O(1)

[node-end] -> [node-begin] => trackList (circle)


## Exercise: Reversing a Linked List

My solution - 1
```Java
    public void reverseWithCollectionsMethod() {
        var arrayList = new ArrayList<Node>();
        var current = last;
        while (current != null) {
            arrayList.add(current);
            current = getPrevious(current);
        }
        Collections.reverse(arrayList);

        for (int i = 0; i < size; i++) {
            removeLast();
            addFirst(arrayList.get(i).value);
        }
    }
```

My solution - 2
```Java
    public void reverseWithGetPrevious() {
        var currentPreviousPrevious = first;
        var currentPrevious = first.next;
        var current = currentPrevious.next;
        first.next = null;

        while ( current != null ) {
            currentPrevious.next = currentPreviousPrevious;
            currentPreviousPrevious = currentPrevious;
            currentPrevious = current;
            current = current.next;
            currentPrevious.next = currentPreviousPrevious;
        }
        last = first;
        first = currentPrevious;
```

Mosh's solution
```Java
    public void reverse() {
        if (isEmpty()) return;

        //  f            l
        // [10 -> 20 -> 30]
        //   p     c     n
        //   n = c.next
        //   c.next = p

        var previous = first;
        var current = first.next;

        while (current != null) {
            var next = current.next;
            current.next = previous;
            previous = current;
            current = next;
        }

        first.next = null;
        last = first;
        first = previous;
    }
```

## Exercise: Kth Node from the End

Find the Kth node from the end of a linked list in one pass.

[10 -> 20 -> 30 -> 40 -> 50]
             *           * 

k = 1 => 50
k = 2 => 40
k = 3 => 30 (distance = 2)      

```Java
    public int getKthFromTheEnd(int k) {
        if (isEmpty())
            throw new IllegalArgumentException();
        var a = first;
        var b = first;
        for (int i = 0; i < k - 1; i++) {
            b = b.next;
            if (b == null)
                throw new IllegalArgumentException();
        }
        while (b != last) {
            a = a.next;
            b = b.next;
        }
        return a.value;
    }
```

## Summary of Linked Lists

***Key Points***
- Second most used data structures
- Grow and shrink automatically 
- Take a bit more memory

***Runtime Complexities*** 
- Lookup 
	- By Index O(n)
	- By Value O(n)

- Insert 
	- Beginning/End O(1)
	- Middle O(n)

- Delete
	- Beginning O(1)
	- Middle O(n)
	- End O(n) / O(1)

# Stacks

## What are Stacks?
- Implement the undo feature
- Build compliers (eg syntax checking)
- Evaluate expressions (eg 1 + 2*3)
- Build navigation (eg forward/back)

Last In First Out - LIFO

***STACK OPERATIONS***
- push(item) - O(1)
- pop() - O(1)
- peek() - O(1)
- isEmpty - O(1)

## Working with Staks
```Java
package com.lawjune;

import java.util.Stack;

public class Main {

    public static void main(String[] args) {
        Stack<Integer> stack = new Stack<>();
        stack.push(10);
        stack.push(20);
        stack.push(30);
        System.out.println(stack);
        var top = stack.pop();
        System.out.println(top);
        System.out.println(stack);
        System.out.println(stack.peek());
    }
}
```

## Reversing a String

***My Solution***
```Java
package com.lawjune;

import java.util.Arrays;
import java.util.Stack;

public class Main {

    public static void main(String[] args) {
        String str = "abcd";
        char[] charArray = str.toCharArray();
        char[] reverseCharArray = new char[charArray.length];
        Stack<Character> stack = new Stack<>();
        for (char c : charArray) {
            stack.push(c);
        }
        for (int i = 0; i < reverseCharArray.length; i++) {
            reverseCharArray[i] = stack.pop();
        }
        String reverseStr = new String(reverseCharArray);

        System.out.println(reverseStr);
    }
}
```

***Mosh's solution***
```Java
package com.lawjune;

import java.util.Stack;

public class StringReverser {
    public String reverse(String input) {
        if (input == null)
            throw  new IllegalArgumentException();

        Stack<Character> stack = new Stack<>();

        for (char ch : input.toCharArray())
            stack.push(ch);

        StringBuffer reversed = new StringBuffer();
        while (!stack.empty())
            reversed.append(stack.pop());
            // Concatenation too long!
            // reversed += stack.pop();

        return reversed.toString();
    }
}
```

## Blance Expressions
Only focus on parenthesis: "(" => "(1 + 2)"

- Iterate over the string
- Get each character at a time
- If this character is an opening bracket 
	=> Push it onto the top of the stack
- If it is a regular character
	=> Ignore it
- If it's a closing bracket 
	=> Pop the item on top of the stack

### My Solution
```Java
package com.lawjune;

import java.util.Stack;

public class BalanceExpression {
    public static boolean isBalance(String input) {
        if (input == null)
            throw  new IllegalArgumentException();

        Stack<Character> stack = new Stack<>();

        for (char ch : input.toCharArray()) {
            if(ch == '(') stack.push(ch);
            if(ch == ')') stack.pop();
        }
        return stack.isEmpty();
    }
}
```

### Mosh's Basic Implementation 
```Java
package com.lawjune;

import java.util.Stack;

public class Expression {
    public boolean isBalanced(String input) {
        Stack<Character> stack = new Stack<>();

        for (char ch : input.toCharArray()) {
            if (ch == '(')
                stack.push(ch);

            if (ch == ')') {
                if (stack.isEmpty()) return false;
                stack.pop();
            }

        }

        return stack.isEmpty();
    }
}
```

### Supporting Other Brackets
```Java
package com.lawjune;

import java.util.Stack;

public class Expression {
    public boolean isBalanced(String input) {
        Stack<Character> stack = new Stack<>();

        for (char ch : input.toCharArray()) {
            if (ch == '(' || ch == '<' || ch == '[' || ch == '{')
                stack.push(ch);

            if (ch == ')' || ch == '>' || ch == ']' || ch == '}') {
                if (stack.isEmpty()) return false;
                var top = stack.pop();
                if (
                        (ch == ')' && top != '(') ||
                        (ch == '>' && top != '<') ||
                        (ch == ']' && top != '[') ||
                        (ch == '}' && top != '{')
                ) return false;
            }
        }

        return stack.isEmpty();
    }
}
```

### First Refactoring
```Java
package com.lawjune;

import java.util.Stack;

public class Expression {
    public boolean isBalanced(String input) {
        Stack<Character> stack = new Stack<>();

        for (char ch : input.toCharArray()) {
            if (isLeftBracket(ch))
                stack.push(ch);

            if (isRightBracket(ch)) {
                if (stack.isEmpty()) return false;
                var top = stack.pop();
                if (bracketMatch(top, ch)) return false;
            }

        }

        return stack.isEmpty();
    }

    private boolean isLeftBracket(char ch) {
        return ch == '(' || ch == '<' || ch == '[' || ch == '{';
    }

    private boolean isRightBracket(char ch) {
        return ch == ')' || ch == '>' || ch == ']' || ch == '}';
    }

    private boolean bracketMatch(char left, char right) {
        return  (right == ')' && left != '(') ||
                (right == '>' && left != '<') ||
                (right == ']' && left != '[') ||
                (right == '}' && left != '{');
    }
}
```

### Second Refactoring
```Java
package com.lawjune;

import java.util.Arrays;
import java.util.List;
import java.util.Stack;

public class Expression {

    private final List<Character> leftBrackets = Arrays.asList('(', '<', '[', '{');
    private final List<Character> rightBrackets = Arrays.asList(')', '>', ']', '}');

    public boolean isBalanced(String input) {
        Stack<Character> stack = new Stack<>();

        for (char ch : input.toCharArray()) {
            if (isLeftBracket(ch))
                stack.push(ch);

            if (isRightBracket(ch)) {
                if (stack.isEmpty()) return false;
                var top = stack.pop();
                if (!bracketMatch(top, ch)) return false;
            }

        }

        return stack.isEmpty();
    }

    private boolean isLeftBracket(char ch) {
        return leftBrackets.contains(ch);
    }


    private boolean isRightBracket(char ch) {
       return rightBrackets.contains(ch);
    }

    private boolean bracketMatch(char left, char right) {
        return leftBrackets.indexOf(left) == rightBrackets.indexOf(right);
    }
}
```

## Building a Stack Using an Array

// Stack
// push
// pop
// peek
// isEmpty
// int[]

### My Solution
```Java
package com.lawjune;

public class Stack {

    private int[] items;
    private int count;

    public Stack() {
        count = 0;
    }

    public void push(int item) {
        if(count == 0) {
            items = new int[1];
            items[0] = item;
            count++;
        }
        else {
            int[] newItems = new int[count+1];
            System.arraycopy(items, 0, newItems, 0, count);
            newItems[count++] = item;
            items = newItems;
        }
    }

    public int pop() {
        if( count == 0 ) {
            throw new IllegalStateException();
        }
        count--;
        int value = items[count];
        int[] newItems = new int[count];
        System.arraycopy(items, 0, newItems, 0, count);
        items = newItems;
        return value;
    }
    public int peek() {
        if( count == 0 ) {
            throw new IllegalStateException();
        }
        return items[count-1];
    }

    public void print() {
        for(int i = 0; i < count; i++)
            System.out.println(items[i]);
    }

    public boolean isEmpty() {
        return count == 0;
    }
}
```

### Mosh's Solution
```Java
package com.lawjune;

import java.util.Arrays;

public class Stack {

    private int[] items;
    private int count;

    public Stack(int size) {
        items = new int[size];
    }

    public void push(int item) {
        if (count == items.length) throw new StackOverflowError();
        items[count++] = item;
    }

    public int pop() {
        if (count == 0) throw new IllegalStateException();
        return items[--count];
    }

    public int peek() {
        if (count == 0) throw new IllegalStateException();
        return items[count - 1];
    }

    public boolean isEmpty() {
        return count == 0;
    }

    @Override
    public String toString() {
        int[] content = Arrays.copyOfRange(items, 0, count);
        return Arrays.toString(content);
    }
}
```

# Queues

## What are Queues?
FIFO
- Printers
- Operating systems
- Web servers
- Live support systems

***OPERATIONS***
- enqueue O(1)
- dequeue O(1)
- peek O(1)
- isEmpty O(1)
- isFull O(1)

## Exercise: Reversing a Queue
```Java
package com.lawjune;


import java.util.ArrayDeque;
import java.util.Queue;
import java.util.Stack;

public class Main {

    public static void main(String[] args) {
        Queue<Integer> queue = new ArrayDeque<>();
        queue.add(10);
        queue.add(20);
        queue.add(30);
        System.out.println(queue);
        reverse(queue);
        System.out.println(queue);

    }

    public static void reverse(Queue<Integer> queue) {
        Stack<Integer> stack = new Stack<>();
        while (!queue.isEmpty())
            stack.push(queue.remove());
        while (!stack.isEmpty())
            queue.add(stack.pop());
    }
}
```

## Exercise: Building a Queue Using an Array

- ArrayQueue (ArrayDeque)
- enqueue
- dequeue
- peek
- isEmpty
- isFull

[10, 20, 30, 40, 50]
	  F           R
 F=0 F=1

### My Solution with Bugs
```Java
package com.lawjune;

import java.util.Arrays;

public class ArrayQueue {

    private int[] items;
    private int front;
    private int rear;
    private int size;

    public ArrayQueue(int size) {
        this.size = size;
        items = new int[size];
    }

    public void enqueue(int item) {
        if (rear == size) throw new StackOverflowError();
        items[rear++] = item;
    }

    public int dequeue() {
        if (front == rear) throw new IllegalStateException();
        int value = items[front];
        front++;
        return value;
    }

    public int peek() {
        return items[front];
    }

    public boolean isEmpty() {
        return rear == 0;
    }

    public boolean isFull() {
        return (rear + 1) == size;
    }

    @Override
    public String toString() {
        int[] content = Arrays.copyOfRange(items, front, rear);
        return Arrays.toString(content);
    }
}
```

### Solution: Circular Arrays

[60, 70, 30, 40, 50]

5 -> 0
6 -> 1
7 -> 2
8 -> 3
9 -> 4
10 -> 0
11 -> 1
(rear + 1) % length

```Java
package com.lawjune;

import java.util.Arrays;

public class ArrayQueue {

    private int[] items;
    private int front;
    private int rear;
    private int capacity;
    private int count;

    public ArrayQueue(int capacity) {
        this.capacity = capacity;
        items = new int[capacity];
    }

    public void enqueue(int item) {
        if (count == capacity) throw new IllegalStateException();
        items[rear] = item;
        rear = (rear + 1) % capacity;
        count++;
    }

    public int dequeue() {
        if (front == rear) throw new IllegalStateException();
        int item = items[front];
        items[front] = 0;
        front = (front + 1) & capacity;
        count--;
        return item;
    }

    public int peek() {
        return items[front];
    }

    public boolean isEmpty() {
        return rear == 0;
    }

    public boolean isFull() {
        return (rear + 1) == capacity;
    }

    @Override
    public String toString() {
//        int[] content = Arrays.copyOfRange(items, front, rear);
        return Arrays.toString(items);
    }
}
```

## Exercise: Building a Queue Using Stacks

### My Solution
```Java
package com.lawjune.streams;

import java.util.Stack;

public class StackQueue {
    private Stack<Integer> stack = new Stack<>();

    public void enqueue(int item) {
        stack.push(item);
    }

    public int peek() {
        int item = stack.firstElement();
        return item;
    }

    public int dequeue() {
        int item = stack.firstElement();
        stack.removeElementAt(0);
        return item;
    }
}
```

### Mosh's Solution with Two Stacks
```Java
package com.lawjune;

import java.util.Stack;

public class QueueWithTwoStacks {
    private Stack<Integer> stack1 = new Stack<>();
    private Stack<Integer> stack2 = new Stack<>();

    // O(1)
    public void enqueue(int item) {
        stack1.push(item);
    }

    // O(n)
    public int dequeue() {
        if (isEmpty())
            throw new IllegalStateException();

        moveStack1ToStack2();
        return stack2.pop();
    }

    public int peek() {
        if (isEmpty())
            throw new IllegalStateException();

        moveStack1ToStack2();
        return stack2.peek();
    }

    private void moveStack1ToStack2() {
        if (stack2.isEmpty())
            while (!stack1.isEmpty())
                stack2.push(stack1.pop());
    }

    public boolean isEmpty() {
        return stack1.isEmpty() && stack2.isEmpty();
    }
}
```

## Priority Queues
```Java
package com.lawjune;

import java.util.PriorityQueue;

public class Main {

    public static void main(String[] args) {
        PriorityQueue<Integer> queue = new PriorityQueue<>();
        queue.add(5);
        queue.add(1);
        queue.add(3);
        queue.add(2);
        while (!queue.isEmpty())
            System.out.println(queue.remove());
    }
}
```

### Exercise: Build a Priority Queue

insert(2) in [1, 3, 5, 7]
-> [1, 3, 5, 7, 7]
-> (5 >= 2) [1, 3, 5, 5, 7]
-> (3 >= 2) [1, 3, 3, 5, 7]
-> (! 1 >= 2) [1, 2, 3, 5, 7]
-> items[i + 1] = items[i]

#### My Solution
```java
package com.lawjune;

public class ArrayPriorityQueue {
    private int[] items;
    private int capacity;
    private int count;

    public ArrayPriorityQueue(int capacity) {
        this.capacity = capacity;
        this.items = new int[capacity];
    }

    public void add(int item) {
        if(count == 0) {
            items[0] = item;
        }

        if (count == 1) {
            if (items[0] > item) {
                items[1] = items[0];
                items[0] = item;
            }
            else {
                items[1] = item;
            }
        }
        else {
            for (int i = count; i > 0; --i)
            {
                items[i] = items[i - 1];
                if (items[i - 1] >= item){
                    continue;
                }
                else {
                    items[i] = item;
                }
            }
        }

        count++;
    }

    public int remove() {
        int item = items[count-1];
        count--;
        return item;
    }

    public boolean isEmpty() {
        return count == 0;
    }
}
```

#### Mosh's Solution Before Refactoring
```Java
package com.lawjune;

import java.util.Arrays;

public class PriorityQueue {
    private int[] items = new int[5];
    private int count;

    public void add(int item) {
        if (count == items.length)
            throw new IllegalStateException();

        // Shifting items
        int i;
        for (i = count - 1; i >= 0; i--) {
            if (items[i] > item)
                items[i + 1] = items[i];
            else
                break;
        }
        items[i + 1] = item;
        count++;
    }

    public int remove() {
        if (isEmpty())
            throw new IllegalStateException();
        return items[--count];
    }

    public boolean isEmpty() {
        return count == 0;
    }

    @Override
    public String toString() {
        return Arrays.toString(items);
    }
}
```

#### Mosh's Refactored Solution
```Java
package com.lawjune;

import java.util.Arrays;

public class PriorityQueue {
    private int[] items = new int[5];
    private int count;

    public void add(int item) {
        if (isFull())
            throw new IllegalStateException();
        var i = shiftItemsToInsert(item);
        items[i] = item;
        count++;
    }

    public int shiftItemsToInsert(int item) {
        // Shifting items
        int i;
        for (i = count - 1; i >= 0; i--) {
            if (items[i] > item)
                items[i + 1] = items[i];
            else
                break;
        }

        return i + 1;
    }

    public int remove() {
        if (isEmpty())
            throw new IllegalStateException();
        return items[--count];
    }

    public boolean isFull() {
        return count == items.length;
    }

    public boolean isEmpty() {
        return count == 0;
    }

    @Override
    public String toString() {
        return Arrays.toString(items);
    }
}
```

# Hash Tables

## What are Hash Tables
- Spell checkers
- Dictionaries
- Compilers
- Code editors

- Java: HashMap
- JavaScript: Object
- Python: Dictionary
- C#: Dictionary

- Insert O(1)
- Lookup O(1)
- Delete O(1)

## Working with Hash Tables

Search "java map interface" in google

## Exercise: First Non-repeated Character

"A Green Apple" -> "G"

### My Solution
```Java
package com.lawjune;

import java.util.HashMap;
import java.util.Map;

public class Main {

    public static void main(String[] args) {
        System.out.println(getNonRepeatedChar("A Green Apple"));
    }

    public static char getNonRepeatedChar(String str) {
        StringBuffer sb = new StringBuffer(str);
        Map<Character, Boolean> map = new HashMap<>();
        for (int i = 0; i < sb.length(); i++) {
            if (map.containsKey(sb.charAt(i)))
                map.put(sb.charAt(i), true);
            else
                map.put(sb.charAt(i), false);;
        }

        for (int i = 0; i < sb.length(); i++) {
            if (!map.get(sb.charAt(i)))
                return sb.charAt(i);
        }

        throw new IllegalStateException();
    }
}
```

### Mosh's Solution
```Java
package com.lawjune;

import java.util.HashMap;
import java.util.Map;

public class CharFinder {
    public char findFirstNonRepeatingChar(String str) {
        Map<Character, Integer> map = new HashMap<>();

        var chars = str.toCharArray();

        for (var ch : chars) {
            var count = map.containsKey(ch) ? map.get(ch) : 0;
            map.put(ch, count + 1);
        }

        for (var ch : chars)
            if (map.get(ch) == 1)
                return ch;

        return Character.MIN_VALUE;
    }
}
```

## Sets

Maps: k -> v
Sets: k
Sets don't allow duplicate will end up with a unique list of values in this list. 

```Java
package com.lawjune;

import java.util.HashSet;
import java.util.Set;

public class Main {

    public static void main(String[] args) {
        Set<Integer> set = new HashSet<>();
        int[] numbers = { 1, 2, 3, 3, 2, 1, 4};
        for (var number : numbers)
            set.add(number);
        System.out.println(set);
    }

}
```

### Exercise: First Repeated Character

```Java
    public char findFirstRepeatedCharacter(String str) {
        Set<Character> set = new HashSet<>();
        var chars = str.toCharArray();
        for (var ch : chars) {

            if (set.contains(ch))
                return ch;
            set.add(ch);
        }
        return Character.MIN_VALUE;
    }
```

## Hash Functions

```Java
package com.lawjune;

import java.util.HashMap;
import java.util.Map;

public class Main {

    public static void main(String[] args) {
        Map<Integer, String> map = new HashMap<>();
        map.put(123456, "JunLuo");;
        System.out.println(hash(123456));
    }

    public static int hash(int number) {
        return number % 100;
    }

}
```

```Java
package com.lawjune;

import java.util.HashMap;
import java.util.Map;

public class Main {

    public static void main(String[] args) {
        Map<String, String> map = new HashMap<>();
        map.put("123456-A", "JunLuo");;
        System.out.println(hash("123456-A"));
    }

    public static int hash(String key) {
        int hash = 0;
        for (var ch : key.toCharArray())
            hash += ch;
        return hash % 100;
    }

}
```

```Java
        String str = "orange";
        System.out.println(str.hashCode());
```
Output is a negative number "-1008851410", obviously we cannot use this as an index value. Because we're not in the context of data structures.

We're not inside a hash table. This just numeric representation of "orange" based on the algorithm inside this method.


## Collisions

### Chaining 

{K=6, V=A}
{K=8, V=B}
{K=11, V=C}
 
 0	| |
 1	| | -> A -> C
 2	| |
 3	| | -> B
 4	| |

### Open Addressing

#### Linear Probing

 0	|       |
 1	|  6,A  | Linear Probing: hash(key) + i
 2	|  11,C | <- Probing
 3	|  8,B  | 
 4	|       |

#### Quadratic Probing

	Linear		|	Quadratic
  hash(key) + i |  hash(key) + i.pow(2)
				|  
				
index: (hash(key) + i).pow(2) % table_szie

#### Double Hashing

hash2(key) = prime - (key & prime)

index: (hash1(key) + i * hash2(key)) % table_size

hash2(key) = 3 - (key & prime)
 0	|       |
 1	|  6,A  | 
 2	|  11,C | -> index = (1 + 1 * 1) % 5 = 2
 3	|  8,B  | 
 4	|       |

## Exercise: Build a Hash Table

- HashTable
- put(k, v)
- get(k): v
- remove(k)
- k:int
- v: string
- Collisions: chaining
- A private class wraps a key value pair -> Entry
- LinkedList<Entry>[]
- [ LL LL LL LL ]

### Solution - put()

```Java
package com.lawjune;

import java.util.LinkedList;

public class HashTable {
    private class Entry {
        private int key;
        private String value;

        public Entry(int key, String value) {
            this.key = key;
            this.value = value;
        }

        public int getKey() {
            return key;
        }
    }

    private LinkedList<Entry>[] entries = new LinkedList[5];

    public void put(int key, String value) {
        var index = hash(key);
        if (entries[index] == null)
            entries[index] = new LinkedList<Entry>();

        var bucket = entries[index];
        for (var entry : bucket) {
            if (entry.key == key) {
                entry.value = value;
                return;
            }
        }
        bucket.addLast(new Entry(key, value));
    }

    private int hash(int key) {
        // Math.abs(key)
        return key % entries.length;
    }
}
```

### Solution - get()
```Java
    public String get(int key) {
        var index = hash(key);
        var bucket = entries[index];

        if (entries[index] != null) {
            for (var entry : bucket) {
                if (entry.key == key)
                    return entry.value;
            }
        }
        return null;
    }
```

### Solution: remove()
```Java
    public void remove(int key) {
        var index = hash(key);
        var bucket = entries[index];

        if (entries[index] == null)
            throw new IllegalStateException();
        for (var entry : bucket) {
            if (entry.key == key)
                bucket.remove(entry);
            return;
        }
        throw new IllegalStateException();
    }
```

### Refactor
```Java
package com.lawjune;

import java.util.LinkedList;

public class HashTable {
    public void put(int key, String value) {
        var entry = getEntry(key);
        if (entry != null) {
            entry.value = value;
            return;
        }

        getOrCreateBucket(key).addLast(new Entry(key, value));
    }

    public String get(int key) {
        var entry = getEntry(key);
        return (entry == null) ? null : entry.value;
    }

    public void remove(int key) {
        var entry = getEntry(key);
        if (entry == null)
            throw new IllegalStateException();
        getBucket(key).remove(entry);
    }

    private class Entry {
        private int key;
        private String value;

        public Entry(int key, String value) {
            this.key = key;
            this.value = value;
        }

        public int getKey() {
            return key;
        }

    }
    private LinkedList<Entry>[] entries = new LinkedList[5];

    private LinkedList<Entry> getBucket(int key) {
        return entries[hash(key)];
    }

    private LinkedList<Entry> getOrCreateBucket(int key) {
        var index = hash(key);
        var bucket = entries[index];
        if (bucket == null)
            entries[index] = new LinkedList<>();

        return bucket;
    }

    private Entry getEntry(int key) {
        var bucket = getBucket(key);
        if (bucket != null) {
            for (var entry : bucket) {
                if (entry.key == key)
                    return entry;
            }
        }
        return null;
    }

    private int hash(int key) {
        // Math.abs(key)
        return key % entries.length;
    }
}
```

## Summary

- HASH TABLES
	- To store key/value pairs
	- Insert, remove, lookup run in O(1)
	- Hash function
	- Collision
		- Chaining
		- Open addressing
			PROBING
	+-------------+
	+ Linar       + (hash1 + i) % table_size
	+-------------+
	+ Quadratic   + (hash1 + i.pow(2)) % table_size
	+-------------+
	+ Double Hash + (hash1 + i * hash2) % table_size
	+-------------+

		