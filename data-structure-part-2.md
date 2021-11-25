# Binary Trees

## What are Tress

A tree is a data structure that stores elements in a hierarchy refer to these elements as nodes and lines that connect them as edges.

Each node contains a value or data.

ROOT - LEAF

### Usage of Trees
- Represent hierarchical data
- Databases
- Autocompletion 
	- Chrome stores all your past web searches in a tree
- Compliers
- Compression (JPEG, MP3)

### Binary Search Tree

	      (7)
	      /  \
	   (4)   (8)    left < node < right 
	   /  \    \
	(1)   (6)  (9)

It allows us to quickly lookup data.

In a binary search tree, the value of any node is always greater than the value of this left child, and less t

- Lookup O(log n)
- Insert O(log n)
- Delete O(log n)

## Build a Tree

- Tree (root)
- Node (value, leftChild, rightChild)
- insert(value)
- find(value):boolean

- var current = root;
- current = current.leftChild;

### My Solution
```Java
package com.lawjune;

public class Tree {han the value of its right child. 

    private Node root;
    private class Node {
        private int value;
        private Node leftChild;
        private Node rightChild;

        public Node(int value) {
            this.value = value;
        }
    }

    public Tree(int rootValue) {
        this.root = new Node(rootValue);
    }


    public void insert(int value) {

        var current = root;
        var previous = root;

        while (current != null) {

            if (current.value == value) return;;

            previous = current;
            if (current.value > value) {
                current = current.leftChild;
            } else {
                current = current.rightChild;
            }
        }

        current = new Node(value);
        if (previous.value > value) previous.leftChild = current;
        else previous.rightChild = current;
    }

    public boolean find(int value) {
        var current = root;

        while (current != null) {

            if (current.value == value) return true;;

            if (current.value > value) {
                current = current.leftChild;
            } else {
                current = current.rightChild;
            }
        }

        return false;
    }

}
```

### Mosh's Solution - insert()
```Java
package com.lawjune;

public class Tree {
    private class Node {
        private int value;
        private Node leftChild;
        private Node rightChild;

        public Node(int value) {
            this.value = value;
        }

        @Override
        public String toString() {
            return "Node=" + value;
        }
    }

    private Node root;

    public void insert(int value) {
        var node = new Node(value);

        if (root == null) {
            root = node;
        }

        var current = root;
        while (true) {
            if (value == current.value) break;
            if (value < current.value) {
                if (current.leftChild == null) {
                    current.leftChild = node;
                    break;
                }
                current = current.leftChild;
            }

            else {
                if (current.rightChild == null) {
                    current.rightChild = node;
                    break;
                }
                current = current.rightChild;
            }
        }
    }
}
```

### Mosh's Solution - find()
```Java
    public boolean find(int value) {
        var current = root;
        while (current != null) {
            if (value < current.value)
                current = current.leftChild;
            else if (value > current.value)
                current = current.rightChild;
            else
                return true;
        }
        return false;
    }
```

## Tree Traversal
		  (7)
	      /  \
	   (4)   (8)    
	   /  \    \
	(1)   (6)  (9)
- **BREADTH FIRST**
	- Level Order
	- (7)
	- (4) -> (8)
	- (1) -> (6) -> (9)

- **DEPTH FIRST**
	- Pre-order => **Root**, Left, Right
		- 7, 4, 6, 1, 8, 9
	- In-order => Left, **Root**, Right
		- 1, 4, 6, 7, 8, 9
	- Post-order => Left, Right, **Root**
		- 1, 6, 4, 9, 8, 7

### Recursion

```Java
    // 4! = 4 * 3 * 2 * 1
    // 3! = 3 * 2 * 1
    public static int factorial(int n) {

        var factorial = 1;
        for (var i = n; i > 1; i--)
            factorial *= i;
        return factorial;
    }
```

Recursion is another approach for implementing repetion in the code without using a loop.

```Java
    // 4! = 4 * 3!
    // n! = n * (n - 1)!
    public static int factorial(int n) {
        // Base condition
        if (n == 0)
            return 1;
        return n * factorial(n - 1);
    }
```

### Depth First Traversals

