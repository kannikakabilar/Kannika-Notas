<h2 style="color:#0303ad">Algorithms II</h2>

<h3 style="color:#0303ad">Sorting</h3>

1\. How do you sort int \[\] vs List\<Integer\> in Java?

2\. <mark style="background-color:#efe3ff"><strong>How do you create a comparator? - LeetCode Q1636</strong></mark>
<br>**Note:** Comparator only works with ArrayList. 

3\. How can you check anagrams w/o hashmaps? - LeetCode Q2273
<br>Hint-Note: char array => sort => toString => compare strings

4\. Easy Q - LeetCode Q2037
<br> Some-Extra: LeetCode Q1200

5\. How do you get the largest 2 integer of an array in O(n)? - LeetCode Q628
<br>Hint-Note: Get product of 3 largest ints and compare it with product of 2 smallest int and largest int

6\. LeetCode Q1630 - &ensp; In <span style="color:#fc6b03">Java</span>:

    - How do you get subarray of int[] in Java?
    - How do you check if 2 int[] arrays are equal?

7\. Good practice Qs for sorting - LeetCode Q1887, LeetCode Q49

<h4 style="color:#0303ad">Topological Sort = DFS + HashMaps (sometimes BFS)</h4>

(Try drawing the graph for some of these Q, it might help)
<br> **Rule of Thumb:** Convert 2-D array or graph/edges to hashmap. Have a recursive dfs function. An additional HashMap or HashSets are used to keep track of 'visited' nodes/values.

8\. Loud and Rich - LeetCode Q851

9\. Course Schedule series - LeetCode Q207, LeetCode Q210, LeetCode Q1462 (good one)

10\. Find Eventual Safe States - LeetCode Q802

11\. Find All Possible Recipes from Given Supplies - LeetCode Q2115

12\. Minimum Height Trees - LeetCode Q310 (via BFS ~ Need to study but doesn't seem like an important Topo Sort Q)

13\. Longest Cycle in a Graph - LeetCode Q2360 **(If you can do this, you can do all above Topo Sort Qs)**

<h4 style="color:#0303ad">Merge Sort</h4>

14\. Merge k Sorted Lists - LeetCode Q23

<h4 style="color:#0303ad">Other Sorting Algorithms to study</h4>

- Quick Sort, Heap Sort
- Bubble Sort, Insertion Sort, Selection Sort


<h3 style="color:#0303ad">Dynamic Programming I</h3>

<p style="color:#0303ad">Fibonacci Style DP Qs - Use variables to store values of previous state</p>

1\. Climbing Stairs - LeetCode Q70

2\. Flip String to Monotone Increasing - LeetCode Q926

3\. <strong style="color:#fc425b">Max Product Subarray - LeetCode Q152</strong>

4\. <strong style="color:#fc425b">Count Sorted Vowel Strings - LeetCode Q1641</strong>

<p style="color:#0303ad">Iterate through the given array to solve the bigger problem</p>

5\. Minimum Time to Make Rope Colorful - LeetCode Q1578

6\. Arithmetic Slices - LeetCode Q413

7\. Minimum Cost of Climbing Stairs - LeetCode Q746

8\. House Robber - LeetCode Q198

9\. <strong style="color:#fc425b">Count Substrings that differ by One Character - LeetCode Q1638</strong>

<p style="color:#0303ad">Following Qs can be solved with 1-D dp array and then can be optimized into just using variables</p>

10\. Decode Ways - LeetCode Q91

11\. Count Number of Teams - LeetCode Q1395 
</br><a>Use two 1-D arrays => n^2</a>

<p style="color:#0303ad">Questions that are better done with a Bottom-Up approach using a 1-D dp array</p>

12\. Coin Change, Perfect Squares - LeetCode Q322, Q279
</br><a>You can do one or the other</a>

13\. Longest Increasing Subsequence - LeetCode Q300

14\. Minimum Cost for Tickets - LeetCode Q983

15\. Number of Good Ways to Split a String - LeetCode Q1525

16\. Word Break - LeetCode Q139

17\. Fair Distribution of Cookies - LeetCode Q2305

18\. <strong style="color:#fc425b">Partition Array for Max Sum - LeetCode Q1043</strong>

19\. <strong style="color:#fc425b">Partition Equal Subset Sum</strong>

<p style="color:#0303ad">Palindromic Qs</p>

20\. Longest Palindrome Substring - LeetCode Q5

21\. Palindromic Substrings - LeetCode Q647

<h3 style="color:#0303ad">Dynamic Programming II</h3>

<p style="color:#0303ad">Self-Note: For all of the 2-D DP Qs, draw out the choices in a tree or 2-D grid and it'll be easier</p>

<p style="color:#0303ad">Questions that are done with a 2-D dp array but can be optimized into just a 1-D dp array</p>

1\. Unique Paths - LeetCode Q62
