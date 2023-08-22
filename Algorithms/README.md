<h1 style="color:#0303ad">Algorithms</h1>

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

<h3 style="color:#0303ad">Recursive Algorithms</h3>

<h4>Sample Qs</h4>

**Depth First Search**
```python
def dfs(graph, start, visited=None):
    if visited is None:
        visited = set()
    visited.add(start)

    print(start)

    for child in graph[start]:
​        if not(child in visited):
            dfs(graph, child, visited)
    return visited

```

**Breadth First Search**
```python
def bfs(graph, root):

    visited = set()
    queue = []

    visited.add(root)
    print(str(root) + " ", end="")

    for child in graph[root]:
        visited.add(child)
        queue.append(child)

    while len(queue) != 0:

        vertex = queue.pop(0)
        print(str(vertex) + " ", end="")

        for child in graph[vertex]:
            if child not in visited:
                visited.add(child)
                queue.append(child)

```

**Tower of Hanoi**
```python
def hanoi(n , src, dest, aux):
    if n == 1:
        print("Move disk 1 from "+src+ " to "+dest)
    else:
        hanoi(n-1, src, aux, dest)
        print("Move disk "+ n +" from " +src+" to "+dest)
        hanoi(n-1, aux, dest, src)

# Driver code
n = 4
TowerOfHanoi(n, 'A', 'C', 'B')
```

**Greatest Common Divisor**
```python
def gcf(a, b):
    if a == 0 or b == 0:
        return a + b
    elif a == b:
        return a
    elif a > b:
        return gcf(a%b, b)
    else:
        return gcf(a, b%a)
```
___________________________________________


<h3 style="color:#0303ad">Divide & Conquer</h3>
- break down problem into smaller different subproblems

<h4>Sample Qs</h4>

**Merge Sort**
```python
def mergeSort(array):

    if len(array) == 0:
         return array  
    m = len(array) // 2
    L = array[:m]
    R = array[m:]
    
    mergeSort(L)
    mergeSort(R)
    
    # merge
    i = j = k = 0
    while i < len(L) and j < len(R):
         if L[i] < R[j]:
             array[k] = L[i]
             i += 1
         else:
             array[k] = R[j]
             j += 1
         k += 1
    
    while i < len(L):
         array[k] = L[i]
         i += 1
         k += 1
    while j < len(R):
         array[k] = R[j]
         j += 1
         k += 1
```

**Quick Sort**
```python
def quickSort(array, low, high):
    if low < high:

        piv = partition(array, low, high)
        quickSort(array, low, piv - 1)
        quickSort(array, piv + 1, high)

def partition(array, low, high):

    pivot = array[high]

    i = low - 1

    for j in range(low, high):
        if array[j] <= pivot:
            i = i + 1
            (array[i], array[j]) = (array[j], array[i])

    (array[i + 1], array[high]) = (array[high], array[i + 1])
    return i + 1
```

