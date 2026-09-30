# Bruviti AI — Coding & Programming Interview Preparation

## Purpose

This document is for the **coding/programming portion of the Bruviti AI placement process**.

Focus areas:

- Python programming
- DSA fundamentals
- Arrays and strings
- Hashing
- Searching and sorting
- Stack and queue
- Linked lists
- Recursion
- Greedy basics
- Trees basics
- Time and space complexity
- SQL/programming logic awareness
- Coding interview questions
- Python-specific interview questions

All coding solutions are provided in **Python**.

---

# 1. What to Prepare First

For a technical assessment/interview, prioritize:

1. Arrays
2. Strings
3. HashMap / Dictionary
4. Two pointers
5. Sliding window
6. Stack
7. Binary search
8. Sorting
9. Linked list
10. Recursion
11. Basic trees
12. Time complexity
13. Python fundamentals
14. OOP basics
15. SQL basics

For an AI/edge-oriented company, also understand how programming connects to:

- Data processing
- Sensor data
- ML preprocessing
- APIs
- Real-time systems
- File/data handling

---

# 2. Python Fundamentals

## Q1. Reverse a string

### Question

Write a Python program to reverse a string.

### Answer

```python
s = input("Enter string: ")

reverse = s[::-1]

print(reverse)
```

### Interview concept

Python slicing with `[::-1]` creates a reversed sequence.

Time: `O(n)`

Space: `O(n)`

---

# 3. Check Palindrome

## Q2. Check whether a string is a palindrome

### Answer

```python
s = input("Enter string: ")

if s == s[::-1]:
    print("Palindrome")
else:
    print("Not Palindrome")
```

### Example

`madam` → Palindrome

`hello` → Not Palindrome

---

# 4. Palindrome Without Slicing

## Q3. Check palindrome using two pointers

```python
s = input("Enter string: ")

left = 0
right = len(s) - 1

is_palindrome = True

while left < right:
    if s[left] != s[right]:
        is_palindrome = False
        break

    left += 1
    right -= 1

if is_palindrome:
    print("Palindrome")
else:
    print("Not Palindrome")
```

Time: `O(n)`

Space: `O(1)`

### Interview point

This demonstrates the **two-pointer technique**.

---

# 5. Reverse a Number

## Q4. Reverse an integer

```python
n = int(input("Enter number: "))

reverse = 0

while n > 0:
    digit = n % 10
    reverse = reverse * 10 + digit
    n //= 10

print(reverse)
```

Example:

`12345 → 54321`

---

# 6. Check Prime Number

## Q5. Check whether a number is prime

```python
n = int(input("Enter number: "))

if n < 2:
    print("Not Prime")
else:
    is_prime = True

    for i in range(2, int(n ** 0.5) + 1):
        if n % i == 0:
            is_prime = False
            break

    if is_prime:
        print("Prime")
    else:
        print("Not Prime")
```

### Why check only up to √n?

If `n` has a factor greater than √n, it must have another factor smaller than √n.

Time: `O(√n)`

---

# 7. Factorial

## Q6. Find factorial of a number

```python
n = int(input("Enter number: "))

factorial = 1

for i in range(1, n + 1):
    factorial *= i

print(factorial)
```

---

# 8. Fibonacci Series

## Q7. Print Fibonacci series

```python
n = int(input("Enter number of terms: "))

a = 0
b = 1

for _ in range(n):
    print(a, end=" ")
    a, b = b, a + b
```

Example:

`0 1 1 2 3 5 8 13`

Time: `O(n)`

---

# 9. Armstrong Number

## Q8. Check Armstrong number

```python
n = int(input("Enter number: "))

original = n
digits = len(str(n))

total = 0

while n > 0:
    digit = n % 10
    total += digit ** digits
    n //= 10

if total == original:
    print("Armstrong")
else:
    print("Not Armstrong")
```

Example:

`153 = 1³ + 5³ + 3³ = 153`

---

# 10. Sum of Digits

## Q9. Find sum of digits

```python
n = int(input("Enter number: "))

total = 0

while n > 0:
    total += n % 10
    n //= 10

print(total)
```

---

# 11. Count Digits

## Q10. Count number of digits

```python
n = int(input("Enter number: "))

count = 0

if n == 0:
    count = 1
else:
    while n > 0:
        count += 1
        n //= 10

print(count)
```

---

