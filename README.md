# DavisAggie-Hangman-Project
UC Davis AISC Aggie Intelligence Beginner Project 1 Aggie Hangman 
# DavisAggie-Hangman-Project
UC Davis AISC Aggie Intelligence Beginner Project 1 Aggie Hangman 
# UC Davis themed Hangcow (Hangman with a cow)
# Save as hangcow.py and run: python hangcow.py

import random
import string

# --- UC Davis themed words ---
WORD_BANK = [
    "aggies", "ucdavis", "davis", "quad", "shields", "memorialunion",
    "cows", "gunrock", "storer", "olson", "silo", "aggiepride",
    "coho", "dairy", "undergrad", "gradstudent", "farm", "arboretum",
    "bikepath", "coffee", "egghead", "aisc", "bike", "wellman",
    "arc", "finals", "midterm", "bikepath", "picnicday",
    "farmersmarket", "turkey", "research", "aggiepride", "giedt"
]

# --- Cow stages: from empty pasture (0) to fully 'gone wrong' cow (final) ---
COW_STAGES = [
    r"""
    
          ~ pasture ~
    """,
    r"""
            \   /
             \ /
              |
             / \
            /   \
    """,
    r"""
             (\_/)
              /|
             / |
            /  |
    """,
    r"""
             (\_/)
             (o o)
              /|
             / |
            /  |
    """,
    r"""
             (\_/)
             (o o)
             /_|\
            / | \
             / \
            /   \
    """,
    r"""
             (\_/)
             (x x)
             /_|\
            / | \
             / \
            /   \
           (spots)
    """,
    r"""
             (\_/)
             (x x)  --- oh no!
             /_|\
            / | \
             / \
            /   \
           (R.I.P)
    """
]

MAX_ATTEMPTS = len(COW_STAGES) - 1


# --- Utility functions ---
def choose_word():
    return random.choice(WORD_BANK).upper()


def display_progress(word, guessed_letters):
    displayed = []
    for ch in word:
        if not ch.isalpha():  # show spaces/punctuation
            displayed.append(ch)
        elif ch in guessed_letters:
            displayed.append(ch)
        else:
            displayed.append("_")
    return " ".join(displayed)

    def game_loop():
    word = choose_word()
    guessed = set()
    wrong_guesses = 0

    print("Welcome to UC Davis Hangcow! Guess letters to save the cow 🐮")
    print(f"You have {MAX_ATTEMPTS} wrong guesses before the cow... um, is in trouble.")
    print()

    while True:
        print(COW_STAGES[wrong_guesses])
        print("Word: ", display_progress(word, guessed))
        print("Guessed letters:", " ".join(sorted(guessed)) if guessed else "None")
        print(f"Wrong guesses left: {MAX_ATTEMPTS - wrong_guesses}")
        guess = input("Guess a letter (or full word/phrase): ").strip().upper()

        if not guess:
            print("No input — try again.")
            continue

        # If user guesses the full word/phrase
        if len(guess) > 1:
            if guess == word:
                print("\nCorrect! You saved the cow!")
                print("Word:", word)
                return True
            else:
                wrong_guesses += 1
                print("That full guess is incorrect.")
        else:
            letter = guess
            if letter not in string.ascii_uppercase:
                print("Please guess an English letter (A-Z).")
                continue

            if letter in guessed:
                print("You already guessed that letter.")
            else:
                guessed.add(letter)
                if letter not in word:
                    wrong_guesses += 1
                    print(f"No '{letter}'. The cow is getting worried...")
                else:
                    print(f"Nice! '{letter}' is in the word.")

        # Check win
        revealed = "".join([ch if (not ch.isalpha() or ch in guessed) else "_" for ch in word])
        if "_" not in revealed:
            print("\nCongratulations — you saved the cow! 🐮🎉")
            print("Word:", word)
            return True

        # Check loss
        if wrong_guesses >= MAX_ATTEMPTS:
            print(COW_STAGES[wrong_guesses])
            print("\nOh no — the cow couldn't be saved.")
            print("The word was:", word)
            return False

        print("-" * 40)


def main():
    while True:
        game_loop()
        again = input("\nPlay again? (Y/N): ").strip().upper()
        if again != "Y":
            print("Thanks for playing Hangcow — go Aggies! 🐮")
            break


if __name__ == "__main__":
    main()