| Merge Sort | Quick Sort |
|------------|------------|
|- it is parallelizable | - average-case runtime is faster than mergesort |
|- works better with linked list | - better cache performance due to its localized and sequential memory access pattern during partitioning |
|- external sorting requirements (sorting large datasets that don't fit in memory), Merge Sort is often used | - partitioning process has a lower overhead compared to merging process |
|- preserves the original order of equal value elements that quicksort does not 

<br>

**Karatsuba Algorithm** <br>

| Elements |
|-----------------|
| a  =  xH  *  yH
| d  =  xL  *  yL
| e  =  (xH  +  xL)  *  (yH  +  yL)  -  a  -  d
| xy  =  (a * (b^n))  +  (e  *  (b^(n/2)​))  +  d

```python
from math import ceil, floor

def karatsuba(x,y):
   
    if x < 10 and y < 10: # in other words, if x and y are single digits
        return x*y

    n = max(len(str(x)), len(str(y)))
    m = ceil(n/2)   

    x_H  = floor(x / 10**m)
    x_L = x % (10**m)

    y_H = floor(y / 10**m)
    y_L = y % (10**m)

    a = karatsuba(x_H,y_H)
    d = karatsuba(x_L,y_L)
    e = karatsuba(x_H + x_L, y_H + y_L) - a - d

    return int(a*(10**(m*2)) + e*(10**m) + d)
```

**Find MaxMin (DAC)**
- Naive method would perform 2*(n-1) comparisons but DAC takes (3*n/2)-2 comparisons

```python
def MaxMinDAC (arr, low, high):
    if low == high:
        return arr[low], arr[low]
    elif high - low == 1:
        return max(arr[low], arr[high]), min(arr[low], arr[high])
    else:
        mid = (low + high)//2
        L_max, L_min = MaxMinDAC (arr, low, mid)
        R_max, R_min = MaxMinDAC (arr, mid+1, high)

        return max(L_max, R_max), min(L_min, R_min)
```

**Preorder List To BST**
```python
def bstFromPreorder(self, preorder: List[int]) -> Optional[TreeNode]:
    if len(preorder) == 0:
        return None
    node = preorder.pop(0)
    root = TreeNode(node)
    l = []
    r = []

    for val in preorder:
        if val < node:
            l.append(val)
        else:
            r.append(val)

    root.left = self.bstFromPreorder(l)
    root.right =  self.bstFromPreorder(r)
    return root
```
**Reverse String**
```python
def reverseString(self, s: List[str]) -> None:
    # Modify s in-place, space complexity = O(1)
    low = 0 
    high = len(s)-1
    while low < high:
        s[low], s[high] = s[high], s[low]
        low += 1
        high -= 1
```
**Find a pair that sums to target in a Sorted Array**
```python
def twoSum(self, numbers: List[int], target: int) -> List[int]:
    if len(numbers) == 2:
        return [0, 1]
    
    low = 0
    high = len(numbers) - 1
    
    while high > low:        
        if numbers[low] + numbers[high] == target:
            return [low, high]
        
        elif numbers[low] + numbers[high] < target:
            low += 1
            
        elif numbers[low] + numbers[high] > target:
            high -= 1
```
**Swap values w/o tmp var**
```python
a = a + b
b = a - b    # => (a + b) - b
a = a - b    # => (a + b) - a

​(*using xor)
x = x ^ y
y = x ^ y
x = x ^ y
```
**List Primes**
-  In order to check if a given number, n is prime <br>
  - You just need to check if n can be divided by any num from 2 to sqrt(n) <br>
&ensp;&ensp;&ensp;&ensp;  because for every a * b = n => a <= sqrt(n) and b >= sqrt(n) <br>

```python
def listPrimes(n):
  lst = []
  for i in range(n+1):
    if i == 0 or i == 1:
      lst.append(False)
    else:
      lst.append(True)
      
  i = 2
  j = 3
  nxt = n+1
  while i < (n+1):
    for j in range(i+1, n+1):
      if i != j and j % i == 0:
        lst[j] = False
      else:
        if nxt > j:
          nxt = j
    i = nxt
    nxt = n+1
      
  for k in range(len(lst)):
    if lst[k]:
      print(k)
```

<h3 style="color:#0303ad">Sorting Algos</h3>

**Heap Sort**
```python
def heapify(arr, n, i):
    largest = i
    left_child = 2 * i + 1
    right_child = 2 * i + 2

    if left_child < n and arr[left_child] > arr[largest]:
        largest = left_child

    if right_child < n and arr[right_child] > arr[largest]:
        largest = right_child

    if largest != i:
        arr[i], arr[largest] = arr[largest], arr[i]
        heapify(arr, n, largest)

def heap_sort(arr):
    n = len(arr)

    # Build a max heap - Start from the last non-leaf node and heapify as the indices go up
    for i in range(n // 2 - 1, -1, -1):
        heapify(arr, n, i)

    # Extract elements from the heap one by one
    for i in range(n - 1, 0, -1):
        arr[0], arr[i] = arr[i], arr[0]  # Swap the root with the last element
        heapify(arr, i, 0)  # Heapify the reduced heap
```

**Bubble Sort**
```python
def bubbleSort(arr):
    n = len(arr)
    for i in range(n):
        # Last i elements are already in place
        for j in range(0, n-i-1):
            if arr[j] > arr[j+1]:
                arr[j], arr[j+1] = arr[j+1], arr[j]
```

| Cons | Pros |
|------|------|
| O(n^2) even on average case |  w/ Parallel processing => BubbleSort sorts in O(n) time better than Insertion and Selection sorts
| performs too many swaps/writes
| O(n^2) even on partially sorted list

**Insertion Sort**
```python
def insertionSort(arr):
    for i in range(1, len(arr)): 
        key = arr[i] 
        # Keep swapping curr element(key) in the sorted section until curr element is put in the correct place
        j = i-1
        while j >= 0 and key < arr[j] :
                arr[j + 1] = arr[j]
                j -= 1
        arr[j + 1] = key
```

**Shell Sort**
```python
def shell_sort(arr):
    n = len(arr)
    gap = n // 2  

    while gap > 0:
        for i in range(gap, n):
            temp = arr[i]
            j = i

            while j >= gap and arr[j - gap] > temp:
                arr[j] = arr[j - gap]
                j -= gap

            arr[j] = temp

        gap //= 2  
```

**Selection Sort**
```python
import sys

def selectionSort(A): 
    for i in range(len(A)):
      
        # Find the minimum element from the unsorted part
        min_idx = i
        for j in range(i+1, len(A)):
            if A[min_idx] > A[j]:
                min_idx = j
                 
        # Swap the found minimum element with end of sorted part     
        A[i], A[min_idx] = A[min_idx], A[i]
```

**Topological Sort**
```python
from collections import defaultdict

class Graph:
    def __init__(self, vertices):
        ​self.graph = defaultdict(list) # dictionary containing adjacency List
        self.V = vertices # No. of vertices

    def addEdge(self, u, v):
        self.graph[u].append(v)

    # helper function
    def topologicalSortUtil(self, v, visited, stack):      
        visited[v] = True
        # Recur for all the vertices adjacent to this vertex
        for i in self.graph[v]:
            if visited[i] == False:
                self.topologicalSortUtil(i, visited, stack)
        # Push child vertices before parent
        stack.append(v)

    # main function 
    def topologicalSort(self):
        # Initially mark all the vertices as not visited
        visited = [False] * self.V
        stack = []

        # Get all vertices from graph added to stack
        for i in range(self.V):
            if visited[i] == False:
                self.topologicalSortUtil(i, visited, stack)
        print(stack[::-1]) # return list in REVERSE order
```

___________________________________________


<h3 style="color:#0303ad">Dynamic Programming</h3>   
-   for repetitive subproblems

### Terms
- **Memoization**: Top-down approach, recursive, uses dictionaries <br>
- **Tabulation**: Bottom-up approach, iterative, uses 2-D array

<h4>Sample Qs</h4>

**Fibonacci Term**
```python
def fib(self, n: int) -> int:
    if n == 0:
        return 0
    elif n == 1:
        return 1
    else:
        nm1 = 1
        nm2 = 1
        
        for i in range(2, n):
            tmp = nm2
            nm2 = nm2 + nm1
            nm1 = tmp
            
        return nm2
```

**Is Sub Sequence?**
```python
def isSubsequence(self, s: str, t: str) -> bool:
    m = len(t)
    n = len(s)
    
    if n == 0:
        return True
    
    j = 0
    for i in range(m):
        if s[j] == t[i]:
            j += 1
        if j == n:
            return True
            
    return j == n
```

**Counting Binary Bits**
```python
def countBits(self, n: int) -> List[int]:
    if n<=1:
        if n==0:
            return [0]
        else:
            return [0,1]
                
        dp = [0]*(n+1)

        dp[1] = 1
        
        dp[2] = 1

        for i in range(3,n+1):
            if i%2==0:
                val = i//2
                dp[i] = dp[val]
                # val its basically i<<2
            else:
                dp[i] = dp[i-1]+1
        return dp
```

**Longest Common Sequence**
- Memoized
```python
def lcs(X, Y, m, n, dp):

    if (m == 0 or n == 0):
        return 0

    if (dp[m][n] != -1):
        return dp[m][n]

    if X[m - 1] == Y[n - 1]:
        dp[m][n] = 1 + lcs(X, Y, m - 1, n - 1, dp)
        return dp[m][n]

    dp[m][n] = max(lcs(X, Y, m, n - 1, dp),lcs(X, Y, m - 1, n, dp))
    return dp[m][n]
```
- Tabulated
```python
def lcs(X , Y):
    m = len(X)
    n = len(Y)
 
    # declaring the array for storing the dp values
    L = [[None]*(n+1) for i in range(m+1)]
 
    for i in range(m+1):
        for j in range(n+1):
            if i == 0 or j == 0 :
                L[i][j] = 0
            elif X[i-1] == Y[j-1]:
                L[i][j] = L[i-1][j-1]+1
            else:
                L[i][j] = max(L[i-1][j] , L[i][j-1])
 
    return L[m][n]
```

**Subset Sum**
- Memoized
```python
def subsetSum(A, n, k, lookup):

    if k == 0:
        return True

    if n <= 0 or k < 0:
        return False

    key = (n, k)
 
    if key not in lookup:
        # Case 1. Include the current item 
        include = subsetSum(A, n - 1, k - A[n], lookup)

        # Case 2. Exclude the current item 
        exclude = subsetSum(A, n - 1, k, lookup)
 
        # Assign true if we get subset by including or excluding the current item
        lookup[key] = include or exclude
 
    return lookup[key]
```
- Tabulated
```python
def isSubsetSum(set, n, sum):
      
    subset = [[False] * (sum + 1) for i in range(n + 1)]
      
    for i in range(n + 1):
        subset[i][0] = True
          
    for i in range(1, sum + 1):
         subset[0][i]= False
              
    for i in range(1, n + 1):
        for j in range(1, sum + 1):

            if j<set[i-1]:
                subset[i][j] = subset[i-1][j]

            else:
                subset[i][j] = (subset[i-1][j] or 
                                subset[i - 1][j-set[i-1]])
      
    return subset[n][sum]
```

**0/1 Knapsack Problem**
```python
def knapSack(C, wt, val, n):
    K = [[0 for j in range(C + 1)] for i in range(n + 1)]

    for i in range(n + 1):
        for j in range(C + 1):
            if i == 0 or j == 0:
                K[i][j] = 0
            if j < wt[i-1]:
                K[i][j] = K[i-1][j]   
            else:
                K[i][j] = max(val[i-1]+ K[i-1][j-wt[i-1]], K[i-1][j])

    ​return K[n][C]
```

**Weighted Job Scheduling**
```python
class Job:
    def __init__(self, start, finish, weight):
        self.start = start
        self.finish = finish
        self.weight = weight

def find_max_weight(jobs):
    # Sort jobs based on finish times
    jobs.sort(key=lambda job: job.finish)

    n = len(jobs)
    dp = [0] * n

    for i in range(n):
        dp[i] = jobs[i].weight

    for i in range(1, n):
        for j in range(i):
            if jobs[j].finish <= jobs[i].start:
                # for each job, check if including the 'j' jobs before it profits more than just completing the ith job
                dp[i] = max(dp[i], dp[j] + jobs[i].weight)    

    return max(dp)

# Example usage
jobs = [Job(1, 3, 5), Job(2, 5, 6), Job(4, 6, 5), Job(6, 7, 4), Job(5, 8, 11), Job(7, 9, 2)]
print("Maximum Weight:", find_max_weight(jobs))
```

**Floyd Warshall**
```python
INF = float('inf')

def floyd_warshall(graph):
    n = len(graph)
    dist = [[0 if i == j else INF for j in range(n)] for i in range(n)]

    for u in range(n):
        for v, weight in graph[u]:
            dist[u][v] = weight

    for k in range(n):
        for i in range(n):
            for j in range(n):
                dist[i][j] = min(dist[i][j], dist[i][k] + dist[k][j])

    return dist
```

**Bellman Ford**
```python
def bellmanFord(V, edges, src):    
    
    # Step 1 - Initialization
    INF = 999999999
    dis = [INF for x in range(V)]
    
    dis[src] = 0 # Since we're already at src
    
    # Step 2 - For V-1 times, traverse over, all the edges and checking if a shorter path between any edge u to v is possible.     
    for _ in range(V-1): 
        for j in range(len(edges)): 
            s = edges[j][0]      # Source vertex
            d = edges[j][1]      # destination vertex
            wt = edges[j][2]   # weight of edge from u to v
            
            # Update dis[v] from u if it can be reached with lower weight
            if(dis[s] != INF and dis[s] + wt < dis[d]):
                dis[d] = dis[s] + wt
                
    # Step 3 - Checking for negative edge weight cycle
    for i in range(len(edges)):
        s = edges[i][0]
        d = edges[i][1]
        wt = edges[i][2]

        if(dis[s] != INF and dis[s] + wt < dis[d]):
            return []

    return dis 
```
___________________________________________


<h3 style="color:#0303ad">Greedy Algorithm</h3>
- Requirements: choice property, optimal substructure, no backtracking, not always optimal

<h4>Sample Qs</h4>

**Coin Change**
- Always choose the greatest coin value that is lower or equal to the target value
- Repeat the above step until the target value is reached

**Huffman Coding**
1) Create a dictionary that stores the frequency of each char in the given string <br>
2) Build a Min Heap based on the frequency <br>
3) Pop smallest frequency and initialize it as a node <br>
4) Pop next smallest node and set it as a right node and prev_node as left child and root node = sum_of_right_&_left_nodes <br>
5) Perform above step until Heap becomes empty to complete building the Huffman Tree <br>
6) Each leaf of the Huffman Tree represents a char, traverse through Huffman Tree to build binary string for each char <br>
    - left_nodes => append '0' | right_nodes => append '1' <br>
