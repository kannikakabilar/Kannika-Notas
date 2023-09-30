<h1 style="color:#5c91fa">Data Structures</h1>

**Primitive DS**       - Predefined way of storing data (ex: int, char, float, double)<br>
**Non-Primitive DS**   - It can store any set of values and even objects<br>

&ensp;&ensp;  **Linear DS**        - elements stored sequentially<br>
&ensp;&ensp;  **Non-Linear DS**    - elements connect to more than 1 elements (ie: trees, graphs)<br>

&ensp;&ensp;  **Static DS**        - fixed size (ie: Arrays) <br>
&ensp;&ensp;  **Dynamic DS**       - can increase size as elements get inserted (ie: Linked List)<br>


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
**If elements are from \[1, n\] => then try using them as index**
Given a list of nums of size n that contains elements 1 to n, return a list of elements from nums that occur twice (or more) in the list.

```javascript
var findDuplicates = function(nums) {
    let res = [];
    for(let n of nums){
        if(n<=nums.length && nums[n-1]>nums.length){
            res.push(Math.abs(n));
        }else if(n>nums.length && nums[n-nums.length-1]>nums.length){
            res.push(Math.abs(n));
        }else{
            nums[n-1] = nums[n-1] + nums.length;
        }
        console.log(nums);
    }
    return res;
};
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
**Check if a LL has a cycle** <br>
&ensp;&ensp;  1) if all elements are distint => fast and slow method where fast would catch up to slow <br>
&ensp;&ensp;  2) change value of elements to -1 and check if you ever reach -1 <br>

___________________________________________


<h3 style="color:#5c91fa">Hash Table</h3>

### Terms
- **Hash function**: input is key-value and the output is memory address/slot# of where the element will be stored<br>
A Hashmap can be designed by creating a large array where the key(int) can be the index of the array and the value can be stored at that index of the array
- **Collision => chaining**: when 2 elements are directed to the same slot use linked list or trees to store the element at that address <br>
- **Open Addressing**: store all values within the hash table <br>
    - **Linear Probing**: if hash(x) % S is full => (hash(x) + 1) % S <br><br>

  **Initializing HashMaps in Java**

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

    // HashMap Integer example
    HashMap <Integer, Integer> freq = new HashMap <Integer, Integer>();
    freq.containsKey(2);    // Checks if the hashmap has key=2

    freq.put(2, freq.get(2)+1);   // updating value of a key in hash map
    freq.keySet();
    freq.values();    // returns a list of values

    Integer [] myArr = new Integer[10];
    HashMap <Integer, Integer> mySet = new HashSet <Integer>(Arrays.asList(myArr));    // change an array into a hash set

```

*HashMaps in java are **pass by reference** (if hashmap is changed in function, the changes can be seen outside the function too) <br><br>

  **Initializing HashSets in Java**
  
```java
    HashSet<String> cars = new HashSet<String>();
    cars.add("McLaren");
    cars.contains("McLaren"); // Returns True

    HashSet <String> uniqueNums = new HashSet <String>();
    uniqueNums.add(n);    // add elements to hash set
    uniqueNums.size();    // get size of hash set
    uniqueNums.contains(9);    // returns true if the hash set contains 9
    uniqueNums.remove(3);    // removes element 3 from hash set
    uniqueNums.clear();    // deletes everything in set
```

- Hash Tables (work similar to HashMaps) aren't used anymore but they provide enumeration and are thread safe while Hash Maps don't

#### Sample HashMap/HashSet Qs

  - Find a pair of nums with given sum and an array of nums<br>
  - Roman Numeral to Num<br>
  - Keeping track of values<br>
  - is Isomorphic?<br>
  - is Anagram? (ie: Nathaniel Black => Anabella Thick)<br>
  - is List unique?<br>
  - union & intersection of 2 LL<br>
  - missing elements of a range<br><br>

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


<h2 style="color:#1669f0">Two Pointers</h2>

### Given a list or a string - loop through all pairs of elements
- In Java **Count Pairs Whose Sum is Less than Target**

```java
  public int countPairs(List<Integer> nums, int target) {
      int count = 0;
      for(int i=0; i<nums.size(); i++){
          for(int j=i+1; j<nums.size(); j++){
              if(nums.get(i)+nums.get(j)<target){
                  count++;
              }
          }
      }
      return count;
  }
```

### Perform a palindrome-like check 
- compare 1st & last elem, 2nd and 2nd-last elem, ...
- use i=0 and compare arr\[i\] and arr\[arr.length-i-1\]

### Remove palindromic subsequence until string is empty
- Given a string made-up of only 2 letters
- at a single step, a palindromic subsequence can be removed
    - Soln.: if org string is a palindrome => only 1 step is needed to make string empty
    - else only 2 step is needed to make string empty

