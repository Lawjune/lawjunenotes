
# Sorting

## Sorting Algorithms Introduction

- How they work
- Time & space complexity
- Implementation

**Sorting Algorithms**
- Bubble Sort
- Selection Sort
- Insertion Sort
- Merge Sort
- Quick Sort
- Counting Sort
- Bucket Sort

## Bubble Sort

### What is Bubble Sort?
                Best      Worst

Passes          O(1)       O(n)

Comparisons     O(n)       O(n)

**Total**     **O(n)**   **O(n.pow(2))**
             **Linear**  **Quadratic**

https://www.bigocheatsheet.com/

### Implementation - Bubble Sort

```java
package com.lawjune;

public class BubbleSort {

    public void sort(int[] array) {
        boolean isSorted;

        for (var i = 0; i < array.length; i++) {
            isSorted = true;
            for (var j = 1; j < array.length - i; j++)
                if (array[j] < array[j - 1]) {
                    swap(array, j, j - 1);
                    isSorted = false;
                }
            if (isSorted)
                return;
        }
    }

    private void swap(int[] arrry, int index1, int index2) {
        var temp = arrry[index1];
        arrry[index1] = arrry[index2];
        arrry[index2] = temp;
    }
}
```

## Selection Sort

### What is Selection Sort?

Multiple paths to sort the array. In each path we should choose the next smallest item, and move it to the correct position. 


[8, 2, 4, 1, 3] => Mimium item 1 in index(3)

=> Swap the index(3) and index(0)
[0, 2, 4, 8, 3]
[0] -> SORTED
[2, 4, 8, 3] -> UNSORTED => Mimium item 2 in index(1) as itself

[0, 2] -> SORTED
[4, 8, 3] -> UNSORTED => Mimium item 3 in index(4) to swap with index(2) with item 4

[0, 2, 3] -> SORTED
[8, 4] -> UNSORTED => Mimium item 34 in index(4) to swap with index(3) with item 8

                Best                Worst

Passes          O(n)                 O(n)

Comparisons     O(n)                 O(n)

**Total**  **O(n.pow(2))**      **O(n.pow(2))**
            **Quadratic**        **Quadratic**

### Implementation
```Java
package com.lawjune;

public class SelectionSort {
    public void sort(int[] array) {
        for (var i = 0; i < array.length; i++) {
            var minIndex = i;
            for (var j = i; j < array.length; j++)
                if (array[j] < array[minIndex])
                    minIndex = j;
            swap(array, minIndex, i);
        }
    }

    private void swap(int[] arrry, int index1, int index2) {
        var temp = arrry[index1];
        arrry[index1] = arrry[index2];
        arrry[index2] = temp;
    }
}

```

## Insertion Sort

### What is Insertion Sort?

Like playing cards.

[8, 2, 4, 1, 3] 

[8] -> SORTED
[2, 4, 1, 3] -> UNSORTED

=>

[2, 8] -> SORTED
[4, 1, 3] -> UNSORTED

=>

[2, 4, 8] -> SORTED
[1, 3] -> UNSORTED

=>

[1, 2, 4, 8] -> SORTED
[3] -> UNSORTED

                Best      Worst

Passes          O(n)       O(n)

Comparisons     O(1)       O(n)

**Total**     **O(n)**   **O(n.pow(2))**
             **Linear**  **Quadratic**

### Implementation

```Java
package com.lawjune;

public class InsertionSort {
    public void sort(int[] array) {
        for (var i = 1; i < array.length; i++) {
            var current = array[i];
            var j = i - 1;
            while (j >= 0 && array[j] > current) {
                array[j + 1] = array[j];
                        j--;
            }
            array[j + 1] = current;
        }
    }
}
```


## Merge Sort

### What is Merge Sort

[8, 2, 4, 1, 3] 

middle = length / 2 = 5 / 2 = 2 =>

[8, 2] [4, 1, 3]

[8] [2] => [2, 8]

[4] [1, 3] => [1, 3, 4]

**A Divide and Conquer Algorithm**

                Best        Worst

Dividing      O(log n)     O(log n)

Merging         O(n)         O(n)

**Total**   **O(log n)**  **O(log n)**
**Space**     **O(n)**     **O(n)**

***COST***: Additional allocating memory space!

*Search "in-place" mergesort in google!*

### Implementation