7) Use binary rep of each char to compress original string <br>

**Dijkstra's**
```python
import math

graph = {'a':{'b':5,'c':2},
        'b':{'a':5,'c':7,'d':8},     
        'c':{'a':2,'b':7,'d':4,'e':8},
        'd':{'b':8,'c':4,'e':6, 'f':4},
        'e':{'c':8,'d':6,'f':3}, 
        'f':{'e':3, 'd':4}}

source = 'a'
destination = 'f'

unvisited = graph  
shortest_distances = {}
route = [] 
path_nodes = {}

# set the distance of all nodes to inf and src to 0
for nodes in unvisited:
   shortest_distances[nodes] = math.inf
shortest_distances[source] = 0

while(unvisited):
       min_node = None
       # for each node find the node that is unvisited and can be reached with the lowest weight
       for current_node in unvisited: 
           if min_node is None:
               min_node = current_node        
           elif shortest_distances[min_node] > shortest_distances[current_node]:
               min_node = current_node

       # for each node connected to the current min_node, update its distance if it can be reached through curr min_node with lower weight
       for node,value in unvisited[min_node].items():
           if value + shortest_distances[min_node] < shortest_distances[node]:  
               shortest_distances[node] = value + shortest_distances[min_node]
               path_nodes[node] = min_node

       # remove the curr min_node from unvisited
       unvisited.pop(min_node)
```

