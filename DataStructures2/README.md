<h1 style="color:#1669f0">Data Structures 2</h1>

<h3 style="color:#1669f0">Two Pointers</h3>

#### Given a list or a string - loop through all pairs of elements

#### Perform a palindrome-like check 
- compare 1st & last elem, 2nd and 2nd-last elem, ...

#### Swapping inside a while(flag) loop

#### Remove palindromic subsequence until string is empty

#### Partition array such that 1st-half of arr contains only even nums and 2nd-half of arr contains odd nums

#### Sometime 2 pointers of 1 array can be like:
- i = 0 and arr.length-i-1 &ensp;&ensp; or
- i = 0; j = 1; and they are incremented like: i+=2 and j+=2 where i<arr.length and j<arr.length

#### Looping through all subsets of an array
- start with outer loop i=0; i<arr.length;
  - add inner loop j=i (or j=i+1) ; j<arr.length
      - body of inner loop contains subset for [i, j)