# 12. Find Maximum Element

## Q11. Find maximum element in an array

```python
arr = [10, 25, 5, 40, 15]

maximum = arr[0]

for x in arr:
    if x > maximum:
        maximum = x

print(maximum)
```

Time: `O(n)`

---

# 13. Find Minimum Element

```python
arr = [10, 25, 5, 40, 15]

minimum = arr[0]

for x in arr:
    if x < minimum:
        minimum = x

print(minimum)
```

---

# 14. Find Second Largest Element

## Q12. Find second largest without sorting

```python
arr = [10, 25, 5, 40, 15]

largest = float("-inf")
second = float("-inf")

for x in arr:
    if x > largest:
        second = largest
        largest = x
    elif largest > x > second:
        second = x

print(second)
```

Time: `O(n)`

Space: `O(1)`

### Interview follow-up

**Why not sort?**

Sorting takes `O(n log n)`, while the one-pass solution takes `O(n)`.

---

# 15. Remove Duplicates

## Q13. Remove duplicates from an array

```python
arr = [1, 2, 2, 3, 4, 4, 5]

result = list(set(arr))

print(result)
```

### Important

`set` does not guarantee the original order in the general conceptual sense.

If order must be preserved:

```python
arr = [1, 2, 2, 3, 4, 4, 5]

result = []

seen = set()

for x in arr:
    if x not in seen:
        result.append(x)
        seen.add(x)

print(result)
```

---

# 16. Frequency of Elements

## Q14. Count frequency of each element

```python
arr = [1, 2, 2, 3, 3, 3, 4]

frequency = {}

for x in arr:
    frequency[x] = frequency.get(x, 0) + 1

print(frequency)
```

Output:

```text
{1: 1, 2: 2, 3: 3, 4: 1}
```

### Important concept

Python dictionary/hash map gives average `O(1)` lookup and insertion.

---

# 17. Character Frequency

## Q15. Count characters in a string

```python
s = "programming"

frequency = {}

for ch in s:
    frequency[ch] = frequency.get(ch, 0) + 1

print(frequency)
```

---

# 18. First Non-Repeating Character

## Q16. Find the first non-repeating character

```python
s = "swiss"

frequency = {}

for ch in s:
    frequency[ch] = frequency.get(ch, 0) + 1

for ch in s:
    if frequency[ch] == 1:
        print(ch)
        break
```

Output:

`w`

Time: `O(n)`

---

# 19. Anagram

## Q17. Check whether two strings are anagrams

```python
s1 = "listen"
s2 = "silent"

if sorted(s1) == sorted(s2):
    print("Anagram")
else:
    print("Not Anagram")
```

### Better interview solution

```python
from collections import Counter

s1 = "listen"
s2 = "silent"

if Counter(s1) == Counter(s2):
    print("Anagram")
else:
    print("Not Anagram")
```

Time: approximately `O(n)` using frequency counting.

---

# 20. Two Sum

## Q18. Find two numbers whose sum equals target

### Example

```text
arr = [2, 7, 11, 15]
target = 9
```

### Answer

```python
arr = [2, 7, 11, 15]
target = 9

seen = {}

for i, x in enumerate(arr):
    complement = target - x

    if complement in seen:
        print(seen[complement], i)
        break

    seen[x] = i
```

### Key concept

This is a classic **hashing** problem.

Time: `O(n)`

Space: `O(n)`

---

# 21. Move Zeroes

## Q19. Move all zeroes to the end

```python
arr = [0, 1, 0, 3, 12]

position = 0

for x in arr:
    if x != 0:
        arr[position] = x
        position += 1

while position < len(arr):
    arr[position] = 0
    position += 1

print(arr)
```

Output:

`[1, 3, 12, 0, 0]`

---

# 22. Find Missing Number

## Q20. Find missing number from 0 to n

```python
arr = [3, 0, 1]

n = len(arr)

expected = n * (n + 1) // 2

actual = sum(arr)

print(expected - actual)
```

Output:

`2`

Time: `O(n)`

Space: `O(1)`

---

# 23. Maximum Subarray Sum

## Q21. Find maximum subarray sum

This is the famous **Kadane's Algorithm** problem.

```python
arr = [-2, 1, -3, 4, -1, 2, 1, -5, 4]

current = arr[0]
maximum = arr[0]

for i in range(1, len(arr)):
    current = max(arr[i], current + arr[i])
    maximum = max(maximum, current)

print(maximum)
```

