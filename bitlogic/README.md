<h1 style="color:#5c91fa">Data Structures</h1>

**Primitive DS**       - Predefined way of storing data (ex: int, char, float, double)</br>
**Non-Primitive DS**   - It can store any set of values and even objects</br>

&ensp;&ensp;  **Linear DS**        - elements stored sequentially</br>
&ensp;&ensp;  **Non-Linear DS**    - elements connect to more than 1 elements (ie: trees, graphs)</br>

&ensp;&ensp;  **Static DS**        - fixed size (ie: Arrays) </br>
&ensp;&ensp;  **Dynamic DS**       - can increase size as elements get inserted (ie: Linked List)</br>


<h3 style="color:#5c91fa">Arrays</h3>   -   indexing = O(1) but everything else O(n)

#### Sample Array Qs

**Sorted Array To BST**
```python
def sortedArrayToBST(nums: List[int]):
    if len(nums) == 0:
        return None

    root = len(nums)//2 
    tree = TreeNode(nums[root])

    tree.left = sortedArrayToBST(nums[:root])

    tree.right = sortedArrayToBST(nums[root+1:])
    
    return tree
```
**Search Sorted Array**
```python
  def searchSortedArray(nums: List[int], target: int) -> int:
      left, right = 0, len(nums) - 1              
          
      while left <= right:                        
          middle = (right+left) // 2       
          if nums[middle] == target:              
              return middle
          if nums[middle] > target:               
              right = middle - 1
          else:                                   
              left = middle + 1
      return left
```
**Reverse Merge**
```python
def reverseMerge(nums1: List[int], m: int, nums2: List[int], n: int) -> None:

    last = m + n - 1

    while m > 0 and n > 0:  
        if nums1[m - 1] > nums2[n - 1]:    
            nums1[last] = nums1[m - 1]    
            m -= 1                        
        else:                             
            nums1[last] = nums2[n - 1]
            n -= 1
        last -= 1  

    while n > 0:
        nums1[last] = nums2[n - 1]
        n, last = n - 1, last - 1
```

**Generate Pascal**
```python
def generatePascal(numRows: int) -> List[List[int]]:
    l = []
    for i in range(numRows):
        l.append([])
        for j in range(i+1):
            if i == 0 or i == 1:
                l[i].append(1)
            elif j == 0 or j == i:
                l[i].append(1)
            else:
                l[i].append(l[i-1][j-1] + l[i-1][j])
    return l
```
**Stock Profit**
```python
def stockProfit(prices: List[int]) -> int:

    if prices != []:
        min = prices[0]

    diff = 0
    for i in range(1, len(prices)):
        if prices[i] < min:
            min = prices[i]
        if diff < prices[i] - min:
            diff = prices[i] - min

    return diff
```
**Find The Single Number**
```python
def singleNumber(nums: List[int]) -> int:
    res = 0
    for num in nums:
        res ^= num
    return res
```
**Remove Duplicates**
```python
def removeDuplicates(nums: List[int]) -> int:
    length = len(nums)
    if length == 1:    
        return 1

    else:
        j = 0                          # i and j double pointers
        i = 1
        count = 1                      
        
        for i in range(length):        
            if nums[i] != nums[j]:
                j += 1                 # j only increases if i reaches a distinct element
                nums[j] = nums[i]      
                count += 1             
        
        return count
```
**Remove Element**
```python
def removeElement(nums: List[int], val: int) -> int:
    j = 0                        # Create 2 pointers i and j
    i = 0
    for j in range:              
        if nums[j] != val:       
            nums[i] = nums[j]    
            i += 1               
    return i
```
**Move Zeroes To End**
```python
def moveZeroes(nums: List[int]) -> None:
    i = 0                        # Create 2 pointers i and j
    j = 0
    zero = 0  

    for j in range(len(nums)):   
        if nums[j] != 0:         
            nums[i] = nums[j]
            i += 1
        else:
            zero += 1

    for j in range(zero):       
        nums[len(nums)-(j+1)] = 0
        
    return nums
```
**Kadane's Algorithm - Max Sub Array**
```python
def maxSubArray(nums: List[int]) -> int:
    # Kadane's algorithm
    maxi=nums[0] 
    sums=0
    for i in range(len(nums)):
        sums+=nums[i]
        maxi=max(sums,maxi)

        if sums<0: 
            sums=0
    
    return maxi
```
**Kadane's Algorithm - Stock Profit**
```python
def stockProfit(prices: List[int]) -> int:
    # Kadane's algorithm
    maxCur = 0
    maxSoFar = 0

    for i in range(1, len(prices)):
        maxCur += prices[i] - prices[i-1]
        maxCur = max(0, maxCur)
        maxSoFar = max(maxCur, maxSoFar)

    return maxSoFar
```
___________________________________________

