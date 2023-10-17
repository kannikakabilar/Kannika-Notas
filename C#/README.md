<h1 style="color:#b69cf7">C#</h1>

<h3 style="color:#b69cf7">Strings</h3>

```c#
Console.WriteLine("Hi Kannika");

string myStr = "Hi Hi Kan Kan";    // Note: s in string does not need to be capitalized in c#
myStr.ToUpper();    // returns "HI HI KAN KAN"
myStr.StartsWith("Hi");    // returns true
myStr.IndexOf("Kan");    // returns 6 - first occurence of "Kan"
myStr.Replace("Kan", "Kes");    // returns "Hi Hi Kes Kes"

string [] strLst = myStr.Split(" ");   // string to list

// string to char
char c = char.Parse("c");

// int to string
int num = 1999;
string str = num.ToString();

// string to int
string eighty = "80";
int myNum = int.Parse(eighty);    // for normal size numbers

string veryHugeNum = "223372036854775807";
BigInteger biggie = BigInteger.Parse(veryHugeNum);    // for very big numbers

string maybeNum = "kan9";
int a = 0;
bool res = int.TryParse(maybeNum, out a);
if(res){
  Console.WriteLine(a);    // print out the number
}else{
  Console.WriteLine("The string was not completely made of numbers");
}

string kan = "Kannika";
kan.Equals("Kannika");    // returns true
kan.Length    // returns 7 (Note: Every method name starts with a capital letter in C#)

string moon = "    Moon Missions   ";
moon = moon.Trim();    // Remove leading and trailing spaces

```

<h3 style="color:#b69cf7">Arrays</h3>

```c#
IList <string> strLst = new List <string>();
res.Add("StringItem");

// ArrayList in C#
ArrayList lst = new ArrayList();
// or: var lst = new ArrayList();
lst.Add(9);
int num = (int)lst[0];    // returns 9 but needs to be casted into an int
int lstSize = lst.Count;

int [] myLst = new int [len];
Array.Sort(myLst);
Array.Reverse(myLst); 
```

<h3 style="color:#b69cf7">HashSets & HashMaps</h3>
