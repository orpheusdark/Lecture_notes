Practical:4 - Scanner Class

import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        // Taking inputs
        int empId = sc.nextInt();
        sc.nextLine();  // consume leftover newline
        String empName = sc.nextLine();
        String department = sc.nextLine();
        double salary = sc.nextDouble();

        // Displaying output
        System.out.println("Employee ID : " + empId);
        System.out.println("Employee Name : " + empName);
        System.out.println("Department : " + department);
        System.out.println("Salary : " + salary);

        sc.close();
    }
}