<h3 style="color:#5c91fa">Linked Lists</h3>   -   inserting = O(1) but everything else O(n)

#### Sample Linked List Qs

**Merge 2 Lists**
```python
def mergeTwoLists(l1: ListNode, l2: ListNode) -> ListNode:
        
        head = ListNode()                    
        m = head                             # Use this variable to traverse through
        while (l1 and l2):     

            if l1.val < l2.val:              
                m.next = ListNode(l1.val)
                l1 = l1.next

            elif l2.val <= l1.val:          
                m.next = ListNode(l2.val)
                l2 = l2.next

            m = m.next
        
        if l1 is not None:                  
            m.next = l1
        if l2 is not None:
            m.next = l2

        return head.next  
```
**Delete Duplicates**
```python
def deleteDuplicates(head: ListNode) -> ListNode:
    if head is None:                
        return head

    m = head                        # Leave a pointer to the head
    prev = m.val                    
    temp = m                        
    m = m.next

    while m is not None:            
        if m.val == prev:           
            temp.next = m.next      
        
        else:                       
            prev = m.val            
            temp = temp.next  

        m = m.next
    return head
```
**Remove Elements**
```python
def removeElements(head: ListNode, val: int) -> ListNode:
    if head is None:                               
        return head

    m = head                                       
    while (m is not None) and m.val == val:        # Find first node that does NOT equal val
        m = m.next
    
    head = m                                       
    temp = m                                       
    if m is not None:                              
        m = m.next

    while m is not None:                           
        if m.val == val:                          
            temp.next = m.next                     
        else:                                      
            temp = temp.next                       
        m = m.next

    return head
```
**Reverse List**
```python
def reverseList(head: ListNode) -> ListNode:
    if (head is None) or (head.next is None):       # Handle empty linked list and 1-element linked list case
        return head   

    prev = None
    current = head

    while(current is not None):
        next = current.next
        current.next = prev
        prev = current
        current = next

    head = prev
    return head
```
**Is Palindrome?**
```python
def isPalindrome(head: ListNode) -> bool:

    if not head.next:
        return True
    
    # find the middle
    fast, slow = head, head
    while fast and fast.next:
        fast = fast.next.next
        slow = slow.next

    # reverse the second half
    prev = None        
    while slow:
        tmp = slow.next
        slow.next = prev
        prev = slow
        slow = tmp
    
    # check if palindrome:
    left, right = head, prev
    while right:
        if left.val != right.val:
            return False
        left = left.next
        right = right.next

    return True  
```
**Find Middle Node**
```python
def middleNode(head: ListNode) -> ListNode:
    if not head.next:
        return True
    
    # find the middle
    fast, slow = head, head
    while fast and fast.next:
        fast = fast.next.next
        slow = slow.next

  return slow
```
**Binary to Decimal**
```python
def getDecimalValue(head: ListNode) -> int:
    
    res = 0                           
    place = 0                         
    if head is None:                  
        return res
    tmp = head

    while not(tmp is None):           # Calculate the total number of digits
        place += 1
        tmp = tmp.next
    tmp2 = head
    place -= 1  

    while not(tmp2 is None):          # Traverse through bin str and sum the decimal value
        res += (2**place)*tmp2.val    
        tmp2 = tmp2.next
        place -= 1

    return res
```
**Check if a LL has a cycle** </br>
&ensp;&ensp;  1) if all elements are distint => fast and slow method where fast would catch up to slow </br>
&ensp;&ensp;  2) change value of elements to -1 and check if you ever reach -1 </br>
___________________________________________