```Java
package com.lawjune;

public class Tree {
    private class Node {
        private int value;
        private Node leftChild;
        private Node rightChild;

        public Node(int value) {
            this.value = value;
        }

        @Override
        public String toString() {
            return "Node=" + value;
        }
    }

    private Node root;

    public void insert(int value) {
        var node = new Node(value);

        if (root == null) {
            root = node;
        }

        var current = root;
        while (true) {
            if (value == current.value) break;
            if (value < current.value) {
                if (current.leftChild == null) {
                    current.leftChild = node;
                    break;
                }
                current = current.leftChild;
            }

            else {
                if (current.rightChild == null) {
                    current.rightChild = node;
                    break;
                }
                current = current.rightChild;
            }
        }
    }

    public boolean find(int value) {
        var current = root;
        while (current != null) {
            if (value < current.value)
                current = current.leftChild;
            else if (value > current.value)
                current = current.rightChild;
            else
                return true;
        }
        return false;
    }

    public void traversePreOrder() {
        traversePreOrder(root);
    }

    private void traversePreOrder(Node root) {
        // Basic Condition
        if (root == null)
            return;

        System.out.println(root.value);
        traversePreOrder(root.leftChild);
        traversePreOrder(root.rightChild);
    }

    public void traverseInOrder() {
        traverseInOrder(root);
    }

    private void traverseInOrder(Node root) {
        if (root == null)
            return;

        traversePreOrder(root.leftChild);
        System.out.println(root.value);
        traversePreOrder(root.rightChild);
    }

    public void traversePostOrder() {
        traverseInOrder(root);
    }

    private void traversePostOrder(Node root) {
        if (root == null)
            return;

        traversePreOrder(root.leftChild);
        traversePreOrder(root.rightChild);
        System.out.println(root.value);
    }
}
```

## Depth and Height of Nodes

***1 + max(height(L), height(R))***

```Java
    public  int height() {
        return height(root);
    }

    private int height(Node root) {
        if (root == null)
            return -1;

        if (root.leftChild == null && root.rightChild == null)
            return 0;

        return 1 + Math.max(
                height(root.leftChild),
                height((root.rightChild)));
    }
```

## Minimum Value in a Tree

### Binary Tree
```Java
    public int min() {
        return min(root);
    }

    private int min(Node root) {
        if (isLeaf(root))
            return root.value;
        var left = min(root.leftChild);
        var right = min(root.rightChild);
        return Math.min(Math.min(left, right), root.value);
    }
```

### Binary Search Tree
```Java
    // O(log n)
    public int min() {
        if (root == null)
            throw new IllegalStateException();

        var curent = root;
        var last = curent;
        while (curent != null ) {
            last = curent;
            curent = curent.leftChild;
        }

        return last.value;
    }
```

## Equality Checking 
```Java
    public boolean equals(Tree other) {
        if (other == null)
            return false;
        return equals(root, other.root);
    }

    private boolean equals(Node first, Node second) {
        if (first == null && second == null)
            return true;

        if (first != null && second != null) {
            return first.value == second.value
                    && equals(first.leftChild, second.leftChild)
                    && equals(first.rightChild, second.rightChild);
        }

        return false;
    }
```

## Validate Binary Search Tree

```Java
    public boolean isBinarySearchTree() {
        return isBinarySearchTree(root, Integer.MIN_VALUE, Integer.MAX_VALUE);
    }

    private boolean isBinarySearchTree(Node root, int min, int max) {
        if (root == null)
            return true;

        if (root.value < min || root.value > max)
            return false;

        return isBinarySearchTree(root.rightChild, root.value + 1, max)
                && isBinarySearchTree(root.leftChild, min, root.value - 1);
    }
```

## Nodes at K Distance from The Root

```Java
    public ArrayList<Integer> getNodesAtDistance(int distance) {
        var list = new ArrayList<Integer>();
        getNodesAtDistance(root, distance, list);

        return list;
    }

    private void getNodesAtDistance(Node root, int distance, ArrayList<Integer> list) {
        if (root == null)
            return;

        if (distance == 0) {
            list.add(root.value);
            return;
        }

//        distance = distance -1;
        getNodesAtDistance(root.leftChild, distance-1, list);
        getNodesAtDistance(root.rightChild, distance-1, list);
    }
```

## Level Order Traversal
```Java
    public void traversalLevelOrder() {
        for (var i = 0; i <= height(); i++) {
            var list = getNodesAtDistance(i);
            System.out.println(list);
        }
    }
```

# AVL Trees

## Balanced and Unbalanced Trees

**SELF-BALANCING TRESS**
- AVL Trees (Adelson-Velsky and Landis)
- Red-black Trees
- B-trees
- Splay Trees
- 2-3 Trees

## Rotations

height(left) - height(right) <= 1

**4 TYPES OF ROTATIONS**
- Left (LL)
- Right (RR)
- Left-Right (LR)
- Right-Left (RL)

## AVL Trees

### Building an AVL Tree
- AVLTree
- AVLNode
- insert() - recursion

