# Online-Quiz-Management
import java.util.Scanner;

public class Main {

    // Question class inside Main for compatibility with online compilers
    static class Question {
        String questionText;
        String[] options;
        char correctAnswer;

        Question(String questionText, String[] options, char correctAnswer) {
            this.questionText = questionText;
            this.options = options;
            this.correctAnswer = Character.toUpperCase(correctAnswer);
        }

        void display() {
            System.out.println("\n" + questionText);
            for (String opt : options) {
                System.out.println(opt);
            }
        }

        boolean isCorrect(char userAnswer) {
            return Character.toUpperCase(userAnswer) == correctAnswer;
        }
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Greet user
        System.out.print("Enter your name: ");
        String name = scanner.nextLine();

        // Create quiz questions
        Question[] questions = {
            new Question("1. Which language is platform independent?",
                new String[]{"A) C", "B) C++", "C) Java", "D) Python"}, 'C'),
            new Question("2. What hides internal details of an object?",
                new String[]{"A) Encapsulation", "B) Inheritance", "C) Polymorphism", "D) Abstraction"}, 'D'),
            new Question("3. Which keyword is used to inherit a class in Java?",
                new String[]{"A) extends", "B) implements", "C) import", "D) inherits"}, 'A'),
            new Question("4. What is the default value of a boolean in Java?",
                new String[]{"A) true", "B) false", "C) 0", "D) null"}, 'B'),
            new Question("5. Which one is not a Java keyword?",
                new String[]{"A) static", "B) void", "C) Integer", "D) private"}, 'C')
        };

        int score = 0;

        System.out.println("\nWelcome, " + name + "! Let's begin the quiz:");

        // Loop through questions
        for (Question q : questions) {
            q.display();
            char userAnswer = getAnswer(scanner);
            if (q.isCorrect(userAnswer)) {
                System.out.println("✅ Correct!");
                score++;
            } else {
                System.out.println("❌ Incorrect. Correct answer: " + q.correctAnswer);
            }
        }

        // Show result
        System.out.println("\n🎉 Quiz Completed!");
        System.out.println("👤 Name: " + name);
        System.out.println("📊 Score: " + score + "/" + questions.length);
        if (score >= 3) {
            System.out.println("🏆 Result: Passed");
        } else {
            System.out.println("❌ Result: Failed");
        }

        scanner.close();
    }

    // Method to safely get user answer
    public static char getAnswer(Scanner scanner) {
        while (true) {
            System.out.print("Enter your answer (A-D): ");
            String input = scanner.next().trim().toUpperCase();
            if (input.length() == 1 && input.charAt(0) >= 'A' && input.charAt(0) <= 'D') {
                return input.charAt(0);
            } else {
                System.out.println("⚠️ Invalid input. Please enter A, B, C, or D.");
            }
        }
    }
}
