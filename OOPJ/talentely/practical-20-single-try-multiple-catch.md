Practical: 20 - Single Try Block with Multiple Catch Blocks

public class Main {

    // Inner static helper class to demonstrate exceptions
    static class ExceptionDemo {

        void runDemo() {
            try {
                /*
                 INSTRUCTIONS:
                 1. Uncomment one of the following lines at a time to test exceptions.
                 2. Do not modify the catch blocks.
                 3. You can experiment with other expressions that may throw exceptions.
                */

                // ArithmeticException: divide by zero
                // int a = 10;
                // int b = 0;
                // int result = a / b;
                // System.out.println("Result: " + result);

                // ArrayIndexOutOfBoundsException: invalid index access
                // int[] arr = {1, 2, 3};
                // System.out.println(arr[5]);

                // Example of safe code (no exception)
                int x = 100;
                int y = 20;
                int res = x / y;
                System.out.println("Result (no exception): " + res);

            } catch (ArithmeticException e) {
                System.out.println("Caught ArithmeticException: " + e.getMessage());
            } catch (ArrayIndexOutOfBoundsException e) {
                System.out.println("Caught ArrayIndexOutOfBoundsException: " + e.getMessage());
            } catch (Exception e) {
                System.out.println("Caught general Exception: " + e.getMessage());
            }
        }
    }

    public static void main(String[] args) {
        // Create object of ExceptionDemo
        ExceptionDemo demo = new ExceptionDemo();

        // Run the demo to test exceptions
        demo.runDemo();
    }
}