```Java
package com.lawjune;

public class AVLTree {

    private class AVLNode {
        private int value;
        private AVLNode leftChild;
        private AVLNode rightChild;

        public AVLNode(int value) {
            this.value = value;
        }

        @Override
        public String toString() {
            return "AVLNode=" + value;
        }
    }

    private AVLNode root;

    public void insert(int value) {
        root = insert(root, value);
    }

    private AVLNode insert(AVLNode root, int value) {
        if (root == null)
            return new AVLNode(value);
        if (root.value > value)
            root.leftChild = insert(root.leftChild, value);
        if (root.value < value)
            root.rightChild = insert(root.rightChild, value);
        return root;
    }
}
```

### Height Calculation

```Java
    private AVLNode insert(AVLNode root, int value) {
        if (root == null)
            return new AVLNode(value);
        if (root.value > value)
            root.leftChild = insert(root.leftChild, value);
        if (root.value < value)
            root.rightChild = insert(root.rightChild, value);

        // root.height = MAX(left, right) + 1
        root.height = 1 + Math.max(height(root.leftChild), height(root.rightChild));
        return root;
    }

    private int height(AVLNode root) {
        return (root == null) ? -1 : root.height;
    }
```

### Balance Factor

```Java
    private AVLNode insert(AVLNode root, int value) {
        if (root == null)
            return new AVLNode(value);
        if (root.value > value)
            root.leftChild = insert(root.leftChild, value);
        if (root.value < value)
            root.rightChild = insert(root.rightChild, value);

        // root.height = MAX(left, right) + 1
        root.height = 1 + Math.max(height(root.leftChild), height(root.rightChild));

        // balanceFactor = height(L) - height(R)
        // > 1 => left heavy
        // < -1 => right heavy
        if (isLeftHeavy(root))
            System.out.println(root.value + " is left heavy");
        else if (isRightHeavy(root))
            System.out.println(root.value + " is right heavy");

        return root;
    }

    private boolean isLeftHeavy(AVLNode node) {
        return balanceFactor(node) > 1;
    }

    private boolean isRightHeavy(AVLNode node) {
        return balanceFactor(node) < -1;
    }

    private int balanceFactor(AVLNode node) {
        return (node == null) ? 0 : height(node.leftChild) - height(node.rightChild);
    }
```

### Detecting Rotations

10
  20 (-1)
    30
leftRotate(10)

10 
  30 (1) balanceFactor(root.right) > 0
20
rightRotate(30)
leftRotate(10)

```Java
    private void balance(AVLNode root) {
        if (isLeftHeavy(root))
        {
            if (balanceFactor(root.leftChild) < 0)
                System.out.println("Left rotate" + root.leftChild.value);
            System.out.println("Right rotate " + root.value);
        }
        else if (isRightHeavy(root)) {
            if (balanceFactor(root.rightChild) > 0)
                System.out.println("Right rotate " + root.rightChild.value);
            System.out.println("Left rotate " + root.value);
        }
    }
```

### Implementing Rotations

10 root
   20 newRoot
15    30
leftRotate(10)

newRoot = root.right
root.right = newRoot.left
newRoot.left = root

reset height of root/newRoot

   20
10    30
   15

```Java
    private AVLNode insert(AVLNode root, int value) {
        if (root == null)
            return new AVLNode(value);
        if (root.value > value)
            root.leftChild = insert(root.leftChild, value);
        if (root.value < value)
            root.rightChild = insert(root.rightChild, value);

        // root.height = MAX(left, right) + 1
        setHeight(root);
        return balance(root);
    }

    private AVLNode balance(AVLNode root) {
        if (isLeftHeavy(root))
        {
            if (balanceFactor(root.leftChild) < 0)
                root.leftChild = rotateLeft(root.leftChild);
            return rotateRight(root);
        }
        else if (isRightHeavy(root)) {
            if (balanceFactor(root.rightChild) > 0)
              root.rightChild = rotateRight(root.rightChild);
            return rotateLeft(root);
        }

        return root;
    }

    private AVLNode rotateLeft(AVLNode root) {
        var newRoot = root.rightChild;

        root.rightChild = newRoot.leftChild;
        newRoot.leftChild = root;

        setHeight(root);
        setHeight(newRoot);

        return newRoot;
    }

    private AVLNode rotateRight(AVLNode root) {
        var newRoot = root.leftChild;

        root.leftChild = newRoot.rightChild;
        newRoot.rightChild = root;

        setHeight(root);
        setHeight(newRoot);

        return newRoot;
    }

    private void setHeight(AVLNode node) {
        node.height = Math.max(height(node.leftChild), height(node.rightChild)) + 1;
    }
```

# Heaps