<h3 style="color:#5c91fa">Stacks</h3>   -   used for evaluating math expr and recursive function calls

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

<h3 style="color:#5c91fa">Hash Table</h3>

### Terms
- **Hash function**: input is key-value and the output is memory address/slot# of where the element will be stored</br>
- **Collision => chaining**: when 2 elements are directed to the same slot use linked list or trees to store the element at that address</br>
- **Open Addressing**: store all values within the hash table</br>
    - **Linear Probing**: if hash(x) % S is full => (hash(x) + 1) % S</br></br>

  **Initializing HashMap and HashSet in Java**

```java
    import java.util.HashMap;
    import java.util.HashSet;

    HashMap<String, String> capitalCities = new HashMap<String, String>();
    capitalCities.put("USA", "Washington DC");
    String USCapital = capitalCities.get("USA");  // "Washington DC"

    for (String i : capitalCities.keySet()) {
        System.out.println(i);  // Print keys
    }

    for (String i : capitalCities.values()) {
        System.out.println(i);  // Print values
    }

    HashSet<String> cars = new HashSet<String>();
    cars.add("McLaren");
    cars.contains("McLaren"); // Returns True
```

#### Sample HashMap/HashSet Qs

  - Find a pair of nums with given sum and an array of nums</br>
  - Roman Numeral to Num</br>
  - Keeping track of values</br>
  - is Isomorphic?</br>
  - is Anagram? (ie: Nathaniel Black => Anabella Thick)</br>
  - is List unique?</br>
  - union & intersection of 2 LL</br>
  - missing elements of a range</br></br>

**4 elements such that a + b = c + d**
```python
def find_pair_of_sum(arr: list, n: int):
    map = {}
 
    for i in range(n):
        for j in range(i+1, n):
            sum = arr[i] + arr[j]
 
            if sum in map:
                print(f"{map[sum]} and ({arr[i]}, {arr[j]})")
                return
            else:
                map[sum] = (arr[i], arr[j])
```
___________________________________________


<h3 style="color:#5c91fa">Trees</h3>

### Sample Tree Implementation Explanations

  - **N-ary**: each node can have upto N children
  - **Binary**: each node can have upto 2 children
  - **BST**: left_child.val < root.val < right_child.val</br></br>

  - **AVL**: better for searching, height <= log2(n)</br>
        types of rotations</br>
          &ensp;&ensp;left-left case => right rotation</br>
          &ensp;&ensp;left-right case => left rotate, right rotate</br>
          &ensp;&ensp;right-left case => right rotate, left rotate</br>
          &ensp;&ensp;right-right case => left rotation</br></br>

  - **Red-Black**: better for insertion and deletion</br>
      rules</br>
        &ensp;&ensp;1) root is always black</br>
        &ensp;&ensp;2) all leaves are black</br>
        &ensp;&ensp;3) all leaves have same # of black ancestors</br>
        &ensp;&ensp;4) all children of red nodes are black</br></br>

  - **B-Tree**</br>
      notes</br>
        &ensp;&ensp;- each node can have upto n-1 values</br>
        &ensp;&ensp;- each node can have atmost n children and at least n/2 children</br>
        &ensp;&ensp;- all leaves have the same depth</br></br>

  - **Heap**</br>
      &ensp;&ensp;- Max/Min Heap: all children node values are less/higher than parent</br>
      &ensp;&ensp;- Insertion: insert in the next according space and performing swapping with parent</br>
      &ensp;&ensp;- Deletion: swap node-to-be-deleted with last node, delete last node, perform swapping with the switched node</br>

    - **Treap**: mix of BST and and Heap </br>
        &ensp;&ensp;- each node stores 2 values (key=value_inserted, priority=random_num)</br>
        &ensp;&ensp;- insert according key which follows BST, then perform AVL rotations to maintain priority which follows Heap</br></br>
      
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











