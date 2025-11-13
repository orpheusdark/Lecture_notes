Practical: 6 - Practical: 6 - Nth Term of Fibonacci Series (Recursion & Iteration)
import java.util.Scanner;

public class Main {

    // Recursive function
    public static int fibRecursive(int n) {
        if (n == 1 || n == 2) {
            return 1;
        }
        return fibRecursive(n - 1) + fibRecursive(n - 2);
    }

    // Iterative function
    public static int fibIterative(int n) {
        if (n == 1 || n == 2) {
            return 1;
        }
        int a = 1, b = 1, c = 0;
        for (int i = 3; i <= n; i++) {
            c = a + b;
            a = b;
            b = c;
        }
        return b;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();

        // Recursive result
        int resultRec = fibRecursive(n);

        // Iterative result
        int resultIter = fibIterative(n);

        System.out.println("Recursive: " + resultRec);
        System.out.println("Iterative: " + resultIter);

        sc.close();
    }
}
