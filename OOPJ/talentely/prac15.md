Practical:15 - Demonstrate Inner Classes in Java
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
