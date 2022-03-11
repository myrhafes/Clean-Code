# **Chapter 6: Objects And Data Structures**

## Data Abstraction:
Abstraction means hiding implementation. Hiding implemntation isn't means making the variables privates and using getters and setters to access these variables. Rather it means providing abstract interfaces (abstract ways) that allow its users to manipulate the data, whithout having to know its implementation.
For exemple:
```java
public interface Vehicle {
    double getFuelTankCapacityInGallons();
    double getGallonsOfGasoline();
}
```
```java
public interface Vehicle {
 double getPercentFuelRemaining();
}
```
> The following code represents Abstraction, which it does the same prupose of the previous code but with the abstraction of percentage. So, in this case you do not at all know anything about the form of the data (internal details).

## Data / Object anti-symmetry:
This section show the difference between objects and data structure.
In a simple word:
**Data structure:** show their data (be public) and hove no function.
```java
    public class Square {
    public Point topLeft;
    public double side;
    }

    public class Rectangle {
    public Point topLeft;
    public double height;
    public double width;
    }

    public class Circle {
    public Point center;
    public double radius;
    }

    public class Geometry {
        public final double PI = 3.141592653589793;
        public double area(Object shape) throws NoSuchShapeException {
            if (shape instanceof Square) {
                Square s = (Square)shape;
                return s.side * s.side;
            }
            else if (shape instanceof Rectangle) {
                Rectangle r = (Rectangle)shape;
                return r.height * r.width;
            }
            else if (shape instanceof Circle) {
                Circle c = (Circle)shape;
                return PI * c.radius * c.radius;
            }
            throw new NoSuchShapeException();
        }
    }
```
If I add a ```perimeter()``` function to ```Geometry```. The ```shape``` classes would be unaffected. On the other hand if I add a new shap (new data structure) I must change all the functions in ```Geometry```.

**Object:** hide their data (be private) and have functions to operate of that data.
```java
    public class Square implements Shape {
        private Point topLeft;
        private double side;
        public double area() {
            return side*side;
        }
    }
    public class Rectangle implements Shape {
        private Point topLeft;
        private double height;
        private double width;
        public double area() {
            return height * width;
        }
    }
    public class Circle implements Shape {
        private Point center;
        private double radius;
        public final double PI = 3.141592653589793;
        public double area() {
            return PI * radius * radius;
        }
    }
```
Here the ```area()``` function is polymorphic. No ```Geometry``` class is necessary. So if I add a new shape, none of the existing functions are affected, but if I add a new function all of the shapes must be changed.

Then, we note from the previous that the two concepts are opposites:
**Procedural code (code using data structure):**
- Make it easy to add new functions whithout changing the existing data structures.
- Make it hard to add new data structutres because all the function must change.

**OO code (code using object oriented):**
- Make it hard to add new functions because all the existing classes change.
- Make it easy to add new classes whitout changing existing functions.

> Q: When OO code is more appropriate ?
> A: In any complex system, because we will having to add more data types rather than new functions.

> Q: When procedural code is more appropriate ?
> A: When we will add new functions more rather than data types.

## The Law of Demeter:
The law of Demeter says a module should not know about the innards of the objects it manipulates. In pther words, a software component or an object should not have the knowledge of the internal working of other objects or components.
**Exemple:** More precisely, method f of a class C should only call the methods of these:
- C
- An object created by f
- An object passed as an argument to f
- An object held in an instance variable of C
> The method should not invoke methods on objects that are returned by any of the allowed functions. In other words, talk to friends, not to strangers.

### Train wrecks:
This is kind of code that violate law of Demeter:
```java
    public void (Car car) {
        printServer(car.getOwner().getAdress().getStreet());
    }
```
> The method received the parameter car, so all method calls on this object are allowed. But, calling any methods on the object returned by getOwner() is not allowed. To correct this misktake:
```java
    public void (Car car) {
        Owner owner = car.getOwner();
        Adress ownerAdress = owner.getAdress();
        Street ownerStreet = ownerAdress.getStreet();
        // ...
    }
```

## Data Transfer Objects(DTO) :
This is a form of data structure which is a class with public variables and no functions and sometimes called DTO. DTOs are very useful structures especially when communicating with database.
