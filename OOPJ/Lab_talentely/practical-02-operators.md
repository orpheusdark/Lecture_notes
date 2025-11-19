# Practical 2: Operators

## Description

Demonstrates various operators in Java including:
- Arithmetic operators (addition, subtraction, multiplication, division, modulus)
- Bitwise operators (OR, AND, NOT, XOR, shift operations)

## Code

```java
public class Main {
    public static void main(String[] args) {
        // Arithmetic operators
        int a = 20;
        int b = 10;

        System.out.println("Addition: " + (a + b));
        System.out.println("Subtraction: " + (a - b));
        System.out.println("Multiplication: " + (a * b));
        System.out.println("Division: " + (a / b));
        System.out.println("Remainder: " + (a % b));

        // Bitwise operators
        int x = 12; 
        int y = 6;  

        System.out.println("Bitwise OR: " + (x | y));
        System.out.println("Bitwise AND: " + (x & y));
        System.out.println("Bitwise NOT of x: " + (~x));
        System.out.println("Bitwise NOT of y: " + (~y));
        System.out.println("Bitwise XOR: " + (x ^ y));
        System.out.println("Bitwise Right Shift: " + (x >> 2));
        System.out.println("Bitwise Left Shift: " + (x << 2));
    }
}
```
