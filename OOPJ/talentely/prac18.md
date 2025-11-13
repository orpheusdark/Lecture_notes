Practical: 18 - Palindrome Checker

import java.util.Scanner;

public class Main {

    // Inner static helper class
    static class PalindromeChecker {
        private String text;

        PalindromeChecker(String text) {
            this.text = text;
        }

        boolean isPalindrome() {
            // Remove spaces and make lowercase
            String cleaned = text.replaceAll("\\s+", "").toLowerCase();
            int left = 0, right = cleaned.length() - 1;

            while (left < right) {
                if (cleaned.charAt(left) != cleaned.charAt(right)) {
                    return false;
                }
                left++;
                right--;
            }
            return true;
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String input = sc.nextLine();   // Read input string

        PalindromeChecker checker = new PalindromeChecker(input);

        if (checker.isPalindrome()) {
            System.out.println(input + " is a palindrome.");
        } else {
            System.out.println(input + " is not a palindrome.");
        }
    }
}