In JavaScript
```javascript
var removePalindromeSub = function(s) {

    let i = 0;
    let j = s.length - 1;
    s = s.split('');
    while(i<j){
        if(s[i++]!=s[j--]){
            return 2;
        }
    }
    return 1;    
};
```

### Partition array such that 1st-half of arr contains only even nums and 2nd-half of arr contains odd nums

```javascript
var sortArrayByParity = function(nums) {
    
    let i = 0;
    while(i<nums.length){
        if(nums[i]%2 != 0){
            break;
        }
        i++;
    }
    let tmp = 0;
    for(let j=i+1; j<nums.length; j++){
        if(nums[j]%2==0){
            tmp = nums[i];
            nums[i] = nums[j];
            nums[j] = tmp;
            i++;
        }
    }
    return nums;
};
```

### Sometimes 2 pointers of 1 array can be like:
- i = 0 and arr.length-i-1 &ensp;&ensp; or
- i = 0; j = 1; and they are incremented like: i+=2 and j+=2 where i<arr.length and j<arr.length &ensp;&ensp; <br>
 &ensp;&ensp; or &ensp;&ensp; **Window Sliding**<br>
- i = 0; while(i+k<arr.length) where we are looping through contiguous subsequence of size k

**Number of Sub-arrays of Size K and Average Greater than or Equal to Threshold**
```javascript
var average = function(arr, i, j, k){
    let sum = 0;
    for(let a=i; a<j; a++){
        sum += arr[a];
    }
    return sum/k;
}
var numOfSubarrays = function(arr, k, threshold) {
    let i = 0;
    let count = 0;
    while(i+k<=arr.length){
        if(average(arr, i, i+k, k)>=threshold){
            count++;
        }
        i++;
    }
    return count;
};
```

### Looping through all subsets of an array
- start with outer loop i=0; i<arr.length;
  - add inner loop j=i (or j=i+1) ; j<arr.length
      - body of inner loop contains subset for [i, j)


<h2 style="color:#1669f0">Math</h2>

### Handling Big Numbers
- In Java, when handling big numbers => convert them to strings and/or use **long int num = ...** 

- In JavaScript, when handling big numbers => convert them to strings and/or use **BigInt(num)**

```javascript
/* Calculate the product of all integers in the inclusive range [left, right] and write it in a specific format */

var abbreviateProduct = function(left, right) {
    let prod = 1;
    while(left<=right){
        prod = BigInt(prod)*BigInt(left);
        left++;
    }
    // # of trailing zeros must be cocatenated after 'e' in the resultin string
    let c = 0;
    while(prod%BigInt(10)==0){
        prod = BigInt(prod) / BigInt(10);
        c++;
    }
    let numStr = prod.toString();
    // if # of digits of prod > 10, then write it in this format: [first 5 digits of prod]...[last 5 digits of prod]e[#_of_trailing_zeros]
    if(numStr.length<=10){
        return numStr+"e"+c.toString();
    }else{
        return numStr.slice(0, 5)+"..."+numStr.slice(numStr.length-5, numStr.length)+"e"+c.toString();
    }
};
```

### Prime Palindrome: Given n, find a number a greater or equal to n that is a palindrome and a prime number

```javascript
var isPrime = function(n) {
    if(n<=1||n==4||n==8||n==6){
        return false;
    }
    if(n==2||n==3||n==5||n==7){
        return true;
    }
    for(let i=3; i<=Math.sqrt(n); i+=2){
        if(n%i == 0){
            return false;
        }
    }
    return true;
};
var isPalindrome = function(n) {
    n = n.toString();
    let i = 0;
    while(i<n.length){
        if(n[i]!=n[n.length-i-1]){
            return false;
        }
        i++;
    }
    return true;
};
var primePalindrome = function(n) {
    while(true){
        if(n==1||n==2){
            return 2;
        }else if(n%2==0){
            n++;
            continue;
        }
        if(isPalindrome(n) && isPrime(n)){
            return n;
        }
        n+=2;
    }
};
```

### Count # of primes strictly less than n

```javascript
var countPrimes = function(n) {
    let count = 0;
    let arr = [];
    for(let i=2; i<n; i++){
        if(arr[i]){
            continue;
        }else{
            count++;
        }
        for(let j=i+i; j<=n; j+=i){
            arr[j]=true;
        }
    }
    return count;   
};
```

### Reverse an integer

```javascript
var reverse = function(x) {
    if(x==0){
        return 0;
    }
    let str = x.toString();
    let arr = str.split('');
    let res = "";
    if(str[0]=="-"){
        res += "-";
    }
    for(let i=0; i<str.length; i++){
        if(str[str.length-i-1]=="-"){
            //res += "-";
            continue;
        }else if(i==0 && str[str.length-i-1]=="0"){
            continue;
        }
        res += str[str.length-i-1];
    }    
    
    if(BigInt(res)<BigInt(-2147483648) || BigInt(res)>BigInt(2147483647)){
        return 0;
    }else{
        return parseInt(res, 10);
    }
    
};
```

