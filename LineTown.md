import java.util.Scanner;

public class LineTown {
    public static void main(String[] args) {
        Scanner s = new Scanner(System.in);

        // Ask the user to enter N
        System.out.print("Enter N value: ");
        int N = s.nextInt();

        int[] happiness = new int[N];

        // Ask the user to enter happiness values
        System.out.print("Enter happiness values separated by spaces: ");
        for (int i = 0; i < N; i++) {
            happiness[i] = s.nextInt();
        }

        System.out.println(minSwaps(N, happiness));
    }

    public static int minSwaps(int N, int[] happiness) {
        int total = 0;

        for (int i = 0; i < N - 1; i++) {
            int maxIndex = i;

            // Find the index of the max element
            for (int j = i + 1; j < N; j++) {
                if (happiness[j] > happiness[maxIndex]) {
                    maxIndex = j;
                }
                // Return -1 if we have a value more than once
                if(happiness[j] == happiness[maxIndex]){
                    return -1;
                }

            }

            // Swap the max element to the end of the array
            int temp = happiness[maxIndex];
            happiness[maxIndex] = happiness[N - 1];
            happiness[N - 1] = temp;

            // If the max element is not at the end, increment total
            if (maxIndex != N - 1) {
                total++;
            }

            // Recursively call minSwaps on the remaining array
            total += minSwaps(N - 1, happiness);
        }

        return total;
    }
}