```Java
package com.company;

public class MergeSort {
    public void sort(int[] array) {
        // Basic condition
        if (array.length < 2)
            return;

        // Divide this array into half
        var middle = array.length / 2;

        int[] left = new int[middle];
        for (var i = 0; i < middle; i++)
            left[i] = array[i];

        int[] right = new int[array.length - middle];
        for (var i = middle; i < array.length; i++)
            right[i - middle] = array[i];

        // Sort each half
        sort(left);
        sort(right);

        // Merge the result
        merge(left, right, array);
    }

    private void merge(int[] left, int[] right, int[] result) {
        int i = 0, j = 0, k = 0;

        while (i < left.length && j < right.length) {
            if (left[i] <= right[j])
                result[k++] = left[i++];
            else
                result[k++] = right[j++];
        }

        while (i < left.length)
            result[k++] = left[i++];

        while (j < right.length)
            result[k++] = right[j++];
    }
}
```


## Quick Sort

### What is Quick Sort?

[15, 6, 3, 1, 22, 10, 13]
-> Choose [13] as pivot 
[6, 3, 1, 10, 13, 15, 22]
    - left partition: [6, 3, 1, 10]
    - right partition: [15, 22]
    - the pivot [13] is in the right position 

-> Then [10] as pivot
[6, 3, 1, 10, 13, 15, 22] 
=> [10] has already been in the right position

-> Then [1] as pivot
[1, 3, 6, 10, 13, 15, 22] 

-> Then [6], [3], [22] and [15] to be pivot 


### Partitioning  

[15, 6, 3, 1, 22, 10, 13]
-> Choose [13] as pivot 
=> i in [15]
=> b(boundary) in index(-1)

=> [6, 15, 3, 1, 22, 10, 13]
=> i in [3]
=> b(boundary) in [6]

=> [6, 3, 15, 1, 22, 10, 13]
=> i in [1]
=> b(boundary) in [3]

=> [6, 3, 1, 15, 22, 10, 13]
=> i in [22]
=> b(boundary) in [1]

=> [6, 3, 1, 15, 22, 10, 13] (No change)
=> i in [10]
=> b(boundary) in [15]

=> [6, 3, 1, 10, 22, 15, 13]
=> i in [13]
=> b(boundary) in [22]

=> [6, 3, 1, 10, 13, 15, 22]
=> pivot [13] has been already in the right position

**QUCIK SORT**

                 Best        Worst

-Partition       O(n)         O(n)
-#of times     O(log n)       O(n)
 
**Total**   **O(log n)**  **O(n.pow(2))**
**Space**   **O(log m)**     **O(n)**


**PIVOT SELECTION**
- Pick randomly
- Use the middle index
- Average of first, middle and last item

### Implementation

```Java
package com.company;

public class QuickSort {
    public void sort(int[] array) {
        sort(array, 0, array.length-1);
    }

    private void sort(int[] array, int start, int end) {
        if (start >= end)
            return;

        // Partitioning
        var boundary = partition(array, start, end);

        // Sort left
        sort(array, start, boundary - 1);

        // Sort right
        sort(array, boundary + 1, end);
    }

    private int partition(int[] array,  int start, int end) {
        var pivot = array[end];
        var boundary = start - 1;
        for (var i = start; i <= end; i++)
            if (array[i] <= pivot)
                swap(array, i, ++boundary);

        return boundary;
    }

    private void swap(int[] arrry, int index1, int index2) {
        var temp = arrry[index1];
        arrry[index1] = arrry[index2];
        arrry[index2] = temp;
    }
}
```

## Counting Sort

### Comparison Sorts and Non-Comparison Sorts

**COMPARISON SORTS**
- Bubble sort
- Selection sort
- Insertion sort
- Merge sort
- Quick sort

**NON-COMPARISON SORTS**
- Counting sort
- Bucket sort
- Radix sort       

### What is Counting Sort

[5, 3, 2, 5, 4, 4, 5] -> range: [0, k]

=> {0:0, 1:0, 2:1, 3:1, 4:2, 5:3}

[2], [3], [4, 4], [5, 5, 5] => [2, 3, 4, 4, 5, 5, 5]

Space: O(k)
Time: 
    - Populate counts: O(n)
    - Iterate count: O(k)
    - Total: O(n + k)

***Time-memory Trade-off***

**WHEN TO USE**
- Allocating extra space is not an issue
- Values are positive integers
- Most of the values in the range are present

