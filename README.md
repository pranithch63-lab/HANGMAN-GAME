import random

# List of 5 predefined words
words = ["apple", "tiger", "house", "robot", "music"]

# Randomly pick a word
chosen_word = random.choice(words)

# Create display list with underscores
display = ["_"] * len(chosen_word)

incorrect_guesses = 0
MAX_GUESSES = 6
guessed_letters = []

print("=== Hangman Game ===")

while incorrect_guesses < MAX_GUESSES:
    print("\nWord:", " ".join(display))
    print("Incorrect guesses:", incorrect_guesses, "/", MAX_GUESSES)

    guess = input("Guess a letter: ").lower()

    # Validate single letter input
    if len(guess) != 1 or not guess.isalpha():
        print("Please enter a single letter.")
        continue

    # Check if already guessed
    if guess in guessed_letters:
        print("You already guessed that letter!")
        continue

    guessed_letters.append(guess)

    # Check if letter exists in word
    if guess in chosen_word:
        print("Good guess!")
        for i, char in enumerate(chosen_word):
            if char == guess:
                display[i] = guess
    else:
        print("Wrong guess!")
        incorrect_guesses += 1

    # Check win condition
    if "_" not in display:
        print("\n🎉 You won! The word was:", chosen_word)
        break

# Lose condition
if incorrect_guesses == MAX_GUESSES:
    print("\n❌ You lost! The word was:", chosen_word)
