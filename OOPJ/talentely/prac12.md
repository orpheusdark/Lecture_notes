Practical-12 - overriding and super keyword.

public class Main {

    // Interface Animal
    interface Animal {
        void eat();
    }

    // Interface Pet
    interface Pet {
        void play();
    }

    // Inner static class Dog implementing both interfaces
    static class Dog implements Animal, Pet {
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