### Impelementation 

```Java
package com.company;

public class CountingSort {
    public void sort(int[] array, int max) {
        int[] counts = new int[max + 1];
        for (var item : array)
            counts[item]++;

        var k = 0;
        for (var i = 0; i < counts.length; i++)
            for (var j = 0; j < counts[i]; j++)
                array[k++] = i;
    }
}
```


## Bucket Sort

### What is Bucket Sort

[6, 2, 5, 4, 3, 7]

Break into 3 buckets: bucket = item / numberOfBuckets

0> -> 2

1> -> 3, 4, 5

2> -> 6, 7

<0>    <1>     <2>
[2] [3, 4, 5] [6, 7]


Space: O(n + k) 
Time: 

                        Best        Worst

-Distribution           O(n)         O(n)
-Iterating buckets      O(k)         O(k)
 
**Sorting**           **O(1)**  **O(n.pow(2))**
**Total**            **O(n+k)** **O(n.pow(2))**

### Implementation 

```Java
package com.company;

import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class BucketSort {
    public void sort(int[] array, int numberOfBuckets) {
        var i = 0;
        for (var bucket : createBuckets(array, numberOfBuckets)) {
            Collections.sort(bucket);
            for (var item : bucket)
                array[i++] = item;
        }
    }

    private List<List<Integer>> createBuckets(int[] array, int numberOfBuckets) {
        List<List<Integer>> buckets = new ArrayList<>();
        for (var i = 0; i < numberOfBuckets; i++)
            buckets.add(new ArrayList<>());

        for (var item : array)
            buckets.get(item / numberOfBuckets).add(item);

        return buckets;
    }
}
```

 
# Searching

## Search Algorithms
- Linear Search
- Binary Search
- Ternary Search
- Jump Search
- Exponential Search 


## Linear Search

[6, 2, 5, 4, 3, 7]

                        Best        Worst

Time Complexity         O(1)         O(n)

```Java
package com.company;

public class Search {
    public int linearSearch(int[] array, int target) {
        for (var i = 0; i < array.length; i++)
            if (array[i] == target)
                return i;

        return -1;
    }
}
```


## Binary Search 

[3, 5, 6, 9, 11, 18, 20, 21, 24, 30] -> Has to be a sorted array
middle = (left + right) / 2 = (0 + 9) / 2 = 4 -> [11 (>6)] 

=> [3, 5, 6, 9]  
middle = (left + right) / 2 = (0 + 3) = 1 -> [5 (<6)]

=> [6, 9]
middle = (left + right) / 2 = (2 + 3) = 2 -> [6]

**Time Complexity**:    O(log n)
**Space Complexity**:   O(log n)     O(1)
                        Recursive  Iterative


### Binary Search: Recursive

```Java
   public int binarySearchRec(int[] array, int target) {
        return binarySearchRec(array, target,0, array.length-1);
    }

    private int binarySearchRec(
            int[] array, int target,
            int left, int right) {

        if (right < left)
            return -1;

        int middle = (left + right) / 2;
        if (array[middle] == target)
            return middle;

        if (target < array[middle])
            return binarySearchRec(array, target, left, middle - 1);
        return binarySearchRec(array, target, middle + 1, right);
    }
```

### Binary Search: Iterative

```Java
public int binarySearch(int[] array, int target) {
        var left = 0;
        var right = array.length - 1;

        while (left <= right) {
            var middle = (left + right) / 2;

            if (array[middle] == target)
                return middle;

            if (target < array[middle])
                right = middle - 1;
            else {
                left = middle + 1;
            }
        }

        return -1;
    }
```


## Ternary Search

### What is Tenary Search

[3, 5, 6, 9, 11, 18, 20, 21, 24, 30]
[0, 1, 2, 3,  4,  5,  6,  7,  8,  9] -> Divide into 3 parts
        (mid1)      (mid2)       

partitionSize = array.length / 3 
              = (right - left) / 3

         mid1 = left + partitionSize
         mid2 = rigth - partitionSize 

**Time Complexity**:    O(log n) -> based 3
**Space Complexity**:   O(log n)     O(1)
                        Recursive  Iterative

Comparisons:
-**BINARY** log(2)n
    - target == mid
    - target > mid
    - target < mid

-**TERNARY** log(3)n
    - target > mid2
    - target == mid2
    - target < mid2 && target > mid1
    - target == mid1
    - target < mid1

