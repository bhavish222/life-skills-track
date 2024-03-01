# S.O.L.I.D Principle

## Single Responsibility Principle (SRP)
The Single Responsibility Principle (SRP) states that a class should have only one reason to change. It's important because multiple teams working on the same class for different reasons can lead to incompatible modules. SRP facilitates easier version control and reduces merge conflicts by ensuring each file has a single responsibility.
Let's understand it by an  simple example : 

The first SOLID principle prohibits creating "God" classes. A "God" class does everything. We can't allow a class in our code to have too many responsibilities.
Here's a Java code snippet. Take a look at the Point class: 

```java
class Point {
private int x;
private int y;
  
public Point(int x, int y) {
    this.x = x;
    this.y = y;
}
  
public int getX() {
    return x;
}
  
public int getY() {
    return y;
}
  
public void draw() {
    System.out.printf("x = %d, y = %d \n", this.x, this.y);
    }
}
```

 The Point class stores information about a point and is responsible for drawing it. Notice that at this stage, the class already has too many responsibilities. We'll try to split our class into two, making them flexible and independent.

We split the Point class in line with the SRP:

```java
class Point {
private int x;
private int y;
  
public Point(int x, int y) {
    this.x = x;
    this.y = y;
}
  
public int getX() {
    return x;
}
  
public int getY() {
    return y;
    }
}
  
class PointDrawer {
  
public void draw(Point point) {
    System.out.printf("x = %d, y = %d \n", point.getX(), point.getY());
    }
}
```
We've adhered to the first SOLID principle by splitting the Point class into Point and PointDrawer. The Point class handles points, while the PointDrawer class is responsible for displaying points. 

## Open-Closed Principle (OSP)
The Open-Closed Principle (OCP) requires classes to be open for extension and closed for modification. It allows adding new functionality without altering existing code, minimizing the risk of introducing bugs. Interfaces and abstract classes facilitate adhering to this principle.

Example :
```java
class Triangle {
public void calculateArea() {
    System.out.println("triangle - calculate area");
    }
}
  
class Square {
    public void calculateArea() {
       System.out.println("square - calculate area");
    }
}
  
class AreaCalculator {
    public static void calculate(Object shape) {
        if(shape instanceof Triangle) {
          ((Triangle) shape).calculateArea();
        } else if(shape instanceof Square) {
          ((Square) shape).calculateArea();
        }
    }
}
```
The code presented here violates the Open/Closed Principle.
Consider the correct implementation: 
```java
abstract class Shape {
abstract public void calculateArea();
}
  
class Triangle extends Shape {
    public void calculateArea() {
       System.out.println("triangle - calculate area");
    }
}
  
class Square extends Shape {
    public void calculateArea() {
       System.out.println("square - calculate area");
    }
}
  
class AreaCalculator {
    public static void calculate(Shape shape) {
       shape.calculateArea();
    }
}
```

## Liskov Substitution Principle (LSP)
The Liskov Substitution Principle (LSP) ensures that objects of a superclass can be replaced by objects of its subclass without altering program behavior. It enables seamless substitution of objects, maintaining program consistency.

Take a look at the provided code:
```java
class CoffeeMachine {
public void makeCoffee() {
    this.prepareCoffee();
}
  
public void prepareCoffee() {
    System.out.println("Prepare coffee");
    }
}
  
class SugarCoffeeMachine extends CoffeeMachine {
    public void makeCoffee() {
       System.out.println("Add sugar");
    }
}
```
The above code, as mentioned, violates the Liskov Substitution Principle.
 A corrected implementation could be:
 
```java
class CoffeeMachine {
public void makeCoffee() {
    this.prepareCoffee();
}
  
public void prepareCoffee() {
    System.out.println("Prepare coffee");
    }
}
  
class SugarCoffeeMachine extends CoffeeMachine {
    public void makeCoffee() {
        super.makeCoffee();
        System.out.println("Add sugar");
    }
}
```

## Interface Segregation Principle (ISP)
The Interface Segregation Principle (ISP) advocates for clients not to be forced to implement interfaces they don't use. It promotes cohesive interfaces to prevent interface pollution and unnecessary dependencies.

Example :
```java
interface Printer {
    void toPdf();
    void toCsv();
    void toXls();
}
  
class GeneralPrinter implements Printer {
    @Override
    public void toPdf() {
       System.out.println("Print pdf");
    }
  
    @Override
    public void toCsv() {
    }
  
    @Override
    public void toXls() {
    }
}
```
The example provided initially breaks the fourth SOLID principle.
In the corrected version applying ISP:

```java
interface PdfPrinter {
    void toPdf();
}
  
interface CsvPrinter {
    void toCsv();
}
  
interface XlsPrinter {
    void toXls();
}
  
class GeneralPrinter implements PdfPrinter {
    @Override
    public void toPdf() {
       System.out.println("Print pdf");
    }
}
```

## Dependency Inversion Principle (DIP)
The Dependency Inversion Principle (DIP) suggests that high-level modules should not depend on low-level modules, but both should depend on abstractions. It decouples modules, promoting flexibility and easier maintenance.
Examle : 
```java
class Runner {
public void training() {
    }
}
  
class Coach {
    private Runner runner;
  
    public Coach(Runner runner) {
       this.runner = runner;
    }
  
    public void manageSportsman() {
       this.runner.training();
    }
}
```
Corrected implementations should be like this:
```java
abstract class Sportsman {
    abstract void training();
}
  
class Runner extends Sportsman {
    public void training() {
    }
}
  
class Coach {
    private Sportsman sportsman;
  
    public Coach(Sportsman sportsman) {
       this.sportsman = sportsman;
    }
  
    public void manageSportsman() {
       this.sportsman.training();
    }
}
```

## References

1. [SOLID Principles on Wikipedia](https://en.wikipedia.org/wiki/SOLID) - Wikipedia provides a detailed overview of the SOLID principles, including explanations of each principle and their importance in software development.

2. [SOLID Principles by Microsoft Docs](https://docs.microsoft.com/en-us/dotnet/architecture/modern-web-apps-azure/architectural-principles) - Microsoft Docs provides a comprehensive guide to SOLID principles, including code examples and practical explanations.

3. [SOLID Principles by Uncle Bob](https://blog.cleancoder.com/uncle-bob/2014/05/08/SingleReponsibilityPrinciple.html) - Articles written by Robert C. Martin (Uncle Bob) himself provide valuable insights into SOLID principles.

Hope by this you'll get good idea of SOLID principles. This references will also help you get the point and also, Its way too nice if you try to implement it by yourself. Understanding and applying these principles can assist programmers in designing more flexible and easier-to-maintain source code. 
