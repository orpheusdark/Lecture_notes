# Practical 26: ArrayList Operations - Add, Search, and Remove

## Description

Demonstrates essential ArrayList operations including adding elements, searching for values, and removing elements.

## Code

```java
import java.util.ArrayList;
import java.util.Scanner;

public class Main {

    // Inner helper class to manage ArrayList operations
    static class ArrayListManager {
        private ArrayList<Integer> list;

        ArrayListManager() {
            list = new ArrayList<>();
        }

        // Add element to ArrayList
        void addElement(int value) {
            list.add(value);
        }

        // Search for an element
        boolean searchElement(int value) {
            return list.contains(value);
        }

        // Remove an element
        boolean removeElement(int value) {
            return list.remove((Integer) value); // cast to Integer to remove object, not index
        }

        // Print current elements
        void printElements(String message) {
            System.out.println(message + list);
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        ArrayListManager manager = new ArrayListManager();

        // Read number of elements to add
        int n = sc.nextInt();
        for (int i = 0; i < n; i++) {
            int num = sc.nextInt();
            manager.addElement(num);
        }

        manager.printElements("After adding elements: ");

        // Read element to search
        int x = sc.nextInt();
        System.out.println("Search " + x + ": " + (manager.searchElement(x) ? "Found" : "Not Found"));

        // Read element to remove
        int y = sc.nextInt();
        System.out.println("Removing " + y + ": " + (manager.removeElement(y) ? "Removed" : "Not Found"));

        manager.printElements("After removals: ");

        sc.close();
    }
}
```