***Binary search is faster than ternary search***

### Implementation

```Java
    public int binarySearch(int[] array, int target) {
        var left = 0;
        var right = array.length - 1;

        while (left <= right) {
            var middle = (left + right) / 2;

            if (array[middle] == target)
                return middle;

            if (target < array[middle])
                right = middle - 1;
            else {
                left = middle + 1;
            }
        }

        return -1;
    }

    public int ternarySearch(int[] array, int target) {
        return ternarySearch(array, target, 0, array.length - 1);
    }

    private int ternarySearch(
            int[] array, int target,
            int left, int right
    ) {
        if (left > right)
            return -1;

        int partitionSize = (right - left) / 3;
        int mid1 = left + partitionSize;
        int mid2 = right - partitionSize;

        if (array[mid1] == target)
            return mid1;

        if (array[mid2] == target)
            return mid2;

        if (target < array[mid1])
            return ternarySearch(array, target, left, mid1 - 1);

        if (target > array[mid2])
            return ternarySearch(array, target, mid2 + 1, right);

        return ternarySearch(array, target, mid1 + 1, mid2 - 1);
    }
```

## Jump Search

### What is Jump Search

An improvement of Linear Search.

[3, 5, 6, 9, 11, 18, 20, 21, 24, 30]
[0, 1, 2, 3,  4,  5,  6,  7,  8,  9]

[3, 5, 6] [9, 11, 18] [20, 21, 24] [30]


blockSize = squre(n) = 3

e.g. target = 23

[3, 5, 6] -> 6 < 23 => Not this block
[9, 11, 18] -> 18 < 23 => Not this block
[21, 21, 24] => 24 > 23 => This block then do the linear search
=> Not in this block, so return -1

**Time Complexity**:    O(squre(n))
**Space Complexity**:   O(log n)     O(1)
                        Recursive  Iterative

Use two points for imeplementation

start -> [3, 5, 6][0].index
next -> [9, 11, 18][0].index
 
Two edges: 
    - start >= length
    - next > length

 
### Implementation
```Java
    public int jumpSearch(int[] array, int target) {
        int blockSize = (int) Math.sqrt(array.length);
        int start = 0;
        int next = blockSize;

        while (start < array.length &&
                array[next - 1] < target) {
            start = next;

            next += blockSize;
            if (next > array.length)
                next = array.length;
        }

        for (var i = start; i < next; i++)
            if (array[i] == target)
                return i;
        return -1;
    }
```

## Exponential Search

### What is Exponential Search

[3, 5, 6, 9, 11, 18, 20, 21, 24, 30]
[0, 1, 2, 3,  4,  5,  6,  7,  8,  9]

[3, 5]
-> bound(2)
[3, 5, 6]
-> bound(4)
[3, 5, 6, 9]
-> bound(8)
[3, 5, 6, 9, 11, 18, 20, 21, 24]
=> binary search range: [bound/2, bound]    

**Time Complexity**:    O(log i)
**Space Complexity**:   O(log n)     O(1)
                        Recursive  Iterative


### Implementation
```Java
    public int exponentialSearch(int[] array, int target) {
        int bound = 1;

        while (bound < array.length &&
                array[bound] < target)
            bound *= 2;

        int left = bound / 2;
        int right = Math.min(bound, array.length-1);

        return binarySearchRec(array, target, left, right);

```


# String Manipulation  

## Count Vowels
```Java
package com.company;

public class StringUtils {
    public static int countVowels(String str) {
        if (str == null)
            return 0;

        int count = 0;
        String vowels = "aeiou";
        // aeiou
        for (var ch : str.toLowerCase().toCharArray())
            // if (vowels.contains(Character.toString(ch)))
            if (vowels.indexOf(ch) != -1)
                count++;
        return count;
    }
}
```

## Reverse a String

### Common Solution - O(n.pow(2))
```Java
    public static String reverse(String str) {
        String reversed = "";
        for (var i = str.length(); i >= 0; i--) // O(n)
            reversed += str.charAt(i); // O(n)
        
        return reversed;
    }
```

### Use StringBuilder
```Java
    public static String reverse(String str) {
        if (str == null)
            return "";
        
        StringBuilder reversed = new StringBuilder();
        for (var i = str.length() - 1; i >= 0; i--) // O(n)
            reversed.append(str.charAt(i)); // O(1)

        return reversed.toString();
```

