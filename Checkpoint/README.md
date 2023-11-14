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

1\. &ensp; Differentiate DS Terms: Primitive vs. Non-Primitive ; Linear vs. Non-Linear ; Static vs. Dynamic

<h3 style="color:#5c91fa">Arrays</h3>
2\. &ensp; Arrays: indexing = O(?) and everything else = O(?)

3\. &ensp; LeetCode Q108

4\. &ensp; LeetCode Q704

5\. &ensp; LeetCode Q88

6\. &ensp; LeetCode Q121

7\. &ensp; LeetCode Q283

8\. &ensp; If elements of an array are from 1 to n => then how can you approach it? 

    - LeetCode Q287
    - LeetCode Q41 (Need to learn the trick!)
    - LeetCode Q1608

9\. &ensp; Kadane's algo LeetCode Q287

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

20\. &ensp; HashMaps in <span style="color:#fc6b03">Java</span>: (skip/skim-over 20. & 21. if you're confident in HashMap & HashSets)

    - Intialize a hashmap that will store name string as key and age int as value
    - Add an key-value element to it
    - Get value given a key
    - Check if map contains key and Update key that's already in the map
    - loop through keySet
    - loop through values
    - Delete an element

* HashMaps in <span style="color:#fc6b03">Java</span> are pass by --------- (if hashmap is passed into a function and its values are changed, then the changes can be seen ------- --- -------- ---)

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

ii\. &ensp; Smallest Infinite Set - LeetCode Q2336

iii\. &ensp; Tricky Hashset Q - LeetCode Q888

<h3 style="color:#5c91fa">Two Pointers</h3>

24\. &ensp; Loop through all pairs of elements - LeetCode Q2824

25\. &ensp; Perform palindrome check in O(n/2) - LeetCode Q125

26\. &ensp; Tricky Palindrome Q - LeetCode Q1332 
<br> Hint-Note: Think about base-case string with length 3

27\. &ensp; Partitioning Array - LeetCode Q905 => Q922(harder)

28\. &ensp; Give 3 ways to have 2-Pointers in 1 Array

    - palindrome-like
    - even & odd index
    - window-sliding - LeetCode Q1343


29\. &ensp; Loop through all subsets of an array

<h3 style="color:#5c91fa">Math</h3>

30\. &ensp; How would you handle big numbers in <span style="color:#fc6b03">Java</span> and how would you handle them in <span style="color:#fcc603">JavaScript</span> - LeetCode Q2117

31\. &ensp; Working with Prime Numbers - LeetCode Q866, <mark style="background-color:#efe3ff"><strong>Q204 (Need to learn Sieve of Eratosthenes)</strong></mark>

32\. &ensp; Reverse an Integer - LeetCode Q7

33\. &ensp; Formula for summing 2+4+6+8+..+n - LeetCode Q1551 <br>
    - nth term = 2 + 2*(n-1) <br>
    - sum total = n * (2 + nth term)/2 <br>


34\. &ensp; Formula for summing 1+3+5+..+n <br>
    - nth term = 1 + 2*(n-1) <br>
    - sum total = n * (1 + nth term)/2 <br>
    - sum of 1+2+3+4+5+...+n = n*(n+1)/2 <br>

35\. &ensp; Like converting a decimal number to binary - LeetCode Q1780 (Num is sum of powers of 3?)

___________________________________________

<h2 style="color:#1669f0">Data Structures II</h2>

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

12\. &ensp; Weave pattern using queues - LeetCode <mark style="background-color:#efe3ff"><strong>Q950</strong></mark>
<br>Hint-Note: Think in reverse-order => in the game you reveal a card and then put one card at the end of the deck - so when we are designing the deck => we add the highest-value card (deck array sorted in descending array) to the deck, then we remove a card from the bottom to and place it on top, and then we add the next highest-value card and so on..

<h3 style="color:#1669f0">Priority Queues OR Min/Max Heaps</h3>

13\. &ensp; In <span style="color:#fc6b03">Java</span>:
    
    - Initialize Min Heap & Max Heap
    - Add elements to the heap
    - Pop-out the min or max element
    - Get the min or max element but don't remove it
    - Get the size of the heap
    - Remove an element 'x' from the heap
    ---------------------------------------------
    - Create an ArrayList of Priority Queues
    - Try doing LeetCode Q2593 or any othe heap Q that you haven't done before

<h3 style="color:#1669f0">Trees</h3>

14\. &ensp; Describe how these simple trees work: N-ary ; Binary ; BST

15\. &ensp; AVL Trees are better for --------- , because the height <= log2(n) <br>
    - left-left case => ? <br>
    - left-right case => ? <br>

16\. &ensp; Red-Black Trees are better for --------- and -------- <br>
    - What are the 4 rules for Red-Black Trees? <br>

17\. &ensp; B-Tree <br>
    - Each node can have upto (how many?) values <br>
    - Each non-leaf node must have at least (how many?) children and atmost (how many?) children <br>
    - All leaves have the same ----- <br>

18\. &ensp; Heaps (Min/Max Priority Queues) <br>
    - How do you insert in heaps? <br>
    - How do you delete in heaps? <br>

19\. &ensp; Treaps are a mix of --- and ---- <br>
    - Each node stores 2 values (what are they - what kind of values?) <br>
    - How do you insert? And what happens after insertion? <br>

20\. &ensp; Splay Trees are just like BST but perform AVL rotations each time an event occurs (what event?) and it updates the root node accordingly

21\. &ensp; LeetCode Q938

22\. &ensp; LeetCode Q590 (How do you concatenate 2 arraylists in java?)

23\. &ensp; LeetCode Q226

24\. &ensp; LeetCode Q1022

25\. &ensp; LeetCode Q1448

26\. &ensp; LeetCode Q2265 (helper functions are sometimes needed when working with trees)

27\. &ensp; LeetCode Q1026

28\. &ensp; <mark style="background-color:#efe3ff"><strong>LeetCode Q894</strong></mark>
<br>Hint-Note: Think about if there are n total nodes, 1 for root and i nodes for left-subtree, how much would the right subtree have?
<br> -use recursion to generate subtrees with i nodes for left-subtree and for each left-subtree loop through every possible right-subtree
<br> -store the list of subtrees of size-n-nodes into a hashmap

29\. &ensp; Balance a Binary Search Tree - LeetCode Q1382 (how do you get subarray of an arraylist?)

30\. &ensp; <mark style="background-color:#efe3ff"><strong>LeetCode Q2415</strong></mark>
<br> Hint-Note: Think of the first few base cases. left-subtree needs to swap values with right subtree. After that, the left-left-subtree will swap values with right-right-subtree and the left-right-subtree will swap values with right-left-subtree. Ofcourse, pefrorm the swap only when the levels are odd.

31\. &ensp; LeetCode Q1325

33\. &ensp; <mark style="background-color:#efe3ff"><strong>LeetCode Q1104</strong></mark>
<br> Hint-Note: Try drawing a normal (non-zigzag tree) and see how you can get the value of parent given value of child node and then compare it by drawing the zigzag tree.

34\. &ensp; LeetCode Q208 (Trie), Q14

35\. &ensp; <mark style="background-color:#efe3ff"><strong>LeetCode Q1373</strong></mark>
<br> Hint-Note: Perform a variation of post-order traversal to make it time efficient

<h3 style="color:#1669f0">Graphs</h3>

36\. &ensp; LeetCode Q1557
<br>Hint-Note: A node that does not have any incoming edge can only be reached by itself => only count the node w/ zero incoming edges

37\. &ensp; LeetCode Q1615

38\. &ensp; LeetCode Q2374

39\. &ensp; LeetCode Q2508 (good practice Q)
<br>Hint-Note: The number of nodes with an odd-degree in the original graph should be either 0, 2, or 4. Try to work on each of these cases.
<br>Hint-Note: Use Pair to store hashset of edges

```java
Pair p1 = new Pair(1, 2);
```

40\. &ensp; Define the following Graph Terms

    - order of a graph
    - size of a graph
    - null graph
    - complete graph
    - adjacency matrix
    - adjacency list

**Graph-Note:** When given a list of edges, it's very useful to store them in a HashMap

**! Data Structures Conclusive Note:** A search in a sorted collection, think binary search. Minimum # of steps, think BFS. Min/max K elements, think heap. Optimization, think DP. Parentheses, think stacks.

___________________________________________

<h2 style="color:#0303ad">Algorithms</h2>

**Big O**: f(n) ∈ O(g(n)) iff for some constant C and N0, f(N) <= c * g(N) for all N > N0 <br>
**Big Ω**: f(n) ∈ Ω(g(n)) iff for some constant C and N0, f(N) >= c * g(N) for all N > N0 <br>
**Big Θ**: f(n) ∈ Θ(g(n)) iff f(n) ∈ Ω(g(n)) AND f(n) ∈ O(g(n)) <br> <br>

**Little o**: f(n) ∈ o(g(n)) iff for some constant C and N0, f(N) < c * g(N) for all N > N0 <br>
<span style="color:red">!Note: Strictly less than NOT equal to</span> <br> <br>

**Worst case**: an input that causes the maximum time for the program to complete execution <br> <br>

**Amortized Time** <br>
&ensp;&ensp;  = Time_taken_for_N_operations/N (~> average time taken for each operation) <br>
&ensp;&ensp;  = (time taken for normal ops + time taken for slow ops) / N <br> <br>

| Cost of Nth insertion 
|---------------------------------|
| = O(N), if N-1 is a power of 2
| = O(1), otherwise

| Amortized Cost
|---------------------------------|
| = ( O(1+1+1+...) + O(1+2+4+...) ) / N
| &ensp;&ensp;&ensp; ^N terms &ensp;&ensp; &ensp;&ensp; ^(log2N)+1 terms
| = ( O(N) + O(2N) ) / N 
| = O(1)

<br> 

**Easily Reduced Time Complexity**: electronically transferring a file = O(size_of_file) ; transferring a file by airplane = O(1)
<br> <br>

<h3 style="color:#0303ad">Depth-First Search</h3>

<h4 style="color:#0303ad">Sample DFS Qs</h4>

1\. &ensp; Find all Battleships on a board (DFS on 2D array) - LeetCode Q419 & Q1992

2\. &ensp; Where will the Ball Fall - simple DFS - LeetCode Q1706

3\. &ensp; Validate Binary Search Tree - LeetCode Q98
<br>Hint-Note: When working with extreme integer values -> you can use Long.MIN_VALUE to Long.MAX_VALUE to act as -infinity to +infinity

<h4 style="color:#0303ad">DFS Tree Qs</h4>

4\. &ensp; Can Flipping SubTrees make them equivalent? - LeetCode Q951

5\. &ensp; Lowest Common Ancester - LeetCode Q1123

6\. &ensp; All paths from source to target - LeetCode Q797
<br>Hint-Note: Sometimes integer & hashmap variables need to be declared outside functions (lie global variables to keep track of data) - (fo ex: tracking total sum of the node values for each level of a binary tree)

7\. &ensp; Cousins in Binary Tree II - LeetCode Q2641

8\. &ensp; Back-Tracking DFS - Pseudo-Palindromic Paths in a Binary Tree - LeetCode Q1457
<br>Hint-Note: When values are within a certain range (ie: 0 to n-1) - using an array might be faster than a hashmap

9\. &ensp; Find Largest Value in Each Tree Row - LeetCode Q515

10\. &ensp; Tricky One! (need to study) Distribute Coins in Binary Tree - LeetCode Q979

<h4 style="color:#0303ad">DFS HashMap Qs</h4>

11\. &ensp; Keys and Rooms - LeetCode Q841

12\. &ensp; Create Binary Tree from Description - (Tree Building w/ DFS) - LeetCode Q2196

<h4 style="color:#0303ad">DFS 4-Directional Graph-ish Qs</h4>

13\. &ensp; Num of Islands - LeetCode Q200

14\. &ensp; Max Area of Island - LeetCode Q695

15\. &ensp; Count Sub Islands - LeetCode Q1905

16\. &ensp; Number of Enclaves - LeetCode Q1020

17\. &ensp; Classic DFS Graph Q (Need to study!) - Find if path exists in graph - LeetCode Q1971

<br> <br>

<h3 style="color:#0303ad">Breadth-First Search</h3>

18\. &ensp; In <span style="color:#fc6b03">Java</span>:

        - Initialize a LinkedList Queue & just a LinkedList (built-in w/ Java)
        - Add an element to the LLQ
        - Remove and return the first element in the LLQ
        - Get the size of the LLQ
        - Get the value of the first element but do not return it

19\. LeetCode Q429, LeetCode Q958
<br>Hint-Note: Tree-Level Order traversals are always handled with BFS

20\. Complete Binary Tree Inserter - LeetCode Q919
<br>Self-Note: Very good Q to test understanding of BFS

21\. Qs that can also be solved with DFS - LeetCode Q865 (unusual one), LeetCode Q1625 
<br>Notes-for-Q1625
    - how do you lexicographically compare strings in Java?)
    - Use HashMaps with BFS to keep track of the 'strings' that you have already visited
    - Create helper functions to perform respective modifications to string