Output:

`6`

Subarray:

`[4, -1, 2, 1]`

Time: `O(n)`

---

# 24. Binary Search

## Q22. Implement binary search

```python
arr = [1, 3, 5, 7, 9, 11]

target = 7

left = 0
right = len(arr) - 1

while left <= right:
    mid = (left + right) // 2

    if arr[mid] == target:
        print("Found at index", mid)
        break

    elif arr[mid] < target:
        left = mid + 1

    else:
        right = mid - 1
else:
    print("Not Found")
```

### Important

Binary search requires a **sorted** search space.

Time: `O(log n)`

Space: `O(1)`

---

# 25. Linear Search vs Binary Search

| Linear Search | Binary Search |
|---|---|
| Checks elements sequentially | Divides search space |
| O(n) | O(log n) |
| Works on unsorted data | Requires sorted data |
| Simple | More efficient for large sorted data |

---

# 26. Bubble Sort

## Q23. Implement Bubble Sort

```python
arr = [5, 3, 8, 4, 2]

n = len(arr)

for i in range(n):
    swapped = False

    for j in range(0, n - i - 1):
        if arr[j] > arr[j + 1]:
            arr[j], arr[j + 1] = arr[j + 1], arr[j]
            swapped = True

    if not swapped:
        break

print(arr)
```

Average/worst time: `O(n²)`

---

# 27. Selection Sort

## Q24. Implement Selection Sort

```python
arr = [64, 25, 12, 22, 11]

n = len(arr)

for i in range(n):
    minimum = i

    for j in range(i + 1, n):
        if arr[j] < arr[minimum]:
            minimum = j

    arr[i], arr[minimum] = arr[minimum], arr[i]

print(arr)
```

Time: `O(n²)`

---

# 28. Merge Sort

## Q25. Implement Merge Sort

```python
def merge_sort(arr):
    if len(arr) <= 1:
        return arr

    mid = len(arr) // 2

    left = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])

    result = []

    i = 0
    j = 0

    while i < len(left) and j < len(right):

        if left[i] <= right[j]:
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1

    result.extend(left[i:])
    result.extend(right[j:])

    return result


arr = [5, 2, 8, 1, 3]

print(merge_sort(arr))
```

Time: `O(n log n)`

Space: `O(n)`

---

# 29. Stack

## Q26. Implement stack using Python list

```python
stack = []

stack.append(10)
stack.append(20)
stack.append(30)

print(stack.pop())

print(stack)
```

Stack follows:

**LIFO — Last In, First Out**

---

# 30. Queue

## Q27. Implement queue

```python
from collections import deque

queue = deque()

queue.append(10)
queue.append(20)
queue.append(30)

print(queue.popleft())

print(queue)
```

Queue follows:

**FIFO — First In, First Out**

---

# 31. Valid Parentheses

## Q28. Check balanced parentheses

```python
def is_valid(s):
    stack = []

    pairs = {
        ')': '(',
        ']': '[',
        '}': '{'
    }

    for ch in s:

        if ch in "([{":
            stack.append(ch)

        else:
            if not stack or stack[-1] != pairs[ch]:
                return False

            stack.pop()

    return len(stack) == 0


print(is_valid("({[]})"))
print(is_valid("([)]"))
```

Output:

```text
True
False
```

### Key concept

Stack is ideal because the most recently opened bracket must be closed first.

---

# 32. Reverse Words

## Q29. Reverse the order of words

```python
s = "I love Python"

words = s.split()

words.reverse()

print(" ".join(words))
```

Output:

`Python love I`

---

# 33. Longest Word

## Q30. Find the longest word in a sentence

```python
s = "Python is powerful"

words = s.split()

longest = max(words, key=len)

print(longest)
```

Output:

`powerful`

---

# 34. Count Vowels

## Q31. Count vowels in a string

```python
s = input("Enter string: ")

vowels = "aeiouAEIOU"

count = 0

for ch in s:
    if ch in vowels:
        count += 1

print(count)
```

---

# 35. Remove Spaces

## Q32. Remove spaces from a string

```python
s = "hello world python"

result = s.replace(" ", "")

print(result)
```

---

# 36. Duplicate Characters

## Q33. Find duplicate characters

