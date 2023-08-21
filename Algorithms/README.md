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

graph = {'0': set(['1', '2']),
         '1': set(['0', '3', '4']),
         '2': set(['0']),
         '3': set(['1']),
         '4': set(['2', '3'])}

dfs(graph, '0')
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
-   break down problem into smaller different subproblems

<h4>Sample Qs</h4>


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





