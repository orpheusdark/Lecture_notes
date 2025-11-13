Practical:5 - Conditional Statements

import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        // Input coefficients
        int a = sc.nextInt();
        int b = sc.nextInt();
        int c = sc.nextInt();

        // Calculate discriminant
        int discriminant = b * b - 4 * a * c;

        if (discriminant > 0) {
            double x1 = (-b + Math.sqrt(discriminant)) / (2.0 * a);
            double x2 = (-b - Math.sqrt(discriminant)) / (2.0 * a);
            System.out.printf("The equation has two real solutions: x1 = %.2f, x2 = %.2f%n", x1, x2);
        } else if (discriminant == 0) {
            double x = -b / (2.0 * a);
            System.out.printf("The equation has one real solution: x = %.2f%n", x);
        } else {
            System.out.println("The equation has no real solutions.");
        }

        sc.close();
    }
}
