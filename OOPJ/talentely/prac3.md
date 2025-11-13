
Practical:3 - Operators using object creation

public class Main {

    // ✅ Static Inner Class
    static class Operations {
        // Method to perform arithmetic and bitwise operations
        void performOperations() {
            // Arithmetic Operations
            int a = 20;
            int b = 10;

            System.out.println("Addition: " + (a + b));
            System.out.println("Subtraction: " + (a - b));
            System.out.println("Multiplication: " + (a * b));
            System.out.println("Division: " + (a / b));
            System.out.println("Remainder: " + (a % b));

            // Bitwise Operations
            int x = 12; // 1100 in binary
            int y = 6;  // 0110 in binary

            System.out.println("Bitwise OR: " + (x | y));
            System.out.println("Bitwise AND: " + (x & y));
            System.out.println("Bitwise NOT of x: " + (~x));
            System.out.println("Bitwise NOT of y: " + (~y));
            System.out.println("Bitwise XOR: " + (x ^ y));
            System.out.println("Bitwise Right Shift: " + (x >> 2));
            System.out.println("Bitwise Left Shift: " + (x << 2));
        }
    }

    public static void main(String[] args) {
        // ✅ Object creation of inner class
        Operations op = new Operations();
        op.performOperations();
    }
}
