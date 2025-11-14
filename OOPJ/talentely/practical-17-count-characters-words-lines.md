
Practical: 17 - Count Characters, Words, and Lines in a Text

import java.util.Scanner;

public class Main {

    // Helper class for text statistics
    static class TextStats {
        private String text;

        TextStats(String text) {
            this.text = text;
        }

        int countCharacters() {
            return text.length();
        }

        int countWords() {
            if (text.trim().isEmpty()) return 0;
            return text.trim().split("\\s+").length;
        }

        int countLines() {
            if (text.isEmpty()) return 0;
            return text.split("\r\n|\r|\n").length;
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        StringBuilder sb = new StringBuilder();

        while (sc.hasNextLine()) {
            String line = sc.nextLine();
            if (line.trim().isEmpty()) break;
            sb.append(line).append("\n");
        }

        // remove trailing newline
        String inputText = sb.toString().stripTrailing();
        TextStats stats = new TextStats(inputText);

        System.out.println("Number of characters: " + stats.countCharacters());
        System.out.println("Number of words: " + stats.countWords());
        System.out.println("Number of lines: " + stats.countLines());
    }
}
