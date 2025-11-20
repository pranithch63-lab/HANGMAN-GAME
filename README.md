import java.util.*;

public class Hangman {
    public static void main(String[] args) {
        // Predefined list of 5 words
        String[] words = {"apple", "tiger", "house", "robot", "music"};

        // Pick a random word
        Random rand = new Random();
        String chosenWord = words[rand.nextInt(words.length)];

        // Convert word to char array
        char[] wordArray = chosenWord.toCharArray();
        char[] displayArray = new char[wordArray.length];

        // Fill display with underscores
        Arrays.fill(displayArray, '_');

        int incorrectGuesses = 0;
        final int MAX_GUESSES = 6;

        Scanner scanner = new Scanner(System.in);
        List<Character> guessedLetters = new ArrayList<>();

        System.out.println("=== Hangman Game ===");

        while (incorrectGuesses < MAX_GUESSES) {
            System.out.println("\nWord: " + String.valueOf(displayArray));
            System.out.println("Incorrect guesses: " + incorrectGuesses + "/" + MAX_GUESSES);
            System.out.print("Guess a letter: ");

            char guess = scanner.next().toLowerCase().charAt(0);

            // Check if already guessed
            if (guessedLetters.contains(guess)) {
                System.out.println("You already guessed that letter!");
                continue;
            }

            guessedLetters.add(guess);

            boolean found = false;

            // Reveal letters
            for (int i = 0; i < wordArray.length; i++) {
                if (wordArray[i] == guess) {
                    displayArray[i] = guess;
                    found = true;
                }
            }

            if (!found) {
                incorrectGuesses++;
                System.out.println("Wrong guess!");
            } else {
                System.out.println("Good guess!");
            }

            // Check if the player won
            if (String.valueOf(displayArray).equals(chosenWord)) {
                System.out.println("\n🎉 You won! The word was: " + chosenWord);
                return;
            }
        }

        // Player loses
        System.out.println("\n❌ You lost! The word was: " + chosenWord);
    }
}
