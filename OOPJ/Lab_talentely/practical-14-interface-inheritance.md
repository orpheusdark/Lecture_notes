# Practical 14: Interface Inheritance using extends

## Description

Demonstrates interface inheritance where one interface extends another, and a class implements the child interface.

## Code

```java
public class Main {

    // Parent interface
    interface Animal {
        void eat();
    }

    // Child interface extending Animal
    interface Pet extends Animal {
        void play();
    }

    // Class Dog implementing Pet
    static class Dog implements Pet {
        @Override
        public void eat() {
            System.out.println("Dog is eating");
        }

        @Override
        public void play() {
            System.out.println("Dog is playing");
        }
    }

    public static void main(String[] args) {
        Dog d = new Dog();
        d.eat();
        d.play();
    }
}
```