## What are Heaps?
A heap is a speical type of tree with two properties. The first property is that it's a complete tree, which means every level except potentially the last level is completely filled, and levels are filled from the left to the right.

### The 1st Property: COMPLETE

**Complete example 1**
      T
  T       T
T   T   T   T

**Complete example 2**
      T
  T       T
T   T   T   

**Complete example 3 - Not Complete**
      T
  T       T
T   T       T
There is a "hole" in the last level.

**Complete example 4 - Not Complete**
      T
  T       
T   T       
There is a "hole" in the last level.

### The 2nd Property: HEAP PROPERTY
The value of every node is greater than or equal with children.

      20 **MAX HEAP**: The root node holds the largest value.
  10       15
4    5   6  

=> Binary heap, because it's a binary tree.

### Application of Heaps
- Sorting (HeapSort)
- Graph alogorithms (shortest path)
    - This is the algorithm that powers your GPS
- Priority queues
- Finding the Kth smallest/largest value

height = log(n) => O(log(n))

## Building a Heap

***Using array***

                 [0]20 
     [1]10              [2]15
[3]4       [4]5      

left = parent * 2 +1
right = parent * 2 + 2

- Heap
- int[]
- insert(int)
- remove

### Solution - insert()
```Java
package com.lawjune;

import java.util.Arrays;

public class Heap {
    private int[] items = new int[10];
    private int size;

    public void insert(int value) {

        if (isFull())
            throw new IllegalStateException();

        items[size++] = value;
        bubbleUp();
    }

    public boolean isFull() {
        return size == items.length;
    }

    private void bubbleUp() {
        var index = size - 1;
        while (index > 0 && items[index] > items[parent(index)]) {
            swap(index, parent(index));
            index = parent(index);
        }
    }

    private void swap(int first, int second) {
        var temp = items[first];
        items[first] = items[second];
        items[second] = temp;
    }

    private int parent(int index) {
        return (index - 1) / 2;
    }

    @Override
    public String toString() {
        return Arrays.toString(items);
    }
}
```

### Solution - remove()
```Java
    public void remove() {

        if (isEmpty())
            throw new IllegalStateException();

        items[0] = items[--size ];
        // item (root) < children
        var index = 0;
        while (index <= size && !isValidParent(index)) {
            var largerChildIndex = largerChildIndex(index);
            swap(index, largerChildIndex);
            index = largerChildIndex;
        }
    }

    public boolean isEmpty () {
        return size == 0;
    }

    private int largerChildIndex(int index) {
        return (leftChild(index) > rightChild(index)) ?
                        leftChildIndex(index) :
                        rightChildIndex(index);
    }

    private boolean isValidParent(int index) {
        return items[index] >= leftChild(index) && items[index] >= rightChild(index);
    }

    private int leftChild(int index) {
        return items[leftChildIndex(index)];
    }

    private int rightChild(int index) {
        return items[rightChildIndex(index)];
    }

    private int leftChildIndex(int index) {
        return index * 2 + 1;
    }

    private int rightChildIndex(int index) {
        return index * 2 + 2;
    }
``` 

### Egde Cases

```Java
    private int largerChildIndex(int index) {

        if (!hasLeftChild(index))
            return index;

        if (!hasRightChild(index))
            return leftChildIndex(index);

        return (leftChild(index) > rightChild(index)) ?
                        leftChildIndex(index) :
                        rightChildIndex(index);
    }

    private boolean hasLeftChild(int index) {
        return leftChildIndex(index) <= size;
    }

    private boolean hasRightChild(int index) {
        return rightChildIndex(index) <= size;
```

```Java
    private boolean isValidParent(int index) {

        if (!hasLeftChild(index))
            return true;

        var isValid = items[index] >= leftChild(index);

        if(!hasRightChild(index))
            isValid = isValid & items[index] >= rightChild(index);
        
        return isValid;
    }
```

```Java
    public int remove() {

        if (isEmpty())
            throw new IllegalStateException();

        var root = items[0];
        items[0] = items[--size ];
        bubbleDown();

        return root;
    }

    private void bubbleDown() {
        var index = 0;
        while (index <= size && !isValidParent(index)) {
            var largerChildIndex = largerChildIndex(index);
            swap(index, largerChildIndex);
            index = largerChildIndex;
        }
    }
```

## Heap Sort

```Java
        int[] numbers = { 5, 3, 10, 1, 4, 2};
        var heap = new Heap();
        for (var number : numbers)
            heap.insert(number);
//        for (var i = 0; i < numbers.length; i++)
//            numbers[i] = heap.remove();
//        System.out.println(Arrays.toString(numbers));

        for (var i = numbers.length - 1; i >= 0; i--)
            numbers[i] = heap.remove();
        System.out.println(Arrays.toString(numbers));
```

