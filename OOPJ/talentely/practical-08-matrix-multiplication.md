# Practical 8: Matrix Multiplication

## Description

Multiplies two matrices if their dimensions are compatible (columns of first matrix equals rows of second matrix).

## Code

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        // Input dimensions
        int r1 = sc.nextInt();
        int c1 = sc.nextInt();
        int r2 = sc.nextInt();
        int c2 = sc.nextInt();

        // Matrix multiplication possible only if c1 == r2
        if (c1 != r2) {
            System.out.println("Matrix multiplication not possible");
            return;
        }

        int[][] A = new int[r1][c1];
        int[][] B = new int[r2][c2];
        int[][] result = new int[r1][c2];

        // Input for first matrix
        for (int i = 0; i < r1; i++) {
            for (int j = 0; j < c1; j++) {
                A[i][j] = sc.nextInt();
            }
        }

        // Input for second matrix
        for (int i = 0; i < r2; i++) {
            for (int j = 0; j < c2; j++) {
                B[i][j] = sc.nextInt();
            }
        }

        // Matrix multiplication
        for (int i = 0; i < r1; i++) {
            for (int j = 0; j < c2; j++) {
                for (int k = 0; k < c1; k++) {
                    result[i][j] += A[i][k] * B[k][j];
                }
            }
        }

        // Print result properly (no trailing space or extra newline)
        for (int i = 0; i < r1; i++) {
            for (int j = 0; j < c2; j++) {
                if (j == c2 - 1) {
                    System.out.print(result[i][j]);
                } else {
                    System.out.print(result[i][j] + " ");
                }
            }
            if (i != r1 - 1) {
                System.out.println();
            }
        }

        sc.close();
    }
}
```
