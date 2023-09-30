<h1 style="color:#1669f0">Data Structures 2</h1>

<h3 style="color:#5c91fa">Stacks</h3>   -   used for evaluating parentheses, math expr and recursive function calls

#### Sample Stack Qs

**Valid Parentheses**
```python
def validParentheses(s: str) -> bool:
    d = {'(':')', '{':'}','[':']'}
    stack = []
    for i in s:
        if i in d:  
            stack.append(i)
        elif len(stack) == 0 or d[stack.pop()] != i:  
            return False
    return len(stack) == 0 
```
**Inorder Traversal**
```python
def inorderTraversal(root: TreeNode) -> List[int]:
        
    lst = []
    if root is None:
        return lst
    if root.left is None:
        lst.append(root.val)
        lst += inorderTraversal(root.right)
    else:
        lst += inorderTraversal(root.left)
        lst.append(root.val)
        lst += inorderTraversal(root.right)
        
    return lst
```
**Backspace Compare**
```python
def backspaceCompare(s: str, t: str) -> bool:
    s_lst = []
    t_lst = []

    for i in s:
        if i == "#" and len(s_lst) > 0:
            s_lst.pop()
        elif i == "#" and len(s_lst) == 0:
            continue
        else:
            s_lst.append(i)

    for i in t:
        if i == "#" and len(t_lst) > 0:
            t_lst.pop()
        elif i == "#" and len(t_lst) == 0:
            continue
        else:
            t_lst.append(i)

    if len(t_lst) != len(s_lst):
        return False
    for i in range(len(s_lst)):
        if s_lst[i] != t_lst[i]:
            return False
        
    return True
```
**Remove Outer Parentheses**
```python
def removeOuterParentheses(s: str) -> str:
    res = []
    curOpen = 0
    for c in s:
        if c == '(':
            if curOpen:
                res.append(c)
            curOpen += 1
        else:
            curOpen -= 1
            if curOpen:
                res.append(c)
    
    return ''.join(res)
```
**Remove Consecutive Duplicates**
```python
def removeConsecutiveDuplicates(s: str) -> str:
    lst = []
    
    for i in range(len(s)):
        if len(lst) > 0 and s[i] == lst[-1]:
            lst.pop()
        else:
            lst.append(s[i])
    return ''.join(lst)
```
**Build Array**
```python
def buildArray(target: List[int], n: int) -> List[str]:
    lst = []
    for i in range(1, n+1):
        if i in target:
            lst.append("Push")
        elif i < target[-1]:
            
            lst.append("Push")
            lst.append("Pop")
            
    return lst
```
**Folder Operations**
```python
def fldOperations(logs: List[str]) -> int:
    level = 0
    for i in logs:
        if i == "../" and level > 0:
            level -= 1
        elif i != "../" and i != "./":
            level += 1
    return level
```
**Max Depth of Brackets**
```python
def maxDepth(s: str) -> int:
    d = 0
    high = 0
    for i in s:
        if i == "(":
            d += 1
            if d > high:
                high = d
        if i == ")":
            d -= 1
    return high
```
___________________________________________

<h3 style="color:#5c91fa">Queues  </h3> 

**Time Required to Wait in Circular Line**
```python
def timeRequiredToBuy(self, tickets: List[int], k: int) -> int:
    time = 0
    i = 0
    tmp = 0
    
    while tickets[k] != 0:
        if tickets[i] > 0:
            tickets[i] = tickets[i] - 1
            #tickets.pop(0)
            #tickets.append(tmp)
            time += 1
            
            
        i = (i + 1) % len(tickets)
        
    return time
```
___________________________________________

<h3 style="color:#5c91fa">Trees</h3>

### Sample Tree Implementation Explanations

  - **N-ary**: each node can have upto N children
  - **Binary**: each node can have upto 2 children
  - **BST**: left_child.val < root.val < right_child.val<br><br>

  - **AVL**: better for searching, height <= log2(n)<br>
        types of rotations<br>
          &ensp;&ensp;left-left case => right rotation<br>
          &ensp;&ensp;left-right case => left rotate, right rotate<br>
          &ensp;&ensp;right-left case => right rotate, left rotate<br>
          &ensp;&ensp;right-right case => left rotation<br><br>

  - **Red-Black**: better for insertion and deletion<br>
      rules<br>
        &ensp;&ensp;1) root is always black<br>
        &ensp;&ensp;2) all leaves are black<br>
        &ensp;&ensp;3) all leaves have same # of black ancestors<br>
        &ensp;&ensp;4) all children of red nodes are black<br><br>

  - **B-Tree**<br>
      notes<br>
        &ensp;&ensp;- each node can have upto n-1 values<br>
        &ensp;&ensp;- each node can have atmost n children and at least n/2 children<br>
        &ensp;&ensp;- all leaves have the same depth<br><br>

  - **Heap**<br>
      &ensp;&ensp;- Max/Min Heap: all children node values are less/higher than parent<br>
      &ensp;&ensp;- Insertion: insert in the next according space and performing swapping with parent<br>
      &ensp;&ensp;- Deletion: swap node-to-be-deleted with last node, delete last node, perform swapping with the switched node<br>

    - **Treap**: mix of BST and and Heap <br>
        &ensp;&ensp;- each node stores 2 values (key=value_inserted, priority=random_num)<br>
        &ensp;&ensp;- insert according key which follows BST, then perform AVL rotations to maintain priority which follows Heap<br><br>
      
  - **Splay**: just like BST but perform AVL rotations each time an element is accessed and make it the root node

___________________________________________


<h3 style="color:#5c91fa">Graphs</h3>

### Terms
  - **order of a graph** = # of vertices in graph
  - **size of a graph** = # of edges of a graph
  - **null graph** = 0 edges in graph (but may have vertices)
  - **complete graph** = has edges with all combination of vertices
  - **adjacency matrix** = nxn matrix where matrix[i][j] indicates an edge/edge_weight between vertex i and j
  - **adjacency list** = key-value table where there's 1 key for each vertex and a list with vertices that the key vertex connects to

___________________________________________







A search in a sorted collection, think binary search. Minimum # of steps, think BFS. Min/max K elements, think heap. Optimization, think DP. Parentheses, think stacks. 