### Priority Queues

insert: O(n) / Heap - O(log n)
delete: O(1) / Heap - O(log n)

```Java
package com.lawjune;

public class PriorityQueueWithHeap {
    private Heap heap = new Heap();

    public void enqueue(int item) {
        heap.insert(item);
    }

    public int dequeue() {
        return heap.remove();
    }

    public boolean isEmpty() {
        return heap.isEmpty();
    }
}
```

## Heapify

### Mosh's Solution

```Java
package com.lawjune;

public class MaxHeap {
    public static void heapify(int[] array) {
        for (var i = 0; i < array.length; i++)
            heapify(array, i);
    }

    private static void heapify(int[] array, int index) {
        var largerIndex = index;

        var leftIndex = index * 2 + 1;
        if (leftIndex < array.length && array[leftIndex] > array[largerIndex])
            largerIndex = leftIndex;

        var rightIndex = index * 2 + 2;
        if (rightIndex < array.length && array[rightIndex] > array[largerIndex])
            largerIndex = rightIndex;

        if (index == largerIndex)
            return;

        swap(array, index, largerIndex);
        heapify(array, largerIndex);
    }

    private static void swap(int[] array, int first, int second) {
        var temp = array[first];
        array[first] = array[second];
        array[second] = temp;
    }
}
```

### Mosh's Optimization

***lastParent = (n/2) - 1***

```Java
    public static void heapify(int[] array) {

        var lastParentIndex = array.length / 2 - 1;
        for (var i = lastParentIndex; i >= 0; i--)
            heapify(array, i);
    }
```

### Kth Largest Item

```Java
    public static int getKthLargest(int[] array, int k) {
        if (k < 1 || k > array.length)
            throw new IllegalStateException();

        var heap = new Heap();
        for (var number : array)
            heap.insert(number);
        for (var i = 0; i < k - 1; i++)
            heap.remove();

        return heap.max();
    }
```

## Summary

- Insert   O(log n)
- Remove   O(log n)
- Get Max  O(1)

# Tries

## What are Tries?

Re**trie**val
- Digital
- Radix
- Prefix

***Example - Suggestions of Google Search***

Auto completion is one of the key applications of tries.

**Why not arrays (of strings)?**
- If you have a large number of words or search queries, this array is going to waste a lot of space because a lot of words have the same prefix.
    - For example, pig, picky pickle, picture, picnic, all start with pic.
- Looking at words that start with a prefix using arrays is relatively slow, we have to go through every word and check to see if the word starts with our prefix. 

Lookup O(L) -> **L**: Length of the word 
Insert O(L) 
Delete O(L)

## Exercise: Building a Trie

### Normal Solution

Trie 
    Node
        value: char
        children: Node[26]
        isEndOfWord: boolean

insert(word: String)
index = ch - 'a'
100('d') - 93 = 3 ('d')

```Java
package com.lawjune;

public class Trie {
    public static int ALPHABET_SIZE = 26;

    private class Node {
        private char value;
        private Node[] children = new Node[ALPHABET_SIZE];
        private boolean isEndOfWord;

        public Node(char value) {
            this.value = value;
        }

        @Override
        public String toString() {
            return "value=" + value;
        }
    }

    private Node root = new Node(' ');
    public void insert(String word) {
        var current = root;
        for (var ch : word.toCharArray()) {
            var index = ch - 'a';
            if (current.children[index] == null)
                current.children[index] = new Node(ch);
            current = current.children[index];
        }

        current.isEndOfWord = true;


    }
}
```

### An Implementation with a Hash Table

```Java
package com.lawjune;

import java.util.HashMap;

public class Trie {
    public static int ALPHABET_SIZE = 26;

    private class Node {
        private char value;
        private HashMap<Character, Node> children = new HashMap<>();
        private boolean isEndOfWord;

        public Node(char value) {
            this.value = value;
        }

        @Override
        public String toString() {
            return "value=" + value;
        }
    }

    private Node root = new Node(' ');
    public void insert(String word) {
        var current = root;
        for (var ch : word.toCharArray()) {
            if (current.children.get(ch) == null)
                current.children.put(ch, new Node(ch));
            current = current.children.get(ch);
        }

        current.isEndOfWord = true;

    }
}
```

### A Better Abstraction