```python
s = "programming"

frequency = {}

for ch in s:
    frequency[ch] = frequency.get(ch, 0) + 1

for ch in frequency:
    if frequency[ch] > 1:
        print(ch)
```

---

# 37. Intersection of Arrays

## Q34. Find common elements

```python
a = [1, 2, 3, 4]
b = [3, 4, 5, 6]

result = list(set(a) & set(b))

print(result)
```

---

# 38. Two Pointer — Pair Sum in Sorted Array

## Q35. Find pair with target sum in a sorted array

```python
arr = [1, 2, 3, 4, 6, 8]
target = 10

left = 0
right = len(arr) - 1

while left < right:

    total = arr[left] + arr[right]

    if total == target:
        print(arr[left], arr[right])
        break

    elif total < target:
        left += 1

    else:
        right -= 1
```

Time: `O(n)`

---

# 39. Sliding Window

## Q36. Maximum sum of subarray of size K

```python
arr = [2, 1, 5, 1, 3, 2]
k = 3

window_sum = sum(arr[:k])
maximum = window_sum

for i in range(k, len(arr)):
    window_sum += arr[i]
    window_sum -= arr[i - k]

    maximum = max(maximum, window_sum)

print(maximum)
```

Output:

`9`

### Key concept

Instead of recalculating every window, remove the element leaving the window and add the new element.

Time: `O(n)`

---

# 40. Longest Substring Without Repeating Characters

## Q37. Find length of longest substring without repeating characters

```python
s = "abcabcbb"

left = 0
seen = set()
maximum = 0

for right in range(len(s)):

    while s[right] in seen:
        seen.remove(s[left])
        left += 1

    seen.add(s[right])

    maximum = max(maximum, right - left + 1)

print(maximum)
```

Output:

`3`

---

# 41. Recursion

## Q38. Factorial using recursion

```python
def factorial(n):
    if n == 0 or n == 1:
        return 1

    return n * factorial(n - 1)


print(factorial(5))
```

### Important concept

Every recursive function needs a **base case**.

---

# 42. Fibonacci Using Recursion

```python
def fibonacci(n):
    if n <= 1:
        return n

    return fibonacci(n - 1) + fibonacci(n - 2)


for i in range(7):
    print(fibonacci(i), end=" ")
```

### Interview follow-up

Why is this inefficient?

Because it repeatedly calculates the same subproblems.

The naive recursive version has exponential time complexity.

---

# 43. Linked List

## Q39. Basic linked list node

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None


first = Node(10)
second = Node(20)
third = Node(30)

first.next = second
second.next = third

current = first

while current:
    print(current.data)
    current = current.next
```

Output:

```text
10
20
30
```

---

# 44. Reverse a Linked List

## Q40. Reverse a singly linked list

```python
def reverse(head):
    previous = None
    current = head

    while current:
        next_node = current.next

        current.next = previous

        previous = current
        current = next_node

    return previous
```

### Key idea

Maintain:

- previous
- current
- next

Time: `O(n)`

Space: `O(1)`

---

# 45. Detect Cycle in Linked List

## Q41. Detect a cycle

Use Floyd's cycle detection algorithm.

```python
def has_cycle(head):
    slow = head
    fast = head

    while fast and fast.next:

        slow = slow.next
        fast = fast.next.next

        if slow == fast:
            return True

    return False
```

### Key concept

- Slow pointer moves 1 step.
- Fast pointer moves 2 steps.

If they meet, a cycle exists.

---

# 46. Binary Tree Traversal

## Q42. Inorder traversal

```python
def inorder(root):

    if root is None:
        return

    inorder(root.left)

    print(root.data, end=" ")

    inorder(root.right)
```

Inorder traversal of a Binary Search Tree gives values in sorted order.

---

# 47. BFS

## Q43. Breadth First Search

```python
from collections import deque

def bfs(graph, start):

    queue = deque([start])
    visited = set([start])

    while queue:

        node = queue.popleft()

        print(node, end=" ")

        for neighbour in graph[node]:

            if neighbour not in visited:
                visited.add(neighbour)
                queue.append(neighbour)
```

### Concept

BFS generally uses a **queue**.

---

# 48. DFS

## Q44. Depth First Search

```python
def dfs(graph, node, visited):

    if node in visited:
        return

    visited.add(node)

    print(node, end=" ")

    for neighbour in graph[node]:
        dfs(graph, neighbour, visited)
