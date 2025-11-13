Practical: 9 - Sorting the names in ascending order.

import java.util.Scanner;
import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        // Input number of names
        int n = sc.nextInt();
        sc.nextLine(); // consume the newline

        String[] names = new String[n];

        // Input names
        for (int i = 0; i < n; i++) {
            names[i] = sc.nextLine();
        }

        // Sort names in ascending order
        Arrays.sort(names);

        // Print sorted names
        for (int i = 0; i < n; i++) {
            System.out.println(names[i]);
        }

        sc.close();
    }
}
