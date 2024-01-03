<h1 style="color:#fa6339">Java</h1>

<h3 style="color:#fa6339">Arrays</h3>

```java
int[] data = new int[3];
int[] nums = {1, 2, 3, 4, 5, 6, 7, 8, 9};
int mini = Collections.min(nums);    // parameter can be an array or set, returns the lowest value element

// Looping through elements of an array
for(int n : nums){    /* This looping method can be used to loop through a hash set as well */
    System.out.println(n);
}
for(int i=0; i<nums.length; i++){
    System.out.println(nums[i]);
}
```

<h3 style="color:#fa6339">Strings</h3>

```java
String.valueOf(stones.charAt(j)));    /* given a sting called stones, get the char at index j and convert it into a string */

str1.equals(str2);    /* checks if str1 equals str2 */

String[] strLst = str1.split("\\s+");    /* splitting str by 1 or more space */

str1.length()    // returns the length of str1

char [] merge = {'a', 'b', 'c', 'd','e'};

String arrToStr = new String(merge);    // combines the char array into a string

char [] arr1 = str1.toCharArray();    // converts the string into a char array

String str3 = str1.replace("k", "c);    // replace all occurrence of 'k' with 'c'
```

<h3 style="color:#fa6339">Hash Sets</h3>

```java
HashSet <Integer> uniqueNums = new HashSet <Integer>();

uniqueNums.add(n);    // add elements to hash set

uniqueNums.size();    // get size of hash set

uniqueNums.contains(9);    // returns true if the hash set contains 9

uniqueNums.remove(3);    // removes element 3 from hash set

uniqueNums.clear();    // deletes everything in set
```

<h3 style="color:#fa6339">Hash Maps</h3>

- HashMaps in java are pass by reference (if hashmap is changed in function, the changes can be seen outside the function too)

```java
HashMap <Integer, Integer> freq = new HashMap <Integer, Integer>();

freq.containsKey(2);    // Checks if the hashmap has key=2

freq.put(2, freq.get(2)+1);   // updating value of a key in hash map

freq.keySet();

freq.values();    // returns a list of values

Integer [] myArr = new Integer[10];

HashMap <Integer, Integer> mySet = new HashSet <Integer>(Arrays.asList(myArr));    // change an array into a hash set

```

<h3 style="color:#fa6339">Thread Variable: volatile, synchronized, Semaphore</h3>

- Print in Order - LeetCode 1114
- Print FooBar Alternately - LeetCode 1115
- Print Zero Even Odd - LeetCode 1116
- Fizz Buzz Multithreaded - LeetCode 1195
- Building H2O = LeetCode 1117