```

### Concept

DFS can be implemented using:

- Recursion
- Stack

---

# 49. Python Interview Questions

## Q45. What is the difference between list and tuple?

**Answer:**

### List
- Mutable
- Uses `[]`
- Can be modified

### Tuple
- Immutable
- Uses `()`
- Cannot be modified after creation

---

## Q46. List vs Set

**Answer:**

### List
- Ordered collection
- Allows duplicates
- Indexing supported

### Set
- Stores unique elements
- Fast average membership testing
- No normal index-based access

---

## Q47. Dictionary vs Set

**Answer:**

Dictionary stores:

`key → value`

Set stores:

`unique values`

---

## Q48. What is mutable and immutable?

**Mutable objects can be changed after creation.**

Examples:

- list
- dictionary
- set

**Immutable objects cannot be changed after creation.**

Examples:

- int
- float
- string
- tuple

---

## Q49. What is a lambda function?

**Answer:**

A lambda is a small anonymous function.

```python
square = lambda x: x * x

print(square(5))
```

Output:

`25`

---

## Q50. What is list comprehension?

**Answer:**

A compact way of creating lists.

```python
squares = [x * x for x in range(5)]

print(squares)
```

Output:

`[0, 1, 4, 9, 16]`

---

# 50. Python OOP Questions

## Q51. What is a class?

**Answer:**
A class is a blueprint for creating objects.

```python
class Student:
    def __init__(self, name):
        self.name = name


s = Student("Rahul")

print(s.name)
```

---

## Q52. What is an object?

**Answer:**
An object is an instance of a class.

---

## Q53. What is inheritance?

**Answer:**
Inheritance allows one class to acquire properties and methods from another class.

```python
class Animal:
    def speak(self):
        print("Animal sound")


class Dog(Animal):
    pass


d = Dog()
d.speak()
```

---

## Q54. What is polymorphism?

**Answer:**
Polymorphism allows the same interface/method name to behave differently for different objects.

---

## Q55. What is encapsulation?

**Answer:**
Encapsulation means bundling data and methods together and controlling access to internal implementation details.

---

# 51. Time Complexity Questions

## Q56. What is Big-O notation?

**Answer:**
Big-O notation describes how the time or space requirements of an algorithm grow as the input size increases.

---

## Q57. Common complexities

| Complexity | Example |
|---|---|
| O(1) | Array access by index |
| O(log n) | Binary search |
| O(n) | Linear traversal |
| O(n log n) | Merge sort |
| O(n²) | Nested loops / bubble sort |
| O(2ⁿ) | Some brute-force recursive problems |

---

# 52. Important Coding Interview Follow-Ups

After solving a coding problem, the interviewer may ask:

### Q: What is the time complexity?

Always be ready to explain the loops and data structures.

### Q: What is the space complexity?

Mention extra memory used by the algorithm.

### Q: Can you optimize it?

Try to reduce:

- Nested loops
- Repeated computation
- Unnecessary memory
- Expensive operations

### Q: Can you solve it without sorting?

This often tests whether you know hashing or linear-time approaches.

### Q: Can you do it in O(n)?

This is a common optimization discussion.

### Q: What edge cases exist?

Examples:

- Empty input
- One element
- Duplicate values
- Negative values
- Already sorted data
- Very large input
- All elements identical

---

# 53. Coding Interview Questions They May Ask You Verbally

## Python

1. Why did you choose Python?
2. What are Python's main data structures?
3. List vs tuple?
4. List vs set?
5. Dictionary vs set?
6. Mutable vs immutable?
7. What is slicing?
8. What is list comprehension?
9. What is a lambda function?
10. What is `enumerate()`?
11. What is `zip()`?
12. What is `range()`?
13. What is exception handling?
14. What is `try-except`?
15. What is a generator?
16. What is an iterator?
17. What is the difference between `is` and `==`?
18. What is shallow copy vs deep copy?
19. What is a virtual environment?
20. What are modules and packages?

---

# 54. DSA Interview Questions

1. What is an array?
2. Array vs linked list?
3. Stack vs queue?
4. What is a hash table?
5. Why is hashing useful?
6. What is collision in hashing?
7. What is binary search?
8. What condition is required for binary search?
9. What is recursion?
10. Why do we need a base case?
11. What is dynamic programming?
12. What is memoization?
13. What is greedy algorithm?
14. What is backtracking?
15. What is BFS?
16. What is DFS?
17. BFS vs DFS?
18. What is a binary tree?
19. What is a binary search tree?
20. What is a heap?
21. What is a graph?
22. What is a cycle?
23. What is time complexity?
24. What is space complexity?
25. What is Big-O notation?

---

# 55. High-Probability Coding Problems to Practice

Before the assessment, make sure you can solve these without looking at the solution:

### Easy

1. Reverse string
2. Palindrome
3. Reverse number
4. Prime number
5. Factorial
6. Fibonacci
7. Armstrong number
8. Sum of digits
9. Maximum/minimum
10. Second largest
11. Count vowels
12. Character frequency
13. Remove duplicates
14. Anagram
15. First non-repeating character

### Medium

16. Two Sum
17. Move Zeroes
18. Missing Number
19. Maximum Subarray
20. Binary Search
21. Valid Parentheses
22. Pair Sum
23. Longest Substring Without Repeating Characters
24. Sliding Window Maximum Sum
25. Merge Intervals
26. Merge Two Sorted Arrays
27. Reverse Linked List
28. Detect Linked List Cycle
29. BFS
30. DFS

---

# 56. Bruviti-Style Scenario Coding Questions

Because Bruviti's technology area involves connected systems, edge technology, data, and AI/ML, you should also be comfortable with simple programming scenarios involving data processing.

## Q58. A device sends temperature readings. Find the average temperature.

```python
temperatures = [30.5, 31.2, 29.8, 32.1, 30.4]

