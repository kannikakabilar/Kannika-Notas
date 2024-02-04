<h1 style="color:#fa6339">Java</h1>

<h3 style="color:#fa6339">Setup</h3>

> - <a style="color:#000000">How do you check if Java is installed in a machine?</a>
>
> - <a style="color:#000000">What needs to be done after installing Java and before running a Java program?</a>
>
> - <a style="color:#000000">How many classes can a Java file have?</a>
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

int randomNum = (int)(Math.random() * 101); ​// 0 to 100

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

Integer [] myArr = new Integer[10];

HashSet <Integer> mySet = new HashSet <Integer>(Arrays.asList(myArr));    // change an array into a hash set

```


<h3 style="color:#fa6339">Java Threads</h3>

<h4 style="color:#fa6339">Thread Variable: volatile, synchronized, Semaphore</h4>

- Print in Order - LeetCode 1114
- Print FooBar Alternately - LeetCode 1115
- Print Zero Even Odd - LeetCode 1116
- Fizz Buzz Multithreaded - LeetCode 1195
- Building H2O = LeetCode 1117

> - <a style="color:#000000">What are the 2 ways to create a thread and show how to implement them?</a>

```java
/* Extend Thread class, create an instance, and override its run method */
​public class Main extends Thread {
  public static void main(String[] args) {
    Main thread = new Main();
    thread.start();
    thread.join();    // Waits for thread to finish executing before continuing
    System.out.println("This code is outside of the thread");
  }
  public void run() {
    System.out.println("This code is running in a thread");
  }
}

/* Implement the Runnable Interface, create an instance, and override its run method */
public class Main implements Runnable {
  public static void main(String[] args) {
    Main obj = new Main();
    Thread thread = new Thread(obj);
    thread.start();
    System.out.println("This code is outside of the thread");
  }
  public void run() {
    System.out.println("This code is running in a thread");
  }
}
```

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
            String data = myReader.nextLine();    // use myReader.nextInt() if you want to read an integer
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
> - <a style="color:#000000">How do you create an object of an inner/nested class and an object of a static-nested class in Java?</a>
>
> - <a style="color:#000000">How do you initialize an abstract class in Java and what is it used for?</a>
>
> - <a style="color:#000000">How is an interface different from abstract class?(2 points) How do you implement an inteface?</a>
>
> - <a style="color:#000000">How do you take in a user input? - 2 lines</a>

```java
/* Packages */
//  MyPackageClass.java
package mypack;    //  package name should be written in lower case
class MyPackageClass {
  public static void main(String[] args) {
    System.out.println("This is my package!");
  }
}

// Above package can be imported like this
import mypack.MyPackageClass;    // or import mypack.*;

>javac -d . MyPackageClass.java
//  The -d keyword specifies the destination for where to save the class file/create the package ( '.' is current dir)

/* Inheritance */
class Vehicle {
  protected String brand = "McLaren";        // Vehicle attribute
  protected String color = "White";        // Default vehicle color
  public void honk() {                    // Vehicle method
    System.out.println("Tuut, tuut!");
  }
}

class Car extends Vehicle {
  private String modelName = "650s Spider";    // Car attribute
  private String color = "Blue";                       // New Car Color
  public static void main(String[] args) {

    // Create a myCar object
    

    // Call the honk() method (from the Vehicle class) on the myCar object
    

    // What does this print?
    System.out.println(myCar.brand + " " + myCar.modelName);

   //  Differentiating between parent and child attributes using 'super'

   // parent constructors can be called using super()
   // only use super when method/attribute names are identical in parent & child

   System.out.println(myCar instanceof Vehicle);   // What does this output?
  }
}

/* Nested Class */
class OuterClass {
  int x = 10;

  class InnerClass {
    int y = 5;
    //  InnerClass can access any attribute/methods from outer class
    public void getParentAttribute(){
        // print the value of x here
    }
  }
}

public class Main {
  public static void main(String[] args) {
    OuterClass myOuter = new OuterClass();
    OuterClass.InnerClass myInner = myOuter.new InnerClass();
    System.out.println(myInner.y + myOuter.x);    // Outputs 15 (5 + 10)
    myInner.getParentAttribute();    //  Outputs: Getting parent attribute: 10
  }
}

/* Abstract Classes */
abstract class Animal {    // abstract classes can contain abstract methods and regular methods
  // Abstract method (does not have a body) and can only exist in abstract classes - must be overriden in child class
  public abstract void animalSound();
  // Regular method
  public void sleep() {
    System.out.println("Zzz");
  }
}

// Subclass (inherit from Animal)
class Pig extends Animal {
  public void animalSound() {
    // The body of animalSound() is provided here
    System.out.println("The pig says: oink oink!");
  }
}

class Main {
  public static void main(String[] args) {
    Pig myPig = new Pig();    // Create a Pig object because abstract classes cannot be used to create objects
    myPig.animalSound();
    myPig.sleep();
  }
}

/* Interfaces */
interface Animal {
  // interface methods cannot contain a body
  public void animalSound(); 
  public void sleep();
  // Interface methods can be: public, abstract
  // Interface attributes can be: public, static, final
}

class Pig implements Animal {
  public void animalSound() {
    // The body of animalSound() and sleep() is provided here and all child classes must override them
    System.out.println("Piggy says: Oink Oink!");
  }
  public void sleep() {
    // The body of sleep() is provided here
    System.out.println("Piggy is asleep: Zzz...");
  }
}

class Main {
  public static void main(String[] args) {
    // Create a Pig object because interface cannot be used to create objects and interface don't/can't have constructors
    Pig myPig = new Pig();  
    myPig.animalSound();
    myPig.sleep();
  }
}

/* Getting User Input */
import java.util.Scanner;  // Import the Scanner class

class Main {
  public static void main(String[] args) {
    Scanner myObj = new Scanner(System.in);  // Create a Scanner object
    System.out.println("Enter username");

    String userName = myObj.nextLine();  // Read user input
    System.out.println("Username is: " + userName);  // Output user input
  }
}
/*   
    nextLine()    reads a string from user
    nextInt()       reads an int from user
    Similarly:    nextBoolean(), nextByte(), nextDouble(), nextFloat(), nextLong(), nextShort()
​*/
```

<h3 style="color:#fa6339"><a style="color:#fa6339" href="https://kannikalibreta.weebly.com/java.html#Serialization">Java Serialization</a></h3>

> - <a style="color:#000000">What is serialization?</a>
>
> - <a style="color:#000000">What 2 conditions need to be for a class to be successfully serializable and what needs to imported?</a>
>
> - <a style="color:#000000">What file extension is used for a serialized Java object to be stored in?</a>
>
> - <a style="color:#000000">Show how you serialize and deserialize an object - What block should the following statements be located in?</a>
> &emsp; - <a style="color:#000000">What are the 2 starting statements in writing an object (serializing) and reading an object (deserializing)?</a>
>
> &emsp; - <a style="color:#000000">What is the statement that is used to write the object to the file and to read the object from a file?</a>
>
> &emsp; - <a style="color:#000000">What are the 2 final closing statements after writing/reading a statement?</a>


<h3 style="color:#fa6339"><a style="color:#fa6339" href="https://kannikalibreta.weebly.com/java.html#InterviewNotes">Java Interview Notes</a></h3>