**Kruskal's**

​Given a graph find the MST <br>
1) Sort all the edges from low weight to high <br>
2) Take the edge with the lowest weight and add it to the spanning tree. If adding the edge created a cycle, then reject this edge. <br>
3) Keep adding edges until we reach all vertices. <br>

```python
class DisjointSet:
    def __init__(self, n):
        self.parent = list(range(n))  # Initialize parent pointers
        self.rank = [0] * n  # Initialize ranks

    # The purpose of this code is to find the representative (also known as the main root) of a given element x in the disjoint-set.
    def find(self, x):
        if self.parent[x] != x:
            self.parent[x] = self.find(self.parent[x])  # Path compression
        return self.parent[x]
    
    # Union: merges 2 disjoint sets - finds the least weighted edge that connects the 2 disjoint set
    def union(self, x, y):
        root_x = self.find(x)
        root_y = self.find(y)
        
        if root_x != root_y:
            if self.rank[root_x] > self.rank[root_y]:
                self.parent[root_y] = root_x  # Attach smaller rank tree under root of higher rank tree
            else:
                self.parent[root_x] = root_y
                if self.rank[root_x] == self.rank[root_y]:
                    self.rank[root_y] += 1

def kruskal(graph, n):
    graph.sort(key=lambda edge: edge[2])  # Sort edges by weight - lowest to highest
    disjoint_set = DisjointSet(n)  # Initialize disjoint-set data structure
    minimum_spanning_tree = []  # To store the selected edges of the MST

    # for each edge in graph from lowest to highest - 
    for u, v, weight in graph:
        # This condition checks whether adding the current edge (u, v) to the MST would create a cycle. It does this by checking if the parent (root) of vertex u is different from the parent (root) of vertex v in the disjoint-set data structure. If they have different parents, it means that adding this edge won't form a cycle.
        if disjoint_set.find(u) != disjoint_set.find(v):
            disjoint_set.union(u, v)  # Union two sets if they are not connected
            minimum_spanning_tree.append((u, v, weight))
    
    return minimum_spanning_tree
```

