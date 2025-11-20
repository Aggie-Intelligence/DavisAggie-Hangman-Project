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

