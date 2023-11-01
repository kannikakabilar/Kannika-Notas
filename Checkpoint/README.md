<h1 style="color:#000000">Checkpoint</h1>

<h2 style="color:#8096c2">Bit Logic</h2>

1. &ensp; bin# * (2^x) = \[How would the answer look like?\]

2. &ensp; **x** xor **0** = ? &ensp;&ensp; **x** xor **1** = ?

3. &ensp; State 2 ways to write a negative number in binary

4. &ensp; Perform left & right \[rotate, logical-shift, arithmetic-shift\] of **1100**

5. &ensp; LeetCode Q1720

6. &ensp; LeetCode Q136

7. &ensp; In <span style="color:#fc6b03">Java</span>:

    - given an int var, return # of 1s in its bin rep
    - given an int var, reverse its bin form and return as int
    - convert an int var to binary sting
    - convert bin string to int

8. &ensp; Reverse loop through binary string

9. &ensp; LeetCode Q338

10. &ensp; Briefly differentiate between signed vs unsigned int

11. &ensp; How do you perform arithmetic & logical shifts in <span style="color:#fc6b03">Java</span> - show with an example

12. &ensp; What gets printed?

```java
int num = 5;
System.out.println(~num);
```


13\. &ensp; Briefly describe what is bitmasking?

___________________________________________

<h2 style="color:#5c91fa">Data Structures I</h2>

1. &ensp; Differentiate DS Terms: Primitive vs. Non-Primitive ; Linear vs. Non-Linear ; Static vs. Dynamic

<h3 style="color:#5c91fa">Arrays</h3>
2. &ensp; Arrays: indexing = O(?) and everything else = O(?)

3. &ensp; LeetCode Q108

4. &ensp; LeetCode Q704

5. &ensp; LeetCode Q88

6. &ensp; LeetCode Q121

7. &ensp; LeetCode Q283

8. &ensp; If elements of an array are from 1 to n => then how can you approach it? LeetCode Q287

9. &ensp; Kadane's algo LeetCode Q287

<h3 style="color:#5c91fa">Linked Lists</h3>
10\. &ensp; LinkedLists: inserting = O(?) and everything else = O(?)

11\. &ensp; LeetCode Q21

12\. &ensp; LeetCode Q83

13\. &ensp; LeetCode Q203

14\. &ensp; LeetCode Q206

15\. &ensp; LeetCode Q876

16\. &ensp; LeetCode Q234

17\. &ensp; LeetCode Q1290

18\. &ensp; What are the 2 ways to check if a LL has cycle? LeetCode Q141

<h3 style="color:#5c91fa">Hash Table</h3>

19\. &ensp; Define Terms: **Hash Function** ; **Collision & Chaining** ; **Open-Addressing & Linear-Probing**

20\. &ensp; HashMaps in <span style="color:#fc6b03">Java</span>:

    - Intialize a hashmap that will store name string as key and age int as value
    - Add an key-value element to it
    - Get value given a key
    - Check if map contains key and Update key that's already in the map
    - loop through keySet
    - loop through values
    - Delete an element

* HashMaps in <span style="color:#fc6b03">Java</span> are pass by _________ (if hashmap is passed into a function and its values are changed, then the changes can be seen _______ ___ ________ ___)

21\. &ensp; HashSets in <span style="color:#fc6b03">Java</span>:

    - Intialize a hashset that will store numbers (ints)
    - Add an element
    - Check if the set has an element
    - Get the Size of the set
    - Remove an element
    - Clear all elements
    - Convert an **ArrayList** to a HashSet

Note: Hash Tables (work similar to HashMaps) aren’t used anymore but they provide enumeration and are thread safe while Hash Maps don’t

- **Sample HashMap and HashSet Questions to Think About**
  - Find a pair of nums with given sum and an array of nums<br>
  - Roman Numeral to Num<br>
  - Keeping track of values<br>
  - is Isomorphic?<br>
  - is Anagram? (ie: Nathaniel Black => Anabella Thick)<br>
  - is List unique?<br>
  - union & intersection of 2 LL<br>
  - missing elements of a range<br><br>

22\. &ensp; Given an array, find 4 elements such that a + b = c + d

23\. &ensp; LeetCode Q2610

i\. &ensp; Arrays + HashMap - LeetCode Q1282

<h3 style="color:#1669f0">Two Pointers</h3>

24\. &ensp; Loop through all pairs of elements - LeetCode Q2824

25\. &ensp; Perform palindrome check in O(n/2) - LeetCode Q125

26\. &ensp; Tricky Palindrome Q - LeetCode Q1332

27\. &ensp; Partitioning Array - LeetCode Q905

28\. &ensp; Give 3 ways to have 2-Pointers in 1 Array
    - palindrome-like
    - even & odd index
    - window-sliding - LeetCode Q1343

<br>

29\. &ensp; Loop through all subsets of an array

<h3 style="color:#1669f0">Math</h3>

30\. &ensp; How would you handle big numbers in <span style="color:#fc6b03">Java</span> and how would you handle them in <span style="color:#fcc603">JavaScript</span> - LeetCode Q2117

31\. &ensp; Working with Prime Numbers - LeetCode Q866, Q204

32\. &ensp; Reverse an Integer - LeetCode Q7

33\. &ensp; Formula for summing 2+4+6+8+..+n - LeetCode Q1551
    - nth term = 2 + 2*(n-1)
    - sum total = n * (2 + nth term)/2

<br>

34\. &ensp; Formula for summing 1+3+5+..+n
    - nth term = 1 + 2*(n-1)
    - sum total = n * (1 + nth term)/2
    - sum of 1+2+3+4+5+...+n = n*(n+1)/2

35\. &ensp; Like converting a decimal number to binary - LeetCode Q1780 (Num is sum of powers of 3?)

___________________________________________

<h2 style="color:#8096c2">Data Structures II</h2>

<h3 style="color:#1669f0">Stacks</h3>
1\. &ensp; Stacks are used for evaluating: parentheses; math expr; recursive function calls

2\. &ensp; LeetCode Q20

3\. &ensp; LeetCode Q844

4\. &ensp; LeetCode Q1021

5\. &ensp; LeetCode Q1047

6\. &ensp; LeetCode Q1441

7\. &ensp; LeetCode Q1598

8\. &ensp; LeetCode Q1614

9\. &ensp; LeetCode Q946

10\. &ensp; LeetCode Q1249/Q921

<h3 style="color:#1669f0">Queues</h3>

11\. &ensp; Time Needed to But Tickets - LeetCode Q2073

12\. &ensp; Weave pattern using queues - LeetCode Q950

<h3 style="color:#1669f0">Priority Queues OR Min/Max Heaps</h3>

13\. &ensp; In <span style="color:#fc6b03">Java</span>:
    
        - Initialize Min Heap & Max Heap
        - Add elements to the heap
        - Pop-out the min or max element
        - Get the size of the heap
    <br> -------------------------------------------- <br>
        - Create an ArrayList of Priority Queues
