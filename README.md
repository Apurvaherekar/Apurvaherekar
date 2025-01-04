#include <stdio.h>
#include <string.h>

#define MAX_TRIES 3

// Function to check if the guessed letter is correct
int checkGuess(char word[], char guessedLetter, char revealedWord[]) {
    int correct = 0;
    for (int i = 0; i < strlen(word); i++) {
        if (word[i] == guessedLetter && revealedWord[i] == '_') {
            revealedWord[i] = guessedLetter;
            correct = 1;
        }
    }
    return correct;
}

// Function to display the current state of the word
void displayWord(char revealedWord[]) {
    for (int i = 0; i < strlen(revealedWord); i++) {
        printf("%c ", revealedWord[i]);
    }
    printf("\n");
}

int main() {
    char word[] = "cat"; // The word the player is trying to guess
    char revealedWord[] = "_ _ _"; // The word with missing letters
    char guessedLetter;
    int attemptsLeft = MAX_TRIES;
    int correctGuesses = 0;
    
    printf("Welcome to the Missing Letter Game!\n");
    printf("Guess the word: ");
    displayWord(revealedWord);

    while (attemptsLeft > 0 && correctGuesses < strlen(word)) {
        printf("You have %d attempts left. Enter a letter: ", attemptsLeft);
        scanf(" %c", &guessedLetter);

        if (checkGuess(word, guessedLetter, revealedWord)) {
            printf("Good guess!\n");
            correctGuesses++;
        } else {
            printf("Wrong guess.\n");
            attemptsLeft--;
        }

        displayWord(revealedWord);
    }

    if (correctGuesses == strlen(word)) {
        printf("Congratulations! You've guessed the word '%s'!\n", word);
    } else {
        printf("Game over! The correct word was '%s'.\n", word);
    }

    return 0;
    }
