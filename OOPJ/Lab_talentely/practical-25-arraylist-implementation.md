# Practical 25: Dynamic Array Implementation Using ArrayList

## Description

Demonstrates the implementation of a dynamic array using ArrayList to store and display integers.

## Code

```java
import java.util.ArrayList;
import java.util.Scanner;

public class Main {

    // Inner helper class for Dynamic Array
    static class DynamicArray {
        private ArrayList<Integer> list;

        DynamicArray() {
            list = new ArrayList<>();
        }

        void addElement(int value) {
            list.add(value);
        }

        void printElements() {
            for (int num : list) {
                System.out.print(num + " ");
            }
            System.out.println();
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt(); // number of elements
        DynamicArray da = new DynamicArray();

        for (int i = 0; i < n; i++) {
            da.addElement(sc.nextInt());
        }

        da.printElements();
        sc.close();
    }
}
```