```Java
package com.lawjune;

import java.util.HashMap;

public class Trie {
    public static int ALPHABET_SIZE = 26;

    private class Node {
        private char value;
        private HashMap<Character, Node> children = new HashMap<>();
        private boolean isEndOfWord;

        public Node(char value) {
            this.value = value;
        }

        @Override
        public String toString() {
            return "value=" + value;
        }

        public boolean hasChild(char ch) {
            return children.containsKey(ch);
        }

        public void addChild(char ch) {
            children.put(ch, new Node(ch));
        }

        public Node getChild(char ch) {
            return children.get(ch);
        }
    }

    private Node root = new Node(' ');
    public void insert(String word) {
        var current = root;
        for (var ch : word.toCharArray()) {
            if (!current.hasChild(ch))
                current.addChild(ch);
            current = current.getChild(ch);
        }

        current.isEndOfWord = true;

    }
}
```

## Exercise: Looking Up a Word
```Java
    public boolean contains(String word) {
        if (word == null)
            return false;

        var current = root;
        for (var ch : word.toCharArray()) {
            if (!current.hasChild(ch))
                return false;
            current = current.getChild(ch);
        }

        return current.isEndOfWord;
    }
```

## Traversals

### Pre-order Traversal

```Java
    public void traverse() {
        traverse(root);
    }

    private void traverse(Node root) {
        // Pre-order: visit the root first
        System.out.println(root.value);

        for (var child: root.getChildren())
            traverse(child);
    }
```

### Post-order Traversal

```Java
    private void traverse(Node root) {

        for (var child: root.getChildren())
            traverse(child);

        // Post-order: visit the root first
        System.out.println(root.value);

    }
```

## Exercise: Removing a Word

```Java
        public boolean hasChildren() {
            return !children.isEmpty();
        }

        public void removeChild(char ch) {
            children.remove(ch);
        }
```


```Java
    private void remove(Node root, String word, int index) {
        if (index == word.length()) {
            root.isEndOfWord = false;
            return;
        }

        var ch = word.charAt(index);
        var child = root.getChild(ch);
        if (child == null)
            return;

        remove(child, word, index + 1);

        if (!child.hasChildren() && !child.isEndOfWord)
            root.removeChild(ch);
    }
```

## Auto Completion

    c          e
    a          g
    r          g
  d   e
      f
      u
      l

card
careful

Node root
String word
List<String> words

```Java
    public List<String> findWords(String prefix) {
        List<String> words = new ArrayList<>();
        var lastNode = findLastNodeOf(prefix);
        findWords(lastNode, prefix, words);

        return words;
    }

    private void findWords(Node root, String prefix, List<String> words) {
        if (root == null)
            return;

        if (root.isEndOfWord)
            words.add(prefix);

        for (var child : root.getChildren())
            findWords(child, prefix + child.value, words);
    }

    private Node findLastNodeOf (String prefix) {
        if (prefix == null)
            return null;

        var current = root;
        for (var ch : prefix.toCharArray()) {
            var child = current.getChild(ch);
            if (child == null)
                return null;
            current = child;
        }
        return current;
    }
```

## Summary

- Insert O(L)
- Lookup O(L)
- Delete O(L)


# Graphs

## What are Graphs

- Such as the routers in a network or people on a social media platform.

- Using a graph, you can see how people are connected, and how strong these connections are.

- Just like trees, graphs consist of nodes and edges. 
    - In fact, mathematically speaking, a tree is a kind of a graph.
    - It's a graph without any cycles.
    - Also, mostly it doesn't have a root node.

- Using weights t orepresent how strong a connection is.
    - In a social media platform, if two people interact a lot, we can put a higher weight on their connection.
    - Later we can show their best frieds by finding the neighboring node with the highest weights.

- Another application of graphs is in finding the shortest path between two nodes.


## Adjacency Matrix 

      John   Mary   Bob   Alice

John    0      1     1      1

Mary    0      0     1      1

Bob     0      0     0      0

Alice   0      0     1      0

*The approach of using a two dimensional array is the amount of space we need to allocate for this matrix - Space:O(n.pow(2))*

Add Node: O(n.pow(2))

Time complexity in terms of V: **Vertices**
The time complexity of certain operations also depend on the number of edges.

Remove Node: O(V.pow(2))

Space: O(V.pow(2))
Add Egde: O(1)
Remove Edge: O(1)
Query Edge: O(1)
Find Neighbors: O(V)
Add Node: O(V.pow(2))
Remove Node: O(V.pow(2))


## Adjacency List

0: (1) -> (2) -> (3)

1: (2) -> (3)

2: 

3: (1)

Space: O(V + E)
E = Total Edges
**DENSE GRAPH**: Every node connects to each other: E = V x (V - 1) = V.pow(2) - V
=> O(V + E) = O(V.pow(2))

