Practical-13 - Method Overriding and Use of super (with Inner Static Classes)

public class Main {

    // Parent class as inner static class
    static class Animal {
        void sound() {
            System.out.println("Animal makes a sound");
        }
    }

    // Child class as inner static class, overriding method
    static class Dog extends Animal {
        @Override
        void sound() {
            super.sound(); // calling parent class method
            System.out.println("Dog barks");
        }
    }

    public static void main(String[] args) {
        Dog d = new Dog();
        d.sound();
    }
}
