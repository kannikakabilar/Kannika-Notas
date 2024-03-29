<h2 style="color:#1669f0">Algorithms II</h2>

<h3 style="color:#1669f0">Sorting</h3>

<strong style="color:#1669f0">1. Basics in Sorting</strong>

> - <a style="color:#000000">How do you sort int \[\] vs List\<Integer\> in <span style="color:#fc6b03">Java</span>?</a>
>
> - <a style="color:#000000">How do you create a comparator? - LeetCode Q1636</a>
<br>**Note:** Comparator only works with ArrayList. 
>
> - <a style="color:#000000">How can you check anagrams w/o hashmaps? - LeetCode Q2273</a>
<br>Hint-Note: char array => sort => toString => compare strings
>
> - <a style="color:#000000">Easy Q - LeetCode Q2037</a>
<br> Some-Extra: LeetCode Q1200
>
> - <a style="color:#000000">How do you get the largest 2 integer of an array in O(n)? - LeetCode Q628</a>
<br>Hint-Note: Get product of 3 largest ints and compare it with product of 2 smallest int and largest int
>
> - <a style="color:#000000">LeetCode Q1630 - &ensp; In <span style="color:#fc6b03">Java</span>:</a>

    - How do you get subarray of int[] in Java?
    - How do you check if 2 int[] arrays are equal?

> - <a style="color:#000000">Good practice Qs for sorting - LeetCode Q1887, LeetCode Q49</a>

<br>

<strong style="color:#1669f0">2. Topological Sort = DFS + HashMaps (sometimes BFS)</strong>