**Prim's**

Given a graph find the MST <br>
1) Initialize the minimum spanning tree with a vertex chosen at random and add it to the tree. <br>
2) Find an minimum weight edges that connect the tree to a new vertices (not already in the tree) <br>
3) Keep repeating step 2 until we get a minimum spanning tree (when all vertices become part of the tree) <br>

```python
from heapq import heappop, heappush

def prim(graph, start):
    n = len(graph)
    visited = [False] * n
    min_heap = [(0, start)]  # Heap of (weight, vertex) pairs
    minimum_spanning_tree = []

    while min_heap:
        weight, node = heappop(min_heap)
        if visited[node]:
            continue
        visited[node] = True

        for neighbor, edge_weight in graph[node]:
            if not visited[neighbor]:
                heappush(min_heap, (edge_weight, neighbor))
        
        if node != start:  # Skip the start node
            minimum_spanning_tree.append((node, weight))

    return minimum_spanning_tree
```

**Fractional Knapsack**
```python
class Item:
    def __init__(self, value, weight):
        self.value = value
        self.weight = weight

def fractionalKnapsack(W, arr):

 # sort items based on ratio => highest-value per weight to lowest
    arr.sort(key=lambda x: (x.value/x.weight), reverse=True)

    finalvalue = 0.0

    for item in arr:
        # If adding Item won't overflow, add it completely
        if item.weight <= W:
            W -= item.weight
            finalvalue += item.value
        # If we can't add current Item, add fractional part of it
        else:
           finalvalue += item.value * W / item.weight
           break

    return finalvalue
```

