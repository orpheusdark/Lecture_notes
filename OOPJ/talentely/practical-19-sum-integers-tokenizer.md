# Practical 19: Sum of Integers using StringTokenizer

## Description

Demonstrates the use of StringTokenizer to parse and sum integers from a space-separated input string.

## Code

```java
import java.util.Scanner;
import java.util.StringTokenizer;

public class Main {

    // Inner static helper class
    static class IntegerProcessor {
        private String input;

        IntegerProcessor(String input) {
            this.input = input;
        }

        void processAndDisplay() {
            StringTokenizer st = new StringTokenizer(input);
            int sum = 0;

            while (st.hasMoreTokens()) {
                int num = Integer.parseInt(st.nextToken());
                System.out.println(num);
                sum += num;
            }

            System.out.println("Sum: " + sum);
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String line = sc.nextLine(); // Read full line of integers

        IntegerProcessor processor = new IntegerProcessor(line);
        processor.processAndDisplay();
    }
}
```
