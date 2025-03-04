# 37.Streams-and-files
37.Stream and files


package streamandfiles;

import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;
import java.util.List;
import java.util.stream.Collectors;

public class StreamAndFile {
    public static void main(String[] args) {
        // Define file paths
        String inputFilePath = "C:\\Users\\1BSCCSA43\\Documents\\input_numbers.txt";
        String outputFilePath = "C:\\Users\\1BSCCSA43\\Documents\\output_squares.txt";

        try {
            // Read numbers from the input file
            List<Integer> numbers = readNumbersFromFile(inputFilePath);

            // Square each number using Stream API
            List<Integer> squares = numbers.stream()
                .map(num -> num * num) // Squaring each number
                .collect(Collectors.toList());

            // Print squares to console
            System.out.println("Squares:");
            squares.forEach(System.out::println);

            // Write squared numbers to the output file
            writeSquaresToFile(outputFilePath, squares);
            System.out.println("Squares written to " + outputFilePath);
        } catch (IOException e) {
            // If there's an IOException, print the stack trace
            e.printStackTrace();
        }
    }

    // Method to read numbers from the input file
    private static List<Integer> readNumbersFromFile(String filePath) throws IOException {
        try (BufferedReader reader = new BufferedReader(new FileReader(filePath))) {
            return reader.lines() // Read lines
                .map(Integer::parseInt) // Convert each line to an integer
                .collect(Collectors.toList()); // Collect into a List
        }
    }

    // Method to write squared numbers to the output file
    private static void writeSquaresToFile(String filePath, List<Integer> squares) throws IOException {
        try (BufferedWriter writer = new BufferedWriter(new FileWriter(filePath))) {
            for (Integer square : squares) {
                writer.write(square.toString()); // Write the squared number as a string
                writer.newLine(); // Add a newline after each square
            }
        }
    }
}

Output
(save as input_numbers)
Squares:
1
4
9
16
25
Squares written to C:\Users\1BSCCSA43\Documents\output_squares.txt
