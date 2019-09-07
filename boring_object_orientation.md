# Boring Object Orientation 9/7/19
## Moshe Zadka - https://cobordism.com
---

### Object Oriented Programming
Everything is an object

Boring objects:
- Declare interfaces
- Simplify initialization
- Avoid mutation
- Avoid hiding
- Avoid methods
- Avoid inheritance

### Why declare interfaces
Explicit is better than implicit. 

### Boring Constructor
Use __init__ methods!
Add @classmethod methods that can then complete the creation- attributes that call other constructors, retrieving things from files, etc. When this fails it is more obvious what has happened. You'll have better tracebacks. Easier testing as well if you want to use mock etc. Also you do not create partial objects. Makes it easier to initialize objects asynchronously. 

### Using Attr
@attr.s(auto_attribs=True, frozen=True)
Will stop you from mutating an attribute later. Immutibility helps you avoid bugs.
Evolve method lets you take an object and create a duplicate of it with an updated value you can store as a new object.

### Functools
Has a decorator for single dispatch, which you can register different class methods that might be shared by different classes (Point2D, Point3D, with distance for example). You can then have a 2D and a 3D distance that are both called distance that get selected automatically based on the class of the object.