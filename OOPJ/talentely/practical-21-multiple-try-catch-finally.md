
Practical: 21 - Multiple Try Blocks with Multiple Catch Blocks and Finally

/*How Students Should Use It
Open the try blocks.
Uncomment lines to generate exceptions and observe which catch block executes.
Notice that the finally block always executes regardless of exception.
Modify values to see normal execution without exceptions.*/

public class Main {

    // Inner static helper class to demonstrate multiple try-catch-finally
    static class MultiTryDemo {

        void runDemo() {

            // FIRST TRY BLOCK
            try {
                /*
                 INSTRUCTIONS:
                 1. Uncomment the line below to test ArithmeticException.
                 2. You can also leave it commented to see normal execution.
                 */
                //int a = 10 / 0; // ArithmeticException

                // Safe execution example
                int a = 20 / 2;
                System.out.println("Result of first try: " + a);

            } catch (ArithmeticException e) {
                System.out.println("Caught ArithmeticException: " + e.getMessage());
            } catch (Exception e) {
                System.out.println("Caught general Exception: " + e.getMessage());
            } finally {
                System.out.println("Finally block executed for first try");
            }

            // SECOND TRY BLOCK
            try {
                /*
                 INSTRUCTIONS:
                 1. Uncomment the line below to test ArrayIndexOutOfBoundsException.
                 2. You can also leave it commented to see normal execution.
                 */
                 //int[] arr = {1, 2, 3};
                 //System.out.println(arr[5]); // ArrayIndexOutOfBoundsException

                // Safe execution example
                int[] arr = {1, 2, 3};
                System.out.println("Result of second try: " + arr[1]);

            } catch (ArrayIndexOutOfBoundsException e) {
                System.out.println("Caught ArrayIndexOutOfBoundsException: " + e.getMessage());
            } catch (Exception e) {
                System.out.println("Caught general Exception: " + e.getMessage());
            } finally {
                System.out.println("Finally block executed for second try");
            }
        }
    }

    public static void main(String[] args) {
        // Create object of MultiTryDemo
        MultiTryDemo demo = new MultiTryDemo();

        // Run the demo
        demo.runDemo();
    }
}
