```java
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

public class Quiz {
    private List<Question> questions;
    private int score;

    public Quiz(List<Question> questions) {
        this.questions = questions;
        this.score = 0;
    }

    public void takeQuiz() {
        Scanner scanner = new Scanner(System.in);
        for (Question question : questions) {
            System.out.println(question.getQuestionText());
            for (int i = 0; i < question.getOptions().size(); i++) {
                System.out.println((i + 1) + ". " + question.getOptions().get(i));
            }
            System.out.print("Enter your answer (1-" + question.getOptions().size() + "): ");
            String userAnswer = scanner.nextLine();
            if (isValidInput(userAnswer)) {
                int answerIndex = Integer.parseInt(userAnswer) - 1;
                if (question.getOptions().get(answerIndex).equals(question.getCorrectAnswer())) {
                    score++;
                }
            } else {
                System.out.println("Invalid input. Skipping this question.");
            }
        }
    }

    public void displayScore() {
        System.out.println("Your score: " + score + "/" + questions.size());
    }

    private boolean isValidInput(String input) {
        try {
            int answerIndex = Integer.parseInt(input);
            return answerIndex >= 1 && answerIndex <= questions.get(0).getOptions().size();
        } catch (NumberFormatException e) {
            return false;
        }
    }

    public static void main(String[] args) {
        List<Question> questions = new ArrayList<>();
        questions.add(new Question("What is the capital of India?", List.of("Delhi", "Mumbai", "Kolkata", "Chennai"), "Delhi"));
        questions.add(new Question("Which planet is known as the Red Planet?", List.of("Mars", "Venus", "Jupiter", "Saturn"), "Mars"));
        questions.add(new Question("Who painted the Mona Lisa?", List.of("Leonardo da Vinci", "Pablo Picasso", "Vincent van Gogh", "Michelangelo"), "Leonardo da Vinci"));

        Quiz quiz = new Quiz
