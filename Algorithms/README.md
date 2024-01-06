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

<strong style="color:#0303ad">1. Basic DFS Qs</strong>

> - <a style="color:#000000">Find all Battleships on a board (DFS on 2D array) - LeetCode Q419 & Q1992</a>
>
> - <a style="color:#000000">Find all Groups of Farmland - LeetCode Q1992</a>
>
> - <a style="color:#000000">Where will the Ball Fall - simple DFS - LeetCode Q1706</a>
>
> - <a style="color:#000000">Validate Binary Search Tree - LeetCode Q98</a><br>Hint-Note: When working with extreme integer values -> you can use Long.MIN_VALUE to Long.MAX_VALUE to act as -infinity to +infinity
&ensp; 


<strong style="color:#0303ad">2. DFS Tree Qs</strong>

> - <a style="color:#000000">Can Flipping SubTrees make them equivalent? - LeetCode Q951</a>
>
> - <a style="color:#000000">Lowest Common Ancester - LeetCode Q1123</a>
>
> - <a style="color:#000000">All paths from source to target - LeetCode Q797</a>
>
> - <a style="color:#000000">Cousins in Binary Tree II - LeetCode Q2641</a><br>Hint-Note: Sometimes integer & hashmap variables need to be declared outside functions (lie global variables to keep track of data) - (for ex: tracking total sum of the node values for each level of a binary tree)
>
> - <a style="color:#000000">Find Largest Value in Each Tree Row - LeetCode Q515</a>

**3\.** <mark style="background-color:#bbffa1">Back-Tracking DFS - Pseudo-Palindromic Paths in a Binary Tree - LeetCode Q1457</mark>
<br>Hint-Note: When values are within a certain range (ie: 0 to n-1) - using an array might be faster than a hashmap

<strong style="color:#0303ad">4. DFS HashMap Qs</strong>

> - <a style="color:#000000">Keys and Rooms - LeetCode Q841</a>
>
> - <a style="color:#000000">Create Binary Tree from Description - (Tree Building w/ DFS) - LeetCode Q2196</a>


<strong style="color:#0303ad">5. DFS 4-Directional Graph-ish Qs</strong>

> - <a style="color:#000000">Num of Islands - LeetCode Q200
>
> - <a style="color:#000000">Max Area of Island - LeetCode Q695
>
> - <a style="color:#000000">Count Sub Islands - LeetCode Q1905
>
> - <a style="color:#000000">Number of Enclaves - LeetCode Q1020
>
> - <mark style="background-color:#bbffa1">Classic DFS Graph Q - Find if path exists in graph - LeetCode Q1971</mark>
>
> - <mark style="background-color:#fffaa1"><strong>Detect Cycles in 2D Grid - LeetCode Q1559</strong></mark>

<br>

<br>
<h3 style="color:#0303ad">Breadth-First Search</h3>

**1\.** &ensp; In <span style="color:#fc6b03">Java</span>:

        - Initialize a LinkedList Queue & just a LinkedList (built-in w/ Java)
        - Add an element to the LLQ
        - Remove and return the first element in the LLQ
        - Get the size of the LLQ
        - Get the value of the first element but do not return it


<strong style="color:#0303ad">2. Tree-Level Order traversals are always handled with BFS</strong><br>

> - <a style="color:#000000">LeetCode Q429</a>
> 
> - <a style="color:#000000">LeetCode Q958</a>


<strong style="color:#0303ad">Very good Q to test understanding of BFS</strong><br>
**3\.** <mark style="background-color:#fffaa1"><strong>Complete Binary Tree Inserter - LeetCode Q919</strong></mark>


**4\.** <mark style="background-color:#bbffa1">Qs that can also be solved with DFS - LeetCode Q865</mark>


<strong style="color:#0303ad">5. 4-Directional type of Q using BFS</strong><br>

> - <a style="color:#000000">Rotting Oranges - LeetCode Q994</a>
>
> - <mark style="background-color:#fffaa1"><strong>Map of Highest Peak - LeetCode Q1765</strong></mark>
>
> - <a style="color:#000000">Nearest Exit from Entrance in Maze - LeetCode Q1926</a><br>


<strong style="color:#0303ad">6. HashSet (for visited values) + BFS Qs</strong><br>

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


**7\.** <mark style="background-color:#fffaa1"><strong>BFS Q that tests your Sorting knowledge - LeetCode Q2471</strong></mark>


**8\.** <mark style="background-color:#fffaa1"><strong>A common BFS / DFS Q - Is Graph Bipartite? - LeetCode Q785</strong></mark>

<br>

<h3 style="color:#0303ad">Recursion and Divide-&-Conquer</h3>

