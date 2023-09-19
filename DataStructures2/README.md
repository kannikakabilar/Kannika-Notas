<h1 style="color:#1669f0">Data Structures 2</h1>

<h3 style="color:#1669f0">Two Pointers</h3>

#### Given a list or a string - loop through all pairs of elements
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

#### Perform a palindrome-like check 
- compare 1st & last elem, 2nd and 2nd-last elem, ...

#### Swapping inside a while(flag) loop

#### Remove palindromic subsequence until string is empty
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

#### Partition array such that 1st-half of arr contains only even nums and 2nd-half of arr contains odd nums

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

#### Sometime 2 pointers of 1 array can be like:
- i = 0 and arr.length-i-1 &ensp;&ensp; or
- i = 0; j = 1; and they are incremented like: i+=2 and j+=2 where i<arr.length and j<arr.length &ensp;&ensp; 
 &ensp;&ensp; or **Window Sliding**<br>
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

#### Looping through all subsets of an array
- start with outer loop i=0; i<arr.length;
  - add inner loop j=i (or j=i+1) ; j<arr.length
      - body of inner loop contains subset for [i, j)


