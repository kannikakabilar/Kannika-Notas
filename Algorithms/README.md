<h2 style="color:#0303ad">Algorithms I</h2>

Differentiate between **Big O** and **Little o** - what are constants c and N0 used for in the definition? (and you should know **Big Θ**)<br> <br>

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

7\. &ensp; Cousins in Binary Tree II - LeetCode Q2641
<br>Hint-Note: Sometimes integer & hashmap variables need to be declared outside functions (lie global variables to keep track of data) - (fo ex: tracking total sum of the node values for each level of a binary tree)

8\. &ensp; <mark style="background-color:#bbffa1">Back-Tracking DFS - Pseudo-Palindromic Paths in a Binary Tree - LeetCode Q1457</mark>
<br>Hint-Note: When values are within a certain range (ie: 0 to n-1) - using an array might be faster than a hashmap

9\. &ensp; Find Largest Value in Each Tree Row - LeetCode Q515

<h4 style="color:#0303ad">DFS HashMap Qs</h4>

10\. &ensp; Keys and Rooms - LeetCode Q841

11\. &ensp; Create Binary Tree from Description - (Tree Building w/ DFS) - LeetCode Q2196

<h4 style="color:#0303ad">DFS 4-Directional Graph-ish Qs</h4>

12\. &ensp; Num of Islands - LeetCode Q200

13\. &ensp; Max Area of Island - LeetCode Q695

14\. &ensp; Count Sub Islands - LeetCode Q1905

15\. &ensp; Number of Enclaves - LeetCode Q1020

16\. &ensp; <mark style="background-color:#bbffa1">Classic DFS Graph Q - Find if path exists in graph - LeetCode Q1971</mark>

17\. &ensp; <mark style="background-color:#fffaa1"><strong>Detect Cycles in 2D Grid - LeetCode Q1559</strong></mark>
<br>

<br>
<h3 style="color:#0303ad">Breadth-First Search</h3>

1\. &ensp; In <span style="color:#fc6b03">Java</span>:

        - Initialize a LinkedList Queue & just a LinkedList (built-in w/ Java)
        - Add an element to the LLQ
        - Remove and return the first element in the LLQ
        - Get the size of the LLQ
        - Get the value of the first element but do not return it


2\. <strong style="color:#0303ad">Tree-Level Order traversals are always handled with BFS</strong><br>

> - <a style="color:#000000">LeetCode Q429</a>
> 
> - <a style="color:#000000">LeetCode Q958</a>


<strong style="color:#0303ad">Very good Q to test understanding of BFS</strong><br>
3\. <mark style="background-color:#fffaa1"><strong>Complete Binary Tree Inserter - LeetCode Q919</strong></mark>


4\. <mark style="background-color:#bbffa1">Qs that can also be solved with DFS - LeetCode Q865</mark>


5\. <strong style="color:#0303ad">4-Directional type of Q using BFS</strong><br>

> - <a style="color:#000000">Rotting Oranges - LeetCode Q994</a>
>
> - <mark style="background-color:#fffaa1"><strong>Map of Highest Peak - LeetCode Q1765</strong></mark>
>
> - <a style="color:#000000">Nearest Exit from Entrance in Maze - LeetCode Q1926</a><br>


6\. <strong style="color:#0303ad">HashSet (for visited values) + BFS Qs</strong><br>

> - <a style="color:#000000">Minimum Genetic Mutation - LeetCode Q433</a>
>
> - <a style="color:#000000">Minimum Operations to Convert Number - LeetCode Q2059</a>
>
> - <a style="color:#000000">Lexicographically Smallest String After Applying Operations - LeetCode Q1625</a>
>
> - <a style="color:#000000">Word Ladder - LeetCode Q127</a>

**Notes-for-Q1625 and HashSet + BFS Qs**

    - how do you lexicographically compare strings in Java? (str1.compareTo(str2)<0 => str1<str2)
    - Use HashSet with BFS to keep track of the 'strings' that you have already visited
    - Create helper functions to perform respective modifications to string


7\. <mark style="background-color:#fffaa1"><strong>BFS Q that tests your Sorting knowledge - LeetCode Q2471</strong></mark>


8\. <mark style="background-color:#fffaa1"><strong>A common BFS / DFS Q - Is Graph Bipartite? - LeetCode Q785</strong></mark>

<br>

<h3 style="color:#0303ad">Recursion and Divide-&-Conquer</h3>

25\. LeetCode Q779 - Need to study
<br>Hint-Note: Build a tree when working with binary num replacements

26\. LeetCode Q390 - Don't understand - (Math related)

27\. LeetCode Q105, Q106, Q889(~slightly trickier) 
<br>Self-Note: If you can do Q105, then you can do Q106

Extra\. Closest Pair of Points Algorithm using DAC

**Note:** A common Div&Conq Q (that's not included here) is to find the closest pair of points,given a list of points.


<h3 style="color:#0303ad">Binary Search</h3>

28\. **Note:** It is important to realize that binary search can only be performed on ------ value-set / value-range / mountain-ish values-sets

29\. In <span style="color:#fc6b03">Java</span> sort a int \[\] arr using built-in sort. In an algorithm Q, if array sorted? => binary search. But sometimes you have to call the built-in sort on the given array.

<h4 style="color:#0303ad">Simple Basic Qs</h4>

30\. LeetCode Q374

31\. LeetCode Q744

32\. LeetCode Q1385
<br>Hint-Note: Subtraction in an absolute sign can result following range: |a - b| = c means b can be between a-c to a+c

<h4 style="color:#0303ad">Peaks & Valleys Qs</h4>

33\. LeetCode Q852

34\. LeetCode Q162

35\. LeetCode Q1901 (nlogm + 2D arr)

<h4 style="color:#0303ad">Maximize Consecutives Qs</h4>

36\. LeetCode Q1004 (if you do this one, you can do the one below)

37\. LeetCode Q2024

<h4 style="color:#0303ad">Search Rotated Array Qs</h4>

38\. LeetCode Q153

39\. LeetCode Q33

<h4 style="color:#0303ad">Search 2-D Array Q (logm * logn)</h4>

40\. LeetCode Q74

<h4 style="color:#0303ad">n*logm or (logm)*n where 'n' is for helper func Qs</h4>

41\. LeetCode Q2540
<br>Self-Note: Can also be solved in O(m+n) with merge-sort-like thinking but try doing it in n*logm

42\. LeetCode Q1237

43\. LeetCode Q1011
<br>Hint-Note: Try to understand what range/values can be iterated w/ binary search

<br>Hint-Note: Manually set your own 'high' value for below 2 Qs

44\. LeetCode Q2517

45\. LeetCode Q1170 (can skip this one if you have a good grasp of bin search)


___________________________________________