## Reverse Words

"Trees are beautiful" -> "beautiful are Trees"

```Java
    public static String reverseWords(String sentence) {
        if (sentence == null)
            return "";

        String[] words = sentence.trim().split(" ");

        Collections.reverse(Arrays.asList(words));
        return String.join(" ", words);

//        StringBuilder reversed = new StringBuilder();
//        for (var i = words.length - 1; i >= 0; i--)
//            reversed.append(words[i] + "");
//
//        return reversed.toString().trim();
    }
```


## Rotation

ABCD -> (1) DABC
     -> (2) CDAB
     -> (3) BCDA
     -> (4) ABCD


```Java
    public static boolean areRotations(
            String str1, String str2
    ) {
        if (str1 == null || str2 == null)
            return false;
        return (str1.length() == str2.length() &&
                (str1 + str1).contains(str2));
    }
```

**Challenge: What if the input string has millions characters?**


## Remove Duplicates
```Java
    public static String removeDuplicates(String str) {
        if (str == null)
            return "";

        StringBuilder output = new StringBuilder();
        Set<Character> seen = new HashSet<>();

        for (var ch : str.toCharArray()) {
            if (!seen.contains(ch)) {
                seen.add(ch);
                output.append(ch);
            }
        }

        return output.toString();
    }
```


## Most Repeated Char
```Java
    public static char getMaxOccurringChar(String str) {
        if (str == null || str.isEmpty())
            throw new IllegalStateException();

//        Map<Character, Integer> frequencies = new HashMap<>();
//        for (var ch : str.toCharArray()) {
//            if (frequencies.containsKey(ch))
//                frequencies.replace(ch, frequencies.get(ch) + 1);
//            else
//                frequencies.put(ch, 1);
//        }

        // ASCII table
        final int ASCII_SIZE = 256;
        int[] frequencies = new int[ASCII_SIZE];
        for (var ch : str.toCharArray())
            frequencies[ch]++;

        int max = 0;
        char result = ' ';
        for (var i = 0; i < frequencies.length; i++)
            if (frequencies[i] > max) {
                max = frequencies[i];
                result = (char) i;
            }

        return result;
    }
```


## Sentence Capitalization
```Java
    public static String capitalize(String sentence) {
        if (sentence == null || sentence.trim().isEmpty())
            return "";

        String[] words = sentence.trim().replaceAll(" +", " ").split(" ");
        for (var i = 0; i < words.length; i++) {
            words[i] = words[i].substring(0, 1).toUpperCase() +
                    words[i].substring(1).toLowerCase();
        }

        return String.join(" ", words);
    }
```

## Anagrams

### Anagrams: Using Sorting 

ABCD -> CBDA
['A', 'B', 'C', 'D'] -> ['A', 'B', 'C', 'D']
['C', 'B', 'D', 'A'] -> ['A', 'B', 'C', 'D']

```Java
    public static boolean areAnagrams(
            String first, String second
    ) {
        if (first == null || second == null ||
                first.length() != second.length())
            return false;

        // O(n)
        var array1 = first.toLowerCase().toCharArray();

        // O(n log n)
        Arrays.sort(array1);

        var array2 = second.toLowerCase().toCharArray();
        Arrays.sort(array2);

        return Arrays.equals(array1, array2);
    }
```

-> O(n logn)


### Anagrams: Using Histogramming 

-> O(n) better than the first solution

```Java
    public static boolean areAnagrams(
            String first, String second
    ) {
        if (first == null || second == null ||
                first.length() != second.length())
            return false;

        var array1 = first.toLowerCase().toCharArray();
        Arrays.sort(array1);

        var array2 = second.toLowerCase().toCharArray();
        Arrays.sort(array2);

        return Arrays.equals(array1, array2);
    }
```


## Palindrome Strings

ABBA - MADAM

### Simplest Solution

```Java
    public static boolean isPalindrome(String word) {
        var input = new StringBuilder(word);
        input.reverse();
        return input.toString().equals(word);
    }
```

### Faster Solution

```Java
    public static boolean isPalindrome(String word) {
        if (word == null)
            return false; 

        int left = 0;
        int right = word.length() - 1;

        while (left < right)
            if (word.charAt(left++) != word.charAt(right--))
                return false;
        return true;
    }
```

# Additional Resrouces

leetcode.com
interviewcake.com






