22\. 4-Directional type of Q using BFS - LeetCode Q994, LeetCode Q1765

23\. Trickier but follows a routine BFS Q - LeetCode Q752, LeetCode Q433
<br>Hint-Note: Use HashMaps with BFS to keep track of the 'strings' that you have already visited

24\. BFS Q that tests your Sorting knowledge - LeetCode Q2471

25\. Interesting and Unique BFS Q - (need to study) - LeetCode Q967

**Note:** A common BFS / DFS Q (that's not included here) is to check if a given graph is bipartite


<h3 style="color:#0303ad">Recursion and Divide-&-Conquer</h3>

26\. LeetCode Q779 - Need to study
<br>Hint-Note: Build a tree when working with binary num replacements

27\. LeetCode Q390 - Don't understand - (Math related)

28\. LeetCode Q105, Q106, Q889(~slightly trickier) 
<br>Self-Note: If you can do Q105, then you can do Q106

**Note:** A common Div&Conq Q (that's not included here) is to find the closest pair of points,given a list of points.


<h3 style="color:#0303ad">Binary Search</h3>

29\. **Note:** It is important to realize that binary search can only be performed on ------ value-set / value-range / mountain-ish values-sets

30\. In <span style="color:#fc6b03">Java</span> sort a int \[\] arr using built-in sort. In an algorithm Q, if array sorted? => binary search. But sometimes you have to call the built-in sort on the given array.

<h4 style="color:#0303ad">Simple Basic Qs</h4>

31\. LeetCode Q374

32\. LeetCode Q744

33\. LeetCode Q1385
<br>Hint-Note: Subtraction in an absolute sign can result following range: |a - b| = c means b can be between a-c to a+c

<h4 style="color:#0303ad">Peaks & Valleys Qs</h4>

34\. LeetCode Q852

35\. LeetCode Q162

36\. LeetCode Q1901 (nlogm + 2D arr)

<h4 style="color:#0303ad">Maximize Consecutives Qs</h4>

37\. LeetCode Q1004 (if you do this one, you can do the one below)

38\. LeetCode Q2024

<h4 style="color:#0303ad">Search Rotated Array Qs</h4>

39\. LeetCode Q153

40\. LeetCode Q33

<h4 style="color:#0303ad">Search 2-D Array Q (logm * logn)</h4>

41\. LeetCode Q74

<h4 style="color:#0303ad">n*logm or (logm)*n where 'n' is for helper func Qs</h4>

42\. LeetCode Q2540
<br>Self-Note: Can also be solved in O(m+n) with merge-sort-like thinking but try doing it in n*logm

43\. LeetCode Q1237

44\. LeetCode Q1011
<br>Hint-Note: Try to understand what range/values can be iterated w/ binary search

<br>Hint-Note: Manually set your own 'high' value for below 2 Qs

45\. LeetCode Q2517

46\. LeetCode Q1170 (can skip this one if you have a good grasp of bin search)


___________________________________________

<h2 style="color:#0303ad">Algorithms II</h2>
