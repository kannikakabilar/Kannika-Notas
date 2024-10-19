<h1 style="color:#0ed5eb">Python</h1>

<h3 style="color:#0ed5eb">Classes</h3>

> - <a style="color:#000000">High-level programming language</a>

```python
class Alien:
    
    total_aliens_created = 0

    def __init__(self, x_coordinate, y_coordinate):
        self.x_coordinate = x_coordinate
        self.y_coordinate = y_coordinate

        self.health = 3

        Alien.total_aliens_created+=1

    def hit(self):
        self.health = max(self.health-1, 0)

    def is_alive(self):
        return self.health>0

    def teleport(self, x_coordinate, y_coordinate):
        self.x_coordinate = x_coordinate
        self.y_coordinate = y_coordinate

    def collision_detection(self, other):
        pass


#TODO:  create the new_aliens_collection() function below to call your Alien class with a list of coordinates.
def new_aliens_collection(coords):
    res = []
    for pos in coords:
        res.append(Alien(pos[0], pos[1]))
    return res
```

> - <a style="color:#000000">Inheritance</a>

```python
class Person:
  def __init__(self, fname, lname):
    self.firstname = fname
    self.lastname = lname

  def printname(self):
    print(self.firstname, self.lastname)

class Student(Person):
  def __init__(self, fname, lname, year):
    super().__init__(fname, lname)
    self.graduationyear = year

  def welcome(self):
    print("Welcome", self.firstname, self.lastname, "to the class of", self.graduationyear)

x = Student("Mike", "Olsen", 2024)
x.welcome()
```

> - <a style="color:#000000">Iterator</a>

```python
class MyNumbers:
  def __iter__(self):
    self.a = 1
    return self

  def __next__(self):
    if self.a <= 20:
      x = self.a
      self.a += 1
      return x
    else:
      raise StopIteration

myclass = MyNumbers()
myiter = iter(myclass)

for x in myiter:
  print(x)
```

> - <a style="color:#000000">Scope</a>

```python

def myfunc1():
  x = "Jane"
  def myfunc2():
    nonlocal x
    x = "hello"
  myfunc2()
  return x

print(myfunc1())    # hello

x = 300

def myfunc():
  global x
  x = 200

myfunc()

print(x)    # 200
```

> - <a style="color:#000000">Modules</a>

```python
# mymodule.py
def greeting(name):
  print("Hello, " + name)

person1 = {
  "name": "John",
  "age": 36,
  "country": "Norway"
}

# main.py
import mymodule

mymodule.greeting("Kannika")

# main2.py
from mymodule import person1

print (person1["age"])

# main3.py
import platform

# List all the defined names belonging to the platform module
x = dir(platform)
print(x)
```

> - <a style="color:#000000">Input</a>

```python
username = input("Enter username:")
print("Username is: " + username)
```
