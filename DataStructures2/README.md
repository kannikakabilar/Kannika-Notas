<h1 style="color:#1669f0">Data Structures 2</h1>

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





A search in a sorted collection, think binary search. Minimum # of steps, think BFS. Min/max K elements, think heap. Optimization, think DP. Parentheses, think stacks. 

