<h1 style="color:#fa6339">Java</h1>

<h3 style="color:#fa6339">Setup</h3>

> - <a style="color:#000000">How do you check if Java is installed in a machine?</a>
>
> - <a style="color:#000000">What needs to be done after installing Java and before running a Java program?</a>
>
> - <a style="color:#000000">What should the name of the Java file match?</a>
>
> - <a style="color:#000000">What method needs to be in a Java program in order to execute?</a>

<h3 style="color:#fa6339">Varaibles</h3>

> - <a style="color:#000000">Initialize a float variable with value: 19.989 and print upto 2 decimal digits using formatting</a>
>
> - <a style="color:#000000">What does it mean if a variable is initialized as a 'final' variable?</a>
>
> - <a style="color:#000000">What is a Wrapper class for a primitive data type in Java?</a>
>
> - <a style="color:#000000">How do you cast a double data type to an int?</a>
>
> - <a style="color:#000000">Print a number between 0 to 100 inclusive</a>

```java
float myFloat = 19.989f;
System.out.printf("myFloat is: %.2f", myFloat);

​final int myNum = 15;
myNum = 20;  // error: cannot re-assign value to final variable

int prim = 5;
Integer wrap = 5;

double myDouble = 19.99d;
int myInt = (int)myDouble;

```

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

String str3 = str1.replace("k", "c");    // replace all occurrence of 'k' with 'c'

String str = "HelloWorld";
System.out.println(str.toLowerCase());

String str1 = "Kannika";
String str2 = "nn";
System.out.println(str1.indexOf(str2));    // outputs 2
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

<h3 style="color:#fa6339">File Handling</h3>

> - <a style="color:#000000">What needs to be imported when handling files in Java?</a>
>
> - <a style="color:#000000">When writing code to handle files, what block must it be in?</a>
>
> - <a style="color:#000000">How do you create a new file? ~2 lines</a>
>
> - <a style="color:#000000">How do you write to a file? ~3 lines</a>
>
> - <a style="color:#000000">How do you read a file? ~3 lines + while-loop</a>

```java
import java.io.*;

public class JavaFile {
  public static void main(String[] args) {
    
    try {
        // Create a new file
        File myObj = new File("C:\\Users\\MyName\\filename.txt");    // double backslash only for windows
        myObj.createNewFile();    // System.out.println("File created: " + myObj.getName());

        // Write to a file
        FileWriter myWriter = new FileWriter("filename.txt");
        myWriter.write("Files in Java might be tricky, but it is fun enough!");
        myWriter.close();

        // Read a file
        File myObj = new File("filename.txt");
        Scanner myReader = new Scanner(myObj);
        while (myReader.hasNextLine()) {
            String data = myReader.nextLine();
            System.out.println(data);
        }
        myReader.close();
    }catch(Exception e){
        System.out.println("An error occurred.");
    }

  }
}
```

<h3 style="color:#fa6339">Java Classes</h3>

> - <a style="color:#000000">What's the difference between Prodecedural-Programming vs Object-Oriented-Programming ?</a>
>
> - <a style="color:#000000">What's the difference between static methods and public method in a class?</a>
>
> - <a style="color:#000000">What is a constructor used for?</a>
>
> - <a style="color:#000000">What must a constructor not mention and it cannot have?</a>
>
> - <a style="color:#000000">What are the 4 access modifiers? and what permissions do they allow?</a>
>
> - <a style="color:#000000">Define what these key words mean in Java: final, static, abstract, transient, synchronized, volatile</a>
>
> - <a style="color:#000000">How do you import a built-in package and how do you create a user-defined package and import it to another file? Also, how do you compile the package?</a>
>
> - <a style="color:#000000">How do you inherit from a parent class? How do you use the parent class' variables and methods?</a>
>
> - <a style="color:#000000">What is Polymorphism and 'instanceof' method in Java?</a>
>
> - <a style="color:#000000">How do you create an object of an inner/nested class in Java?</a>
>
> - <a style="color:#000000">How do you initialize an abstract class in Java and what is it used for?</a>
>
> - <a style="color:#000000">How is an interface different from abstract class?(2 points) How do you implement an inteface?</a>
>
> - <a style="color:#000000">How do you take in a user input? - 2 lines</a>

```java
```

<h3 style="color:#fa6339">Java Threads</h3>

> - <a style="color:#000000">What are the 2 ways to create a thread and show how to implement them?</a>


<h3 style="color:#fa6339">Java Serialization</h3>

> - <a style="color:#000000">What is serialization?</a>
>
> - <a style="color:#000000">Show how you serialize and deserialize an object</a>

<a href="https://kannikalibreta.weebly.com/java.html#InterviewNotes"><h3 style="color:#fa6339">Java Interview Notes</h3></a>
