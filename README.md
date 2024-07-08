# Java_Intern_Task
Task 1 - Online Quiz Application
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

class Question {
    private String questionText;
    private List<String> options;
    private int correctAnswer;

    public Question(String questionText, List<String> options, int correctAnswer) {
        this.questionText = questionText;
        this.options = options;
        this.correctAnswer = correctAnswer;
    }

    public String getQuestionText() {
        return questionText;
    }

    public List<String> getOptions() {
        return options;
    }

    public int getCorrectAnswer() {
        return correctAnswer;
    }
}

public class Quiz {
    private List<Question> questionBank;
    private int score;

    public Quiz(List<Question> questionBank) {
        this.questionBank = questionBank;
        this.score = 0;
    }

    public void startQuiz() {
        Scanner scanner = new Scanner(System.in);
        for (Question question : questionBank) {
            System.out.println(question.getQuestionText());
            List<String> options = question.getOptions();
            for (int i = 0; i < options.size(); i++) {
                System.out.println((i + 1) + ". " + options.get(i));
            }

            int userAnswer = getUserInput(scanner, options.size());
            checkAnswerAndUpdateScore(userAnswer, question, options);
        }

        System.out.println("Your final score: " + score + "/" + questionBank.size());
    }

    private int getUserInput(Scanner scanner, int maxOptions) {
        int userAnswer = -1;
        boolean isValidInput = false;

        while (!isValidInput) {
            try {
                System.out.print("Enter your answer (1-" + maxOptions + "): ");
                userAnswer = scanner.nextInt();

                if (userAnswer >= 1 && userAnswer <= maxOptions) {
                    isValidInput = true;
                } else {
                    System.out.println("Invalid input. Please enter a number between 1 and " + maxOptions);
                }
            } catch (java.util.InputMismatchException e) {
                System.out.println("Invalid input. Please enter a number.");
                scanner.next(); // consume the invalid input to prevent an infinite loop
            }
        }

        return userAnswer;
    }

    private void checkAnswerAndUpdateScore(int userAnswer, Question question, List<String> options) {
        if (userAnswer - 1 == question.getCorrectAnswer()) {
            System.out.println("Correct!");
            score++;
        } else {
            System.out.println("Incorrect! The correct answer was: " + options.get(question.getCorrectAnswer()));
        }
    }

    public static void main(String[] args) {
        List<Question> questionBank = new ArrayList<>();
        // Add your questions here
        questionBank.add(new Question("What is the capital of France?", List.of("Paris", "Madrid", "Berlin"), 0));
        questionBank.add(new Question("Which planet is known as the Red Planet?", List.of("Earth", "Mars", "Venus"), 1));
        // Add more questions...

        Quiz quiz = new Quiz(questionBank);
        quiz.startQuiz();
    }
}