> <a style="color:#1669f0"> **Rule of Thumb:** Convert 2-D array or graph/edges to hashmap. Have a recursive dfs function. An additional HashMap or HashSets are used to keep track of 'visited' nodes/values.
> <br> **Note:** Try drawing the graph for some of these Q, it might help</a>
>
> - <a style="color:#000000">Loud and Rich - LeetCode Q851</a>
>
> - <a style="color:#000000">Course Schedule series - LeetCode Q207, LeetCode Q210, LeetCode Q1462 (good one)</a>
>
> - <a style="color:#000000">Find Eventual Safe States - LeetCode Q802</a>
>
> - <a style="color:#000000">Find All Possible Recipes from Given Supplies - LeetCode Q2115</a>
>
> - <a style="color:#000000">Minimum Height Trees - LeetCode Q310 (via BFS ~ Need to study but doesn't seem like an important Topo Sort Q)</a>
>
> - <a style="color:#000000">Longest Cycle in a Graph - LeetCode Q2360 **(If you can do this, you can do all above Topo Sort Qs)** </a>

<strong style="color:#1669f0">3. Merge Sort</strong>

> - <a style="color:#000000">Merge k Sorted Lists - LeetCode Q23</a>
>
> - <a style="color:#000000">Interval List Intersections - LeetCode Q986</a>

<strong style="color:#1669f0">4. Other Sorting Algorithms to study</strong>

> - <a style="color:#000000">Quick Sort, Heap Sort</a>
> - <a style="color:#000000">Bubble Sort, Insertion Sort, Selection Sort</a>

<br><br>
<h3 style="color:#1669f0">Dynamic Programming I</h3>

<strong style="color:#1669f0">1. Fibonacci Style DP Qs - Use variables to store values of previous state</strong>

> - <a style="color:#000000">Climbing Stairs - LeetCode Q70</a>
>
> - <a style="color:#000000"><mark style="background-color:#fffaa1"><strong style="color:#000000">Flip String to Monotone Increasing - LeetCode Q926</strong></mark></a>
>
> - <a style="color:#000000"><mark style="background-color:#fffaa1"><strong style="color:#000000">Max Product Subarray - LeetCode Q152</strong></mark></a>
>
> - <a style="color:#000000"><mark style="background-color:#fffaa1"><strong style="color:#000000">Count Sorted Vowel Strings - LeetCode Q1641</strong></mark></a>

<strong style="color:#1669f0">2. Iterate through the given array to solve the bigger problem</strong>

> - <a style="color:#000000">Minimum Time to Make Rope Colorful - LeetCode Q1578</a>
>
> - <a style="color:#000000"><mark style="background-color:#fffaa1"><strong style="color:#000000">Arithmetic Slices - LeetCode Q413</strong></mark></a>
>
> - <a style="color:#000000">Minimum Cost of Climbing Stairs - LeetCode Q746</a>
>
> - <a style="color:#000000">House Robber - LeetCode Q198</a>
>
> - <a style="color:#000000"><mark style="background-color:#fffaa1"><strong style="color:#000000">Count Substrings that differ by One Character - LeetCode Q1638</strong></mark></a>

<strong style="color:#1669f0">3. Following Qs can be solved with 1-D dp array and then can be optimized into just using variables</strong>

> - <a style="color:#000000">Decode Ways - LeetCode Q91</a>
>
> - <a style="color:#000000">Count Number of Teams - LeetCode Q1395</a>
<br> Use two 1-D arrays => n^2
>
> - <a style="color:#000000"><mark style="background-color:#fffaa1"><strong style="color:#000000">Best Time to Buy and Sell Stock with Cooldown - LeetCode Q309</strong></mark></a>

<strong style="color:#1669f0">4. Questions that are better done with a Bottom-Up approach using a 1-D dp array</strong>

> - <a style="color:#000000">Coin Change, Perfect Squares - LeetCode Q322, Q279</a>
<br>You can do one or the other
>
> - <a style="color:#000000">Longest Increasing Subsequence - LeetCode Q300</a>
>
> - <a style="color:#000000">Minimum Cost for Tickets - LeetCode Q983</a>
>
> - <a style="color:#000000">Number of Good Ways to Split a String - LeetCode Q1525</a>
>
> - <a style="color:#000000">Word Break - LeetCode Q139</a>
>
> - <a style="color:#000000">Fair Distribution of Cookies - LeetCode Q2305</a>
<br>dfs + dp
>
> - <a style="color:#000000"><mark style="background-color:#ff6373"><strong style="color:#000000">Partition Array for Max Sum - LeetCode Q1043</strong></mark></a>
>
> - <a style="color:#000000"><mark style="background-color:#fffaa1"><strong style="color:#000000">Partition Equal Subset Sum</strong></mark></a>

<strong style="color:#1669f0">5. Palindromic Qs</strong>

> - <a style="color:#000000">Longest Palindrome Substring - LeetCode Q5</a>
>
> - <a style="color:#000000">Palindromic Substrings - LeetCode Q647</a>

<br><br>

<h3 style="color:#1669f0">Dynamic Programming II</h3>

<strong style="color:#1669f0">1. Questions that are done with a 2-D dp array but can be optimized into just a 1-D dp array</strong>

> <a style="color:#1669f0">Self-Note: For all of the 2-D DP Qs, draw out the choices in a tree or 2-D grid and it'll be easier</a>
>
> - <a style="color:#000000">Unique Paths - LeetCode Q62</a>
>
> - <a style="color:#000000">Coin Change II - LeetCode Q518</a>

<strong style="color:#1669f0">2. Grid dp Qs can *sometimes be optimized into 1-D dp array</strong>

> - <a style="color:#000000">Minimum Falling Path Sum - LeetCode Q931</a>
> 
> - <a style="color:#000000"><mark style="background-color:#fffaa1"><strong style="color:#000000">Harder ver. Minimum Falling Path Sum II - LeetCode Q1289</strong></mark></a>
>
> - <a style="color:#000000">Minimum Path Cost in a Grid - LeetCode Q2304 + try Q2684</a>
>
> - <a style="color:#000000">Minimum Path Sum - LeetCode Q64 + try Q174</a>

<strong style="color:#1669f0">3. A typical 2-D dp Q</strong>

> - <a style="color:#000000">Interleaving String - LeetCode Q97</a>

<strong style="color:#1669f0">4. Subsequence type of Qs are better done with Bottom-Up (Iterating from the end of the string to start)</strong>

> - <a style="color:#000000">Longest Common Subsequence - LeetCode Q1143 (and others that are similar Q712, Q516)</a>
>
> - <a style="color:#000000">Distinct Subsequence - LeetCode Q115 + try Q1987</a>
>
> - <a style="color:#000000">Delete Operations for Two Strings - LeetCode Q583</a>
>
> - <a style="color:#000000">Edit Distance - LeetCode Q72</a>

<strong style="color:#1669f0">5. Memoization using hashmaps and strings as keys for Multi-D dp Qs</strong>

> - <a style="color:#000000">Target Sum - LeetCode Q494</a>
>
> - <a style="color:#000000"><mark style="background-color:#fffaa1"><strong style="color:#000000">Number of Dice Rolls with Target Sum - LeetCode Q1155</strong></mark></a>

<strong style="color:#1669f0">6. DFS + dp Qs</strong>

> - <a style="color:#000000">Longest Increasing Path in a Matrix - LeetCode Q329 (and others that are similar Q2328, try Q2713)</a>
<br><a style="color:#1669f0">Kind of like <strong>memoization</strong> - solve it like how you would using recursion, but store each result in dp\[\]\[\] or hashmap</a>
>
> - <a style="color:#000000"><mark style="background-color:#fffaa1"><strong style="color:#000000">Solving Questions with Brainpower - LeetCode Q2140</strong></mark></a>
<br> This Q is helpful for improving your understanding
>
> - <a style="color:#000000"><mark style="background-color:#fffaa1"><strong style="color:#000000">Burst Balloons - LeetCode Q312</strong></mark></a>
>
> - <a style="color:#000000"><mark style="background-color:#fffaa1"><strong style="color:#000000">Regex Matching, Wildcard Matching - LeetCode Q10, Q44</strong></mark></a>

<br><br>

<h3 style="color:#1669f0">Greedy</h3>

<strong style="color:#1669f0">1. Fractional Knapsack-like Q</strong>

> - <a style="color:#000000">Max. Units on a Truck - LeetCode Q1710</a>

<strong style="color:#1669f0">2. CoinChange-like Qs</strong>

> - <a style="color:#000000">Min. # of Ops to Convert Time - LeetCode Q2224</a>
>
> - <a style="color:#000000">Find the Min. # of Fibonacci Numbers whose sum is K - LeetCode Q1414</a>

<strong style="color:#1669f0">3. Greedy + HashMap Qs</strong>

> - <a style="color:#000000"><mark style="background-color:#fffaa1"><strong style="color:#000000">Partition Labels - LeetCode Q763</strong></mark></a>
>
> - <a style="color:#000000"><mark style="background-color:#fffaa1"><strong style="color:#000000">Task Scheduler - LeetCode Q621</strong></mark></a>

<strong style="color:#1669f0">4. Greedy w/ 2D Arrays</strong>

> - <a style="color:#000000">Max Increase to Keep City Skyline - LeetCode Q807</a>
>
> - <a style="color:#000000">Find Valid Matrix Given Row and Column Sums - LeetCode Q1605</a>
>
> - <a style="color:#000000">Largest Submatrix w/ Rearrangements - LeetCode Q1727</a>

<strong style="color:#1669f0">5. Intuitive Greedy Qs</strong>

> <a style="color:#1669f0">Greedy Qs are generally intuitive - you either get it or you don't. There is usually no specific patterns to look for. Try to solve them by looking at the sample test cases</a>
>
> - <a style="color:#000000">Gas Station - LeetCode Q134</a>
>
> - <a style="color:#000000">Hand of Straights - LeetCode Q846</a>
>
> - <a style="color:#000000">Two City Scheduling - LeetCode Q1029</a>
<br> Need to know how to use Collections.sort()
>
> - <a style="color:#000000">Max element after Decreasing and Rearranging - LeetCode Q1846</a>
>
> - <a style="color:#000000">Container With Most Water - LeetCode Q11</a>

<strong style="color:#1669f0">6. Classic Greedy</strong>

> - <a style="color:#1669f0" href="https://kannikalibreta.weebly.com/algorithms-ii.html#JobSequencing">Job Sequencing</a>
>
> - <a style="color:#1669f0" href="https://kannikalibreta.weebly.com/algorithms-ii.html#ActivitySelection">Activity Selection</a>
>
> - <a style="color:#1669f0" href="https://kannikalibreta.weebly.com/algorithms-ii.html#VertexCover">Vertex Cover</a>
>
> - <a style="color:#1669f0" href="https://kannikalibreta.weebly.com/algorithms-ii.html#Dijkstra">Dijkstra</a>
> - <a style="color:#000000">Design Graph with Shortest Path - LeetCode Q2642</a>
<br> A Typical Dijkstra problem but it just has a tiny twist to test your understanding
>
> - <a style="color:#1669f0" href="https://kannikalibreta.weebly.com/algorithms-ii.html#Prim">Prim's Algo to Find MST</a>
> - <a style="color:#000000">Min Cost to Connect All Points - LeetCode Q1584</a>
