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

___________________________________________


<h3 style="color:#0303ad">Dynamic Programming</h3>   
-   for repetitive subproblems

### Terms
- **Memoization**: Top-down approach, recursive, uses dictionaries <br>
- **Tabulation**: Bottom-up approach, iterative, uses 2-D array

<h4>Sample Qs</h4>


___________________________________________


<h3 style="color:#0303ad">Greedy Algorithm</h3>
- Requirements: choice property, optimal substructure, no backtracking, not always optimal

<h4>Sample Qs</h4>


___________________________________________


<h3 style="color:#0303ad">Backtracking</h3>
- better than naive because eliminates an option when it doesn't work instead of naively checking validity at the end

<h4>Sample Qs</h4>


___________________________________________