> - <a style="color:#000000">LeetCode Q779 - Need to study</a>
> <br><a style="color:#0303ad">Hint-Note: Build a tree when working with binary num replacements</a>
>
> - <a style="color:#000000">LeetCode Q390 - Don't understand - (Math related)</a>
>
> - <a style="color:#000000">LeetCode Q105, Q106, Q889(~slightly trickier)</a>
> <br><a style="color:#0303ad">Self-Note: If you can do Q105, then you can do Q106

<strong style="color:#0303ad">Extra Q</strong> 
> - <a style="color:#000000">Closest Pair of Points Algorithm using DAC</a>
> <br> **Note:** This is a common Div&Conq Q: to find the closest pair of points, given a list of points.


<h3 style="color:#0303ad">Binary Search</h3>

<strong style="color:#0303ad">Notes</strong><br>
<strong style="color:#0303ad">*</strong> It is important to realize that binary search can only be performed on ------ value-set / value-range / mountain-ish values-sets

<strong style="color:#0303ad">*</strong> In <span style="color:#fc6b03">Java</span> sort a int \[\] arr using built-in sort. In an algorithm Q, if array sorted? => binary search. But sometimes you have to call the built-in sort on the given array.

<strong style="color:#0303ad">1. Simple Basic Qs</strong>

> - <a style="color:#000000">Guess Number Higher or Lower - LeetCode Q374</a>
>
> - <a style="color:#000000">Find Smallest Letter Greater Than Target - LeetCode Q744</a>
>
> - <a><mark style="background-color:#fffaa1"><strong style="color:#000000">Find the Distance Value Between Two Arrays - LeetCode Q1385</strong></mark>
> <br><a style="color:#0303ad">Binary Search can also be used to find if an element in a sorted array is in a specified range (instead of looking for a target element)</a>

<strong style="color:#0303ad">2. Peaks & Valleys Qs</strong>

> - <a style="color:#000000">Peak Index in a Mountain Array - LeetCode Q852</a>
> - <a style="color:#000000">Find in Mountain Array - LeetCode Q1095</a>
>
> - <a style="color:#000000">Find Peak Element - LeetCode Q162</a>
>
> - <a style="color:#000000"><strong>So Annoying! </strong><mark style="background-color:#fffaa1"><strong>Find Peak Element II - LeetCode Q1901 (nlogm + 2D arr)</strong></mark></a>

<strong style="color:#0303ad">3. Maximize Consecutives Qs</strong>

> - <a style="color:#000000">Max Consecutive Ones III - LeetCode Q1004 (if you do this one, you can do the one below)</a>
>
> - <a style="color:#000000">Maximize the Confusion of an Exam - LeetCode Q2024</a>

<strong style="color:#0303ad">4. Search Rotated Array Qs</strong>

> - <a style="color:#000000">Find Minimum in Rotated Sorted Array - LeetCode Q153
> - <a style="color:#000000"><mark style="background-color:#fffaa1"><strong>Find Minimum in Rotated Sorted Array II - LeetCode Q154</strong></mark></a>
>
> - <a style="color:#000000">Search in Rotated Sorted Array - LeetCode Q33</a>
> - <a style="color:#000000">Search in Rotated Sorted Array II - LeetCode Q81</a>

<strong style="color:#0303ad">5. n*logm or (logm)*n where 'n' is for helper func or outer-loops</strong>

> - <a style="color:#000000">Search a 2D Matrix - LeetCode Q74</a>
> <br><a style="color:#0303ad">Exception: (logm * logn)</a>
>
> - <a style="color:#000000">Search a 2D Matrix II - LeetCode Q240</a>
>
> - <a style="color:#000000">Minimum Common Value - LeetCode Q2540</a>
> <br><a style="color:#0303ad">Self-Note: Can also be solved in O(m+n) with merge-sort-like thinking but try doing it in n*logm</a>
>
> - <a style="color:#000000">Find Positive Integer Solution for a Given Equation - LeetCode Q1237</a>
>
> - <a style="color:#000000">Capacity to Ship Packages within D days - LeetCode Q1011</a>
> <br><a style="color:#0303ad">Hint-Note: Try to understand what range/values can be iterated w/ binary search</a>
>
> <br><a style="color:#0303ad">Hint-Note: Manually set your own 'high' value for below 2 Qs</a>
>
> - <a style="color:#000000">Maximum Tastiness of Candy Basket - LeetCode Q2517</a>
>
> - <a style="color:#000000">Compare Strings by Frequency of the Smallest Characters - LeetCode Q1170</a>
> <br><a style="color:#0303ad">(can skip this one if you have a good grasp of bin search)</a>
>
> - <a style="color:#000000">LeetCode Q1482</a>

___________________________________________
