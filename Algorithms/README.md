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

**Karatsuba Algorithm**
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


___________________________________________


<h3 style="color:#0303ad">Backtracking</h3>
- better than naive because eliminates an option when it doesn't work instead of naively checking validity at the end

<h4>Sample Qs</h4>


___________________________________________





