<h1 style="color:#0ed5eb">Python</h1>

<h3 style="color:#0ed5eb">Classes</h3>

> - <a style="color:#000000">High-level programming language</a>
> <br>

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