- Add Node: O(1)
- Remove Node: O(V + E) = O(V.pow(2))
    - Remove the corresponding element from the adjacentcy list.
    - Make sure no other nodes have a link to this node. 
    => Iterate over the entire adjacency list and remove the target node from every link. 

- Add Edge: O(K) -> Worst Case: O(V)
- Remove Edge: O(K) -> Worst Case: O(V)
- Query Edge: O(K) -> Worst Case: O(V)
- Find Neighbors: O(K) -> Worst Case: O(V)


                MATRIX           LIST
Space        O(V.pow(2))      O(V + E)
Add Edge        O(1)             O(K)
Remove Edge     O(1)             O(K)
Query Edge      O(1)             O(K)
Find Neighbors  O(V)             O(K)
Add Node     O(V.pow(2))         O(1) 
Remove Node  O(V.pow(2))       O(V.pow(2)) 

***If you process a DENSE graph, implement your graph for the matrix, otherwise use list. In reality, the adjacency list is often better to represent graphs.***

## Build a Graph

Graph 
    Node
        label: String
    addNide(label)
    removeNode(label)
    addEdge(from, to)
    removeEdge(from, to)
    print()
        A is connected with [B, C]
        B is connected with [A]

### My Solution
```Java
package com.lawjune;

import java.util.HashMap;
import java.util.LinkedList;

public class MyGraph {

    private HashMap<String, Node> items = new HashMap<>();

    private class Node {
        private String label;
        private LinkedList<String> edges = new LinkedList<>();
        public Node(String label) {
            this.label = label;
        }
        public void connect(String label) {
            if (label == null)
                throw new IllegalStateException();

            if (label == this.label)
                throw new IllegalStateException();
            edges.add(label);
        }
    }

    public void addNode(String label) {
        if (items.containsKey(label))
            throw new IllegalStateException();

        items.put(label, new Node(label));
    }

    public void removeNode(String label) {
        if (!items.containsKey(label))
            throw new IllegalStateException();

        items.remove(label);
    }

    public void addEdge(String from, String to) {
        if (!items.containsKey(from) || !items.containsKey(to))
            throw new IllegalStateException();

        items.get(from).connect(to);
    }

    public void print() {
        for (String label : items.keySet())
            System.out.println(label + " is " + "connected with " + items.get(label).edges);
    }
}
```

### Mosh's Solution - Adding Nodes and Edges

```Java
package com.lawjune;

import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

public class Graph {

    private class Node {
        private String label;

        public Node(String label) {
            this.label = label;
        }

        @Override
        public String toString() {
            return label;
        }
    }

    private Map<String, Node> nodes = new HashMap<>();
    private Map<Node, List<Node>> adjacencyList = new HashMap<>();

    public void addNode(String label) {
        var node = new Node(label);
        nodes.putIfAbsent(label, node);
        adjacencyList.putIfAbsent(node, new ArrayList<>());
    }

    public void addEdge(String from, String to) {
        var fromNode = nodes.get(from);
        if (fromNode == null)
            throw new IllegalStateException();

        var toNode = nodes.get(to);
        if (toNode == null)
            throw new IllegalStateException();

        adjacencyList.get(fromNode).add(toNode);
    }

    public void print() {
        for (var source : adjacencyList.keySet()) {
            var targets = adjacencyList.get(source);
            if (!targets.isEmpty())
                System.out.println(source + "is connected to " + targets);
        }
    }
}
```

### Mosh's Solution: Removing Nodes and Edges

```Java
    public void removeNode(String label) {
        var node = nodes.get(label);
        if (node == null)
            return;

        for (var n : adjacencyList.keySet())
            adjacencyList.get(n).remove(node);

        adjacencyList.remove(node);
        nodes.remove(node);
    }

    public void removeEdge(String from, String to) {
        var fromNode = nodes.get(from);
        var toNode = nodes.get(to);

        if (fromNode == null || toNode == null)
            return;

        adjacencyList.get(fromNode).remove(toNode);
    }
```

## Traversal Algorithms

### Depth-first Traversal (Recursive)

```Java
    public void traverseDepthFirst(String root) {
        var node = nodes.get(root);
        if (node == null)
            return;;

        traverseDepthFirst(node, new HashSet<>());
    }

    private void traverseDepthFirst(Node root, Set<Node> visited) {
        System.out.println(root);
        visited.add(root);

        for (var node : adjacencyList.get(root))
            if (!visited.contains(node))
                traverseDepthFirst(node, visited);
    }
```

### Depth-first Traversal (Iterative)

**How the Java Runtime executes a method**

Call Stack [x, y]

