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
**Push and Pop Sequence of Stack**
Given an array called pushed which contains the order in which elements were pushed into a stack and another array called popped which contains the order in which the elements were popped from the stack. Return true if this could have been the result of a sequence of push and pop operations on an initially empty stack.

```javascript
var validateStackSequences = function(pushed, popped) {
    let stack = [];
    let j = 0;
    for(let i=0; i<pushed.length; i++){
        stack.push(pushed[i]);
        while(stack.length>0 && popped[j]==stack[stack.length-1]){
            stack.pop();
            j++;
        }
    }
    
    return stack.length==0;
};
```

**Remove Minimal Parentheses**
Remove the minimum amount of parentheses to make it a valid parentheses string

```javascript
var minRemoveToMakeValid = function(s) {
    let count = 0;
    let news = s
    for(let i=0; i<s.length; i++){
        if(count>0 && s[i] == ")"){
            count--;
        }else if(s[i]==")"){
            news = news.replace(")", "");
        }else if(s[i]=="("){
            count++;
        }
    }

    news = news.split("").reverse().join("");
    while(count != 0){
        news = news.replace("(", "");
        count--;
    }
    return news.split("").reverse().join("");
    
};
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

**Creating a weave pattern using Queues**
Given an integer array called 'deck' change the order of its element such that it can be 'revealed in an increasing order'
*reveal increasing order - the resulting array should contain weave patterns, for ex:
Input: deck = \[17,13,11,2,3,5,7\]
Output: \[2,13,3,11,5,17,7\]
Explanation: In the output, 2 gets revealed (removed from list), 13 gets put at the end of the list. Then 3 gets revealed, the next smallest value (removed from list) and 11 gets put at the end of the list, and so on... Keep doing this and all elements will be revealed in increasing order.

```javascript
var deckRevealedIncreasing = function(deck) {
    let arr = deck.sort((a,b)=>b-a);
    let queue = [arr.shift()];

    while(arr.length>0){
        queue.unshift(queue.pop());
        queue.unshift(arr.shift());
    }
    return queue;
};
```

**Priority Queues in Java**

```java
// Initialize Min Heap
PriorityQueue <Integer> pq = new PriorityQueue <Integer>();
// Initialize Max Heap
PriorityQueue <Integer> pq = new PriorityQueue <Integer>(Collections.reverseOrder());

// Add an element to the heap
pq.add(9);

// Pop the min or max element from the heap
int root = pq.poll();

// Size of heap (Get # of elements in heap)
int heapLen = pq.size();
```

**Implement HeapSort: Heapify and turning array into a heap**

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

**Create an ArrayList of Priority Queues in Java**

```java
ArrayList<PriorityQueue<Integer>> list = new ArrayList<>();
for(int i=0; i<grid.length; i++){
    // Create a new priority queue for each row in the grid
    PriorityQueue<Integer> row = new PriorityQueue<>(Collections.reverseOrder());
    for(int j=0; j<grid[i].length; j++){    // Add all values of the row to the priority queue
        row.add(grid[i][j]);
    }
    list.add(row);
}

// Given index j - get the jth priority queue from the ArrayList
PriorityQueue<Integer> pq = list.get(j);
```

**Given 2D arrays like \[\[9, 6\], \[8, 7\]\] sort it by the 1st value of each element in Java**

```java
int [][] array = new int [mat.length] [2];
// fill array with values ...
Arrays.sort(array, (a, b) -> a[0]==b[0] ? a[1]-b[1] : a[0]-b[0]);
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