average = sum(temperatures) / len(temperatures)

print(average)
```

---

## Q59. Detect abnormal temperature readings

Assume temperature above 40 is abnormal.

```python
temperatures = [32, 35, 41, 37, 45, 30]

for temp in temperatures:
    if temp > 40:
        print("Abnormal:", temp)
```

---

## Q60. Count abnormal sensor readings

```python
temperatures = [32, 41, 35, 45, 30, 42]

count = 0

for temp in temperatures:
    if temp > 40:
        count += 1

print("Abnormal readings:", count)
```

---

## Q61. Find maximum sensor reading

```python
readings = [32, 35, 41, 37, 45, 30]

maximum = max(readings)

print(maximum)
```

---

## Q62. Remove duplicate sensor readings

```python
readings = [30, 30, 31, 32, 31, 33]

unique_readings = list(dict.fromkeys(readings))

print(unique_readings)
```

This preserves insertion order.

---

## Q63. Find the most frequent sensor value

```python
from collections import Counter

readings = [30, 31, 30, 32, 30, 31, 33]

frequency = Counter(readings)

print(frequency.most_common(1))
```

---

# 57. Coding + ML Connection Questions

## Q64. Why is Python widely used in AI/ML?

**Answer:**

Python is widely used because it has:

- Simple syntax
- Large ecosystem
- NumPy
- Pandas
- Scikit-learn
- TensorFlow
- PyTorch
- OpenCV
- Strong community support

---

## Q65. What is NumPy?

**Answer:**
NumPy is a Python library for numerical computing and efficient array operations.

---

## Q66. What is Pandas?

**Answer:**
Pandas is a Python library used for data manipulation and analysis.

Common structures:

- Series
- DataFrame

---

## Q67. What is Scikit-learn?

**Answer:**
Scikit-learn is a Python machine learning library containing implementations of many classical ML algorithms and preprocessing/evaluation utilities.

---

## Q68. What is PyTorch?

**Answer:**
PyTorch is a deep learning framework used to build and train neural networks.

---

## Q69. What is OpenCV?

**Answer:**
OpenCV is a computer vision library used for image and video processing.

---

# 58. Interview Questions About Your Coding Approach

## Q70. What do you do before writing code?

**Good answer:**

1. Understand the problem.
2. Identify inputs and outputs.
3. Consider constraints.
4. Think of a brute-force solution.
5. Look for optimization.
6. Choose an appropriate data structure.
7. Analyze time and space complexity.
8. Test edge cases.
9. Then implement.

---

## Q71. What if your first solution is O(n²)?

**Answer:**

First verify correctness.

Then ask whether the problem allows:

- Hashing
- Two pointers
- Sliding window
- Binary search
- Sorting
- Prefix sums
- Greedy techniques

to reduce complexity.

---

# 59. Important Coding Patterns

Learn these patterns rather than memorizing individual programs.

## Pattern 1 — Hashing

Useful for:

- Two Sum
- Frequency counting
- Duplicate detection
- First non-repeating element

---

## Pattern 2 — Two Pointers

Useful for:

- Pair sum
- Palindrome
- Sorted array problems
- Removing duplicates
- Partitioning

---

## Pattern 3 — Sliding Window

Useful for:

- Subarray problems
- Substring problems
- Fixed-size windows
- Longest/shortest window problems

---

## Pattern 4 — Binary Search

Useful when:

- Search space is sorted
- Search space can be divided into halves
- Answer has a monotonic property

---

## Pattern 5 — Stack

Useful for:

- Parentheses
- Undo-like operations
- Expression processing
- Next greater element
- Monotonic stack problems

---

## Pattern 6 — BFS/DFS

Useful for:

- Trees
- Graphs
- Connected components
- Grid problems
- Shortest path in unweighted graphs

---

# 60. Final Bruviti Coding Revision Plan

## If you have only 1 day

### First 2 hours
Practice:

- Arrays
- Strings
- Hashing
- Two Sum
- Frequency counting
- Palindrome
- Anagram

### Next 1.5 hours

Practice:

- Binary search
- Sorting
- Stack
- Queue
- Valid parentheses

### Next 1.5 hours

Practice:

- Linked list
- Reverse linked list
- Cycle detection
- BFS
- DFS

### Final 1 hour

Revise:

- Big-O
- Python basics
- OOP
- ML/Python libraries
- Edge/sensor data scenarios

---

# 61. Most Important 20 Coding Problems

If time is extremely limited, practice these first:

1. Reverse String
2. Palindrome
3. Prime Number
4. Fibonacci
5. Second Largest Element
6. Remove Duplicates
7. Character Frequency
8. First Non-Repeating Character
9. Anagram
10. Two Sum
11. Missing Number
12. Move Zeroes
13. Maximum Subarray
14. Binary Search
15. Valid Parentheses
16. Sliding Window Maximum Sum
17. Longest Substring Without Repeating Characters
18. Reverse Linked List
19. Detect Linked List Cycle
20. BFS/DFS

---

# 62. How to Answer During a Coding Interview

When given a coding problem, use this structure:

### Step 1 — Clarify
Restate the problem in your own words.

### Step 2 — Explain approach
For example:

> "I will use a dictionary to store previously seen values so that I can find the required complement in O(1) average time."

### Step 3 — Mention complexity

> "The time complexity is O(n) and the extra space is O(n)."

### Step 4 — Code

Write clean code.

### Step 5 — Test

Test:

- Normal case
- Empty case
- One-element case
- Duplicate case
- Boundary case

### Step 6 — Optimize

If the interviewer asks for a better solution, explain the trade-off.

---

# 63. Final Technical Interview Checklist

Before Bruviti's technical assessment/interview, make sure you can:

- [ ] Write basic Python without help
- [ ] Explain list/tuple/set/dictionary
- [ ] Use dictionary for frequency counting
- [ ] Solve Two Sum
- [ ] Solve palindrome
- [ ] Solve anagram
- [ ] Find second largest
- [ ] Use two pointers
- [ ] Use sliding window
- [ ] Implement binary search
- [ ] Understand sorting complexity
- [ ] Use stack and queue
- [ ] Reverse a linked list
- [ ] Detect a linked-list cycle
- [ ] Explain BFS and DFS
- [ ] Explain recursion
- [ ] Explain Big-O
- [ ] Explain OOP concepts
- [ ] Explain Python ML libraries
- [ ] Process sensor data using Python
- [ ] Explain how coding connects to AI/ML
- [ ] Explain how data preprocessing can be performed
- [ ] Explain basic model inference
- [ ] Explain edge-device data processing

---

# 64. Key Takeaway

For this placement, don't prepare only LeetCode-style questions.

Prepare the combination:

**Python + DSA + Problem Solving + AI/ML Fundamentals + Data Processing + Edge/IoT Scenarios**

A coding question may be simple, while the follow-up can test whether you understand:

**Why this data structure?  
Why this algorithm?  
What is the complexity?  
Can you optimize it?  
How would this work with real-time/device data?**

That combination is more valuable for a technical interview than memorizing large numbers of programs.
