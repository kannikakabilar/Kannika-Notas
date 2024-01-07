<h2 style="color:#1669f0">Data Structures II</h2>

<h3 style="color:#1669f0">Stacks</h3>

<strong style="color:#1669f0">Stacks are used for evaluating: parentheses; math expr; recursive function calls</strong>

> - <a style="color:#000000">LeetCode Q20</a>
>
> - <a style="color:#000000">LeetCode Q844</a>
>
> - <a style="color:#000000">LeetCode Q1021</a>
>
> - <a style="color:#000000">LeetCode Q1047</a>
>
> - <a style="color:#000000">LeetCode Q1441</a>
>
> - <a style="color:#000000">LeetCode Q1598</a>
>
> - <a style="color:#000000">LeetCode Q1614</a>
>
> - <a style="color:#000000">LeetCode Q946</a>
>
> - <a style="color:#000000">LeetCode Q1249/Q921</a>


<h3 style="color:#1669f0">Queues</h3>

> - <a style="color:#000000">Time Needed to But Tickets - LeetCode Q2073</a>
>
> - <mark style="background-color:#bbffa1">Weave pattern using queues - LeetCode Q950</mark><br>

    Hint-Note: Think in reverse-order
    => in the game you reveal a card and then put one card at the end of the deck
    => so when we are designing the deck => we add the highest-value card (deck array sorted in descending array) to the deck,
    then we remove a card from the bottom to and place it on top, and then we add the next highest-value card and so on..

<h3 style="color:#1669f0">Priority Queues OR Min/Max Heaps</h3>

In <span style="color:#fc6b03">Java</span>:
    
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

1\. &ensp; Describe how these simple trees work: <strong style="color:#1669f0">N-ary</strong> ; <strong style="color:#1669f0">Binary</strong> ; <strong style="color:#1669f0">BST</strong>

2\. &ensp; <strong style="color:#1669f0">AVL Trees</strong> are better for --------- , because the height <= log2(n) <br>
    - left-left case => ? <br>
    - left-right case => ? <br>

3\. &ensp; <strong style="color:#1669f0">Red-Black Trees</strong> are better for --------- and -------- <br>
    - What are the 4 rules for Red-Black Trees? <br>

4\. &ensp; <strong style="color:#1669f0">B-Tree</strong> <br>
    - Each node can have upto (how many?) values <br>
    - Each non-leaf node must have at least (how many?) children and atmost (how many?) children <br>
    - All leaves have the same ----- <br>

5\. &ensp; <strong style="color:#1669f0">Heaps (Min/Max Priority Queues)</strong> <br>
    - How do you insert in heaps? <br>
    - How do you delete in heaps? <br>

6\. &ensp; <strong style="color:#1669f0">Treaps</strong> are a mix of --- and ---- <br>
    - Each node stores 2 values (what are they - what kind of values?) <br>
    - How do you insert? And what happens after insertion? <br>

7\. &ensp; <strong style="color:#1669f0">Splay Trees</strong> are just like BST but perform AVL rotations each time an event occurs (what event?) and it updates the root node accordingly

<strong style="color:#1669f0">Practice Qs</strong>

> - <a style="color:#000000">LeetCode Q938</a>
>
> - <a style="color:#000000">LeetCode Q590 (How do you concatenate 2 arraylists in java?)</a>
>
> - <a style="color:#000000">LeetCode Q226</a>
>
> - <a style="color:#000000">LeetCode Q1022</a>
>
> - <a style="color:#000000">LeetCode Q1448</a>
>
> - <a style="color:#000000">LeetCode Q2265 (helper functions are sometimes needed when working with trees)</a>
>
> - <a style="color:#000000">LeetCode Q1026</a>

8\. &ensp; <mark style="background-color:#bbffa1">LeetCode Q894</mark>

    Hint-Note: Think about if there are n total nodes, 1 for root and i nodes for left-subtree, how much would the right subtree have?
    -use recursion to generate subtrees with i nodes for left-subtree and for each left-subtree loop through every possible right-subtree
    -store the list of subtrees of size-n-nodes into a hashmap

9\. &ensp; Balance a Binary Search Tree - LeetCode Q1382 (how do you get subarray of an arraylist?)

10\. &ensp; <mark style="background-color:#bbffa1">LeetCode Q2415</mark>

    Hint-Note: Think of the first few base cases. left-subtree needs to swap values with right subtree. 
    After that, the left-left-subtree will swap values with right-right-subtree and the left-right-subtree will swap values with right-left-subtree. 
    Ofcourse, pefrorm the swap only when the levels are odd.

> - <a style="color:#000000">LeetCode Q1325</a>
>
> - <mark style="background-color:#fffbb8"><strong>LeetCode Q1104</strong></mark>

    Hint-Note: Try drawing a normal (non-zigzag tree) and see how you can get the value of parent given value of child node 
    and then compare it by drawing the zigzag tree.
>
> - <a style="color:#000000">LeetCode Q208 (Trie), Q14</a>

<strong style="color:#1669f0">Postorder Qs</strong>

> - <mark style="background-color:#fffbb8"><strong>LeetCode Q1373</strong></mark>
> <br> Hint-Note: Perform a variation of post-order traversal to make it time efficient
>
> - <mark style="background-color:#fffbb8"><strong>Longest Univalue Path - LeetCode Q687</strong></mark>
>
> - <mark style="background-color:#fffbb8"><strong>Distribute Coins in Binary Tree - LeetCode Q979</strong></mark>
>
> - <mark style="background-color:#fffbb8"><strong>Binary Tree Maximum Path Sum - LeetCode Q124</strong></mark>

<br>

<h3 style="color:#1669f0">Graphs</h3>

> - <a style="color:#000000">LeetCode Q1557</a>
> <br>Hint-Note: A node that does not have any incoming edge can only be reached by itself => only count the node w/ zero incoming edges
>
> - <a style="color:#000000">LeetCode Q1615</a>
>
> - <a style="color:#000000">LeetCode Q2374</a>
>
> - <a style="color:#000000">LeetCode Q2508 (good practice Q)</a>
> <br>Hint-Note: The number of nodes with an odd-degree in the original graph should be either 0, 2, or 4. Try to work on each of these cases.
> <br>Hint-Note: Use Pair to store hashset of edges
>
> - <mark style="background-color:#fffbb8"><strong>(Need to study) Longest Cycle in a Graph - LeetCodeQ2360</strong></mark>

```java
Pair p1 = new Pair(1, 2);    // I think 'Pair' in java might be pass-by-value
```

<strong style="color:#1669f0">Define the following Graph Terms</strong>

    - order of a graph
    - size of a graph
    - null graph
    - complete graph
    - adjacency matrix
    - adjacency list

**Graph-Note:** When given a list of edges, it's very useful to store them in a HashMap

**! Data Structures Conclusive Note:** A search in a sorted collection, think binary search. Minimum # of steps, think BFS. Min/max K elements, think heap. Optimization, think DP. Parentheses, think stacks.

___________________________________________
