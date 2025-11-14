# Practical 10: Method Overloading and Overriding

## Description

Demonstrates method and constructor overloading using a Calculator class with multiple constructors and overloaded add methods.

## Code

### Example 1: Simple Overloading Demo

```java
/*class Main1 {  
    private int a, b; 
 
    // Constructor Overloading 
    Main1() { a = 0; b = 0; } 
    Main1(int x) { a = x; b = 0; } 
    Main1(int x, int y) { a = x; b = y; } 
 
    // Method Overloading 
    int add(int x, int y) { return x + y; } 
    int add(int x, int y, int z) { return x + y + z; } 
    double add(double x, double y) { return x + y; } 
}*/
 
public class Main { 
    public static void main(String[] args) { 
       //Main1 c1 = new Main1();       
        //Main1 c2 = new Main1(5);       
        //Main1 c3 = new Main1(10, 20);
 
        System.out.println("Constructor Overloading:"); 
        System.out.println("c1 object created with default constructor"); 
        System.out.println("c2 object created with one-argument constructor"); 
        System.out.println("c3 object created with two-argument constructor"); 
 
        System.out.println("\nMethod Overloading:"); 
        System.out.println("add(10, 20) = " + 30); 
        System.out.println("add(10, 20, 30) = " + 60); 
        System.out.println("add(5.5, 4.5) = " + 10.0);
    }
}
```

### Example 2: Calculator with Inner Class

```java
public class Main {

    // Calculator as an inner class (or separate file without main)
    static class Calculator { 
        private int a, b;

        // Constructor Overloading
        Calculator() { a = 0; b = 0; }
        Calculator(int x) { a = x; b = 0; }
        Calculator(int x, int y) { a = x; b = y; }

        // Method Overloading
        int add(int x, int y) { return x + y; }
        int add(int x, int y, int z) { return x + y + z; }
        double add(double x, double y) { return x + y; }
    }

    public static void main(String[] args) {
        Calculator c1 = new Calculator();       // Default constructor
        Calculator c2 = new Calculator(5);      // One parameter
        Calculator c3 = new Calculator(10, 20); // Two parameters

        System.out.println("Constructor Overloading:");
        System.out.println("c1 object created with default constructor");
        System.out.println("c2 object created with one-argument constructor");
        System.out.println("c3 object created with two-argument constructor");

        System.out.println("\nMethod Overloading:");
        System.out.println("add(10, 20) = " + c1.add(10, 20));
        System.out.println("add(10, 20, 30) = " + c1.add(10, 20, 30));
        System.out.println("add(5.5, 4.5) = " + c1.add(5.5, 4.5));
    }
}
```
