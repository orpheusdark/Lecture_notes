# Practical 11: Abstract Class

## Description

Demonstrates the use of abstract classes by creating a Shape abstract class with Rectangle and Circle as concrete implementations.

## Code

```java
import java.util.Scanner;

public class Main {

    // Abstract class Shape
    static abstract class Shape {
        abstract double area();
        abstract double perimeter();
    }

    // Inner static class Rectangle
    static class Rectangle extends Shape {
        int length, breadth;

        Rectangle(int length, int breadth) {
            this.length = length;
            this.breadth = breadth;
        }

        @Override
        double area() {
            return length * breadth;
        }

        @Override
        double perimeter() {
            return 2 * (length + breadth);
        }
    }

    // Inner static class Circle
    static class Circle extends Shape {
        int radius;

        Circle(int radius) {
            this.radius = radius;
        }

        @Override
        double area() {
            return Math.PI * radius * radius;
        }

        @Override
        double perimeter() {
            return 2 * Math.PI * radius;
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        // Input for Rectangle
        int length = sc.nextInt();
        int breadth = sc.nextInt();

        // Input for Circle
        int radius = sc.nextInt();

        // Create objects
        Rectangle rect = new Rectangle(length, breadth);
        Circle circ = new Circle(radius);

        // Print Rectangle results
        System.out.printf("Rectangle Area: %.0f%n", rect.area());
        System.out.printf("Rectangle Perimeter: %.0f%n", rect.perimeter());

        // Print Circle results with 2 decimal places
        System.out.printf("Circle Area: %.2f%n", circ.area());
        System.out.printf("Circle Perimeter: %.2f%n", circ.perimeter());

        sc.close();
    }
}
```
