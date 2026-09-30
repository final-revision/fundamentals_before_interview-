# Bruviti AI Placement Coding Preparation (Java)

## DSA + Coding Interview Questions + Answers

This document focuses on coding topics likely useful for Bruviti AI
campus assessment: - Problem solving - Data structures - Algorithms -
Java implementation - Coding interview discussion questions

------------------------------------------------------------------------

# 1. Reverse a String

## Question

Write a Java program to reverse a given string.

## Approach

Use StringBuilder because it provides an efficient reverse method.

## Java Code

``` java
public class Main {
    public static void main(String[] args) {
        String str = "Bruviti";

        String reversed = new StringBuilder(str)
                .reverse()
                .toString();

        System.out.println(reversed);
    }
}
```

Time Complexity: O(n)

Space Complexity: O(n)

------------------------------------------------------------------------

# 2. Check Palindrome String

## Question

Check whether a string is palindrome.

Example: madam -\> true

## Java Code

``` java
public class Main {

    static boolean isPalindrome(String str) {

        int left = 0;
        int right = str.length() - 1;

        while(left < right) {

            if(str.charAt(left) != str.charAt(right))
                return false;

            left++;
            right--;
        }

        return true;
    }

    public static void main(String[] args) {

        System.out.println(isPalindrome("madam"));
    }
}
```

Time Complexity: O(n)

------------------------------------------------------------------------

# 3. Find Duplicate Elements in Array

## Question

Find duplicate numbers in an array.

## Java Code

``` java
import java.util.*;

public class Main {

    public static void main(String[] args) {

        int arr[] = {1,2,3,2,4,1};

        HashSet<Integer> set = new HashSet<>();

        for(int num : arr){

            if(!set.add(num)){
                System.out.println("Duplicate: " + num);
            }
        }
    }
}
```

Concepts tested: - HashSet - Searching - Time optimization

------------------------------------------------------------------------

# 4. Two Sum Problem

## Question

Find two numbers whose sum equals target.

Example:

Array: \[2,7,11,15\]

Target: 9

Answer: \[2,7\]

## Java Code

``` java
import java.util.*;

class Main {

    public static int[] twoSum(int arr[], int target){

        HashMap<Integer,Integer> map = new HashMap<>();

        for(int i=0;i<arr.length;i++){

            int difference = target - arr[i];

            if(map.containsKey(difference)){
                return new int[]{
                    map.get(difference),
                    i
                };
            }

            map.put(arr[i],i);
        }

        return new int[]{};
    }
}
```

Time Complexity: O(n)

------------------------------------------------------------------------

# 5. Find Maximum Element in Array

## Java Code

``` java
public class Main {

    public static void main(String args[]){

        int arr[] = {10,5,30,20};

        int max = arr[0];

        for(int i=1;i<arr.length;i++){

            if(arr[i] > max)
                max = arr[i];
        }

        System.out.println(max);
    }
}
```

------------------------------------------------------------------------

# 6. Binary Search

## Question

Search an element in sorted array.

## Java Code

``` java
public class Main {

static int binarySearch(int arr[], int target){

    int low = 0;
    int high = arr.length-1;

    while(low <= high){

        int mid = (low+high)/2;

        if(arr[mid] == target)
            return mid;

        else if(arr[mid] < target)
            low = mid+1;

        else
            high = mid-1;
    }

    return -1;
}

}
```

Time Complexity: O(log n)

------------------------------------------------------------------------

# 7. Reverse Linked List

## Question

Reverse a linked list.

## Java Code

``` java
class Node {

    int data;
    Node next;

    Node(int data){
        this.data=data;
        next=null;
    }
}


class Main {

    Node reverse(Node head){

        Node previous=null;
        Node current=head;

        while(current!=null){

            Node next=current.next;

            current.next=previous;

            previous=current;
            current=next;
        }

        return previous;
    }
}
```

Concept: - Pointer manipulation - Linked list traversal

------------------------------------------------------------------------

# 8. Valid Parentheses

## Question

Check if brackets are balanced.

Example:

(){}\[\] -\> true

## Java Code

``` java
import java.util.*;

class Main {

public static boolean isValid(String s){

    Stack<Character> stack=new Stack<>();

    for(char c:s.toCharArray()){

        if(c=='(' || c=='{' || c=='['){

            stack.push(c);

        }else{

            if(stack.isEmpty())
                return false;

            char top=stack.pop();

            if(c==')' && top!='(')
                return false;

            if(c=='}' && top!='{')
                return false;

            if(c==']' && top!='[')
                return false;
        }
    }

    return stack.isEmpty();
}

}
```

------------------------------------------------------------------------

# 9. Merge Two Sorted Arrays

## Concept

Two pointer technique.

## Java Code

``` java
import java.util.*;

class Main {

static int[] merge(int a[], int b[]){

    int result[]=new int[a.length+b.length];

    int i=0,j=0,k=0;


    while(i<a.length && j<b.length){

        if(a[i]<b[j])
            result[k++]=a[i++];

        else
            result[k++]=b[j++];
    }


    while(i<a.length)
        result[k++]=a[i++];

    while(j<b.length)
        result[k++]=b[j++];


    return result;
}

}
```

------------------------------------------------------------------------

# 10. Fibonacci Series

## Java Code

``` java
class Main {

public static void main(String args[]){

int a=0;
int b=1;

for(int i=0;i<10;i++){

System.out.print(a+" ");

int next=a+b;

a=b;
b=next;

}

}

}
```

------------------------------------------------------------------------

# Coding Interview Questions They Can Ask

## Q1. Why choose HashMap instead of Array?

Answer:

HashMap provides average O(1) lookup time while searching values using
keys.

------------------------------------------------------------------------

## Q2. Difference between ArrayList and LinkedList?

Answer:

ArrayList: - Faster random access - Uses dynamic array

LinkedList: - Faster insertion/deletion in middle - Uses nodes

------------------------------------------------------------------------

## Q3. Difference between Stack and Queue?

Answer:

Stack: LIFO (Last In First Out)

Queue: FIFO (First In First Out)

------------------------------------------------------------------------

## Q4. Explain time complexity.

Answer:

Time complexity describes how execution time grows with input size.

Examples:

O(1): Constant

O(n): Linear

O(log n): Binary search

O(n²): Nested loops

------------------------------------------------------------------------

## Q5. How do you optimize slow code?

Answer:

Steps:

1.  Analyze complexity
2.  Choose better data structure
3.  Remove unnecessary loops
4.  Use caching
5.  Reduce memory usage

------------------------------------------------------------------------

# DSA Topics To Prepare

Priority:

1.  Arrays
2.  Strings
3.  HashMap
4.  Sorting
5.  Searching
6.  Linked List
7.  Stack
8.  Queue
9.  Trees
10. Recursion
11. Dynamic Programming basics

------------------------------------------------------------------------

# Bruviti Coding Test Strategy

Expected:

-   Easy to medium DSA problems
-   Focus on logic
-   Explain approach before coding
-   Write clean Java
-   Discuss complexity

Important: They may test how you think and optimize solutions, not only
whether code works.