### Summing &ensp;&ensp; 1+3+5+...+n &ensp;&ensp; or &ensp;&ensp; 2+4+6+...+n
- Sequence: 1, 3, 5, 7, 9, ...
  - formula to get nth term = 1 + 2*(n-1)
  - formula to get sum = n*(1 + nth_term)/2

- Sequence: 2, 4, 6, 8, 10, ...
  - formula to get nth term = 2 + 2*(n-1)
  - formula to get sum = n*(2 + nth_term)/2

### Summing 1+2+3+4+...+n
- formula to get sum = n*(n+1)/2

**Given an integer array nums, return the number of subarrays filled with 0.
A subarray is a contiguous non-empty sequence of elements within an array.**

```javascript
var zeroFilledSubarray = function(nums) {
    let start = -1;
    let count = 0;
    let n = 0;
    for(let i=0; i<nums.length; i++){
        if(start!=-1 && nums[i]!=0){
            n = i - start;
            count += ((n*(n+1))/2);
            start = -1;
        }else if(start==-1 && nums[i]==0){
            start = i;
        }
    }
    if(start!=-1){
        n = nums.length - start;
        count += ((n*(n+1))/2);
        start = -1;
    }
    return count;
};
```

**Minimum Operations to Make Array Equal**

```javascript
var minOperations = function(n) {
    if(n%2 == 0){
        let myn = n/2;
        let res = 2 + (2*(myn-1));
        return (res * myn)/2;
    }else{
        let mym = (n-1)/2;
        let res = 4 + (2*(mym-1));
        return (res * mym)/2;
    }
    
};
```

### Like converting a decimal number to binary: 
### &ensp; Given a number check if it can be written by sum of powers-of-3

```javascript
var checkPowersOfThree = function(n) {
    if(n==0 || n%3==2){
        return false;
    }else if(n==1){
        return true;
    }else{
        let count = 1;
        while(Math.pow(3, count)<n){
            count++;
        }
        if(Math.pow(3, count) == n){
            return true;
        }else{
            count--;
            n -= Math.pow(3, count);
            for(let i=count-1; i>=0; i--){
                if(Math.pow(3, i)<=n){
                    n -= Math.pow(3, i);
                }
            }
            return n==0;
        }
    }
};
```

<h2 style="color:#1669f0">Arrays + HashMap</h2>

Given an integer array nums of length n where all the integers of nums are in the range \[1, n\] and each integer appears once or twice, return an array of all the integers that appears twice. Try time complexity O(n) and space complexity O(1)

```javascript
var findDuplicates = function(nums) {
    let res = [];
    for(let n of nums){
        if(n<=nums.length && nums[n-1]>nums.length){
            res.push(Math.abs(n));
        }else if(n>nums.length && nums[n-nums.length-1]>nums.length){
            res.push(Math.abs(n));
        }else{
            nums[n-1] = nums[n-1] + nums.length;
        }
        console.log(nums);
    }
    return res;
};
```

Given an integer array => create a 2D array from it such that each row in the 2D array contians distinct elements and the number of rows should be minimal <br>

for example:
Input: nums = \[1,3,4,1,2,3,1\]
Output: \[\[1,3,4,2\],\[1,3\],\[1\]\]

```javascript
var findMatrix = function(nums) {
    let freq = new Map();
    let res = [];
    for(let i=0; i<nums.length; i++){
        if(freq.has(nums[i])){
            freq.set(nums[i], freq.get(nums[i])+1);
        }else{
            freq.set(nums[i], 1);
        }
    }

    for(let [key, value] of freq){
        for(let j=0; j<Math.min(res.length, value); j++){
            res[j].push(key);
        }
        while(res.length<value){
            res.push([key]);
        }
    }
    return res;
};
```

Given an integer array groupSizes, where groupSizes[i] is the size of the group that person i is in. Return a list of groups such that each person i is in a group of size groupSizes[i].

for example
Input: groupSizes = \[3,3,3,3,3,1,3\]
Output: \[\[5\],\[0,1,2\],\[3,4,6\]\] 

```javascript
var groupThePeople = function(groupSizes) {
    let res = [];
    let groups = {};

    let size = 0;
    for(let i=0; i<groupSizes.length; i++){
        size = groupSizes[i];
        if(!groups[size]){
            groups[size] = [];
        }
        groups[size].push(i);

        if(groups[size].length == size){
            res.push(groups[size]);
            delete groups[size];
        }
    }
    return res;
};
```
___________________________________________