**Traveling Salesman**
```python
def tsp_greedy(graph, start):
    n = len(graph)
    visited = [False] * n       # keep track of the visited nodes
    tour = [start]                 # order of nodes visited
    total_distance = 0
    current_city = start

    for _ in range(n - 1):    # loop through until every n-1 nodes other than start node is visited
        nearest_city = None
        min_distance = float('inf')

        # loop through all connected nodes to the current node and find the node that can be reached with the least distance
        for next_city in range(n):     
            if not visited[next_city] and graph[current_city][next_city] < min_distance:
                nearest_city = next_city
                min_distance = graph[current_city][next_city]

        tour.append(nearest_city)
        total_distance += min_distance
        visited[nearest_city] = True.      # mark next city as visited for hamiltonian cycle or mark current city as visited for path
        current_city = nearest_city       # set next city in tour to the least distance node

    # Return to the starting city
    tour.append(start)
    total_distance += graph[current_city][start]

    return tour, total_distance
```

**Activity Selection**
```python
def activity_selection(activities):
    n = len(activities)
    activities.sort(key=lambda x: x[1])  # Sort activities by finish time
    selected_activities = [activities[0]]
    
    last_selected = 0  # Index of the last selected activity
    
    for i in range(1, n):    # for each of the next selected activities check if its start time is after finish time of current activity
        if activities[i][0] >= activities[last_selected][1]:
            selected_activities.append(activities[i])
            last_selected = i
    
    return selected_activities
```