methodA(x
    methodB(y)

=>

Call Stack [x]

methodA(x
    methodB(y)
    print(x)

- push(root)
- while(stack is not empty)
- current = pop()
- visit(current)
- push each unvisited neighbour onto the stack

```Java
    public void traverseDepthFirst(String root) {
        var node = nodes.get(root);
        if (node == null)
            return;;

//        traverseDepthFirst(node, new HashSet<>());

        Set<Node> visited = new HashSet<>();
        Stack<Node> stack = new Stack<>();
        stack.push(node);

        while (!stack.isEmpty()) {
            var current = stack.pop();

            if (visited.contains(current))
                continue;

            System.out.println(current);
            visited.add(current);

            for (var neighbour : adjacencyList.get(current))
                if (!visited.contains(neighbour))
                    stack.push(neighbour);
        }
    }
```

## Exercise: Breadth-first Traversal

A

Front [A] Back

=>

A

Front [B, C] Back

=>

A B

Front [C, D] Back

```Java
    public void traverseBreadthFirst(String root) {
        var node = nodes.get(root);
        if (node == null)
            return;;

//        traverseDepthFirst(node, new HashSet<>());

        Set<Node> visited = new HashSet<>();
        Queue<Node> queue = new ArrayDeque<>();
        queue.add(node);

        while (!queue.isEmpty()) {
            var current = queue.remove();

            if (visited.contains(current))
                continue;

            System.out.println(current);
            visited.add(current);

            for (var neighbour : adjacencyList.get(current))
                if (!visited.contains(neighbour))
                    queue.add(neighbour);
        }
    }
```

## Exercise: Topological Sorting

Let's say we have a project like a web or a mobile app. And this project is dependent on the code and a few other projects. When we want to compile or build our project, all these dependencies should be compiled in the right order. 

**A graph without a cycle -> DIRECTED ACYCLIC GRAPTH**

- topologicalSort(): List<String>

### My Solution
```Java
   public List<String> myTopologicalSort() {

        var sorted = new LinkedList<String>();
        var visited = new HashSet<Node>();
//        var node = nodes.get(root);
//        if (node == null)
//            return sorted;;
        for (var label : nodes.keySet()) {
            var node = nodes.get(label);

            myTopologicalSort(node, visited, sorted);
        }
        return sorted;
    }

    private void myTopologicalSort(Node root, Set<Node> visited, List<String> sorted) {
//        System.out.println(root);
        visited.add(root);

        for (var node : adjacencyList.get(root))
            if (!visited.contains(node))
                myTopologicalSort(node, visited, sorted);
            sorted.add(root.label);
    }
```

### Mosh's Solution 

```Java
    public List<String> topologicalSort() {
        Stack<Node> stack = new Stack<>();
        Set<Node> visited = new HashSet<>();
        for (var node : nodes.values())
            topologicalSort(node, visited, stack);
        List<String> sorted = new ArrayList<>();
        while (!stack.empty())
            sorted.add(stack.pop().label);

        return sorted;
    }

    private void topologicalSort(Node node, Set<Node> visited, Stack<Node> stack) {
        if (visited.contains(node))
            return;

        visited.add(node);

        for (var neighbour : adjacencyList.get(node))
            topologicalSort(neighbour, visited, stack);

        stack.push(node);
    }
```

## CYCLE DETECTION

Keep 3 sets of nodes:
    - all
    - visiting
    - visited
The difference between the last two sets is that if you visit a node and all of his children, we putit in the visted set. But as long as we haven't visited all of the children of a node, we're going to keep it in the visiting set.

```Java
    public boolean hasCycle() {
        Set<Node> all = new HashSet<>();
        all.addAll(nodes.values());

        Set<Node> visiting = new HashSet<>();
        Set<Node> visited = new HashSet<>();

        while (!all.isEmpty()) {
//            var current = all.toArray(new Node[0])[0]; // Object
            var current = all.iterator().next();
            if (hasCycle(current, all, visiting, visited))
                return true;
        }

        return false;
    }

    private boolean hasCycle(Node node,
                             Set<Node> all,
                             Set<Node> visiting,
                             Set<Node> visited) {
        all.remove(node);
        visiting.add(node);

        for (var neighbour : adjacencyList.get(node)) {
            if (visited.contains(neighbour))
                continue;
            if (visiting.contains(neighbour))
                return true;
            if (hasCycle(neighbour, all, visiting, visited))
                return true;
        }

        visiting.remove(node);
        visited.add(node);
        return false;
    }
```

## Graph Summary

- To represent connected objects
- Implementation
    - Adjacency Matrix
    - Adjacency List
- Traversal algorithms
    - Breadth-first Search (BFS)
    - Depth-first Search (DFS)