**Job Sequencing**
```python
# t = no. of jobs to schedule
def printJobScheduling(arr, t):

    n = len(arr)

    # Sort all jobs according to decreasing order of profit
    for i in range(n):
        for j in range(n - 1 - i):
            if arr[j][2] < arr[j + 1][2]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]

    result = [False] * t    # To keep track of free time slots

    job = ['-1'] * t    # To store result (Sequence of jobs)

    # Iterate through all given jobs
    for i in range(len(arr)):
        # Find a free slot for this job
        # (Note that we start from the last possible slot)
        for j in range(min(t - 1, arr[i][1] - 1), -1, -1):
            # Free slot found
            if result[j] is False:
                result[j] = True
                job[j] = arr[i][0]
                break

    print(job)    # print the sequence
```

**Ford Fulkerson**
```python
from collections import defaultdict

class Graph:

    def __init__(self, graph):
        self.graph = graph # residual graph
        self. ROW = len(graph)
        # self.COL = len(gr[0])

     '''Returns true if there is a path from source 's' to sink 't' in
     residual graph. Also fills parent[] to store the path '''
    def BFS(self, s, t, parent):

        # Mark all the vertices as not visited
        visited = [False]*(self.ROW)
        # Create a queue for BFS
        queue = []
        # Mark the source node as visited and enqueue it
        queue.append(s)
        visited[s] = True

        # Standard BFS Loop
        while queue:

            # Dequeue a vertex from queue and print it
            u = queue.pop(0)

            # Get all adjacent vertices of the dequeued vertex u
            # If a adjacent has not been visited, then mark it visited and enqueue it
            for ind, val in enumerate(self.graph[u]):
                if visited[ind] == False and val > 0:
                # If we find a connection to the sink node, then there is no point in BFS anymore
                # We just have to set its parent and can return true
                    queue.append(ind)
                    visited[ind] = True
                    parent[ind] = u
                    if ind == t:
                        return True

        # We didn't reach sink in BFS starting from source, so return false
        return False
   
    # Returns the maximum flow from s to t in the given graph
    def FordFulkerson(self, source, sink):

        # This array is filled by BFS and to store path
        parent = [-1]*(self.ROW)

        max_flow = 0 # There is no flow initially

        # Augment the flow while there is path from source to sink
        ​while self.BFS(source, sink, parent) :

        # Find minimum residual capacity of the edges along the path filled by BFS.
        # Or we can say find the maximum flow through the path found.
            path_flow = float("Inf")
            s = sink
            while(s != source):
                path_flow = min (path_flow, self.graph[parent[s]][s])
                s = parent[s]

            # Add path flow to overall flow
            max_flow += path_flow

            # update residual capacities of the edges and reverse edges along the path
            v = sink
            while(v != source):
                u = parent[v]
                self.graph[u][v] -= path_flow
                self.graph[v][u] += path_flow
                v = parent[v]

        ​return max_flow
```
___________________________________________


<h3 style="color:#0303ad">Backtracking</h3>
- better than naive because eliminates an option when it doesn't work instead of naively checking validity at the end

<h4>Sample Qs</h4>


___________________________________________





