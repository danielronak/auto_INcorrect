# auto_INcorrect
A package to intentionally introduce human-like errors into text
It's a "spell-checker-in-reverse" that, instead of fixing mistakes, artfully creates them.

The Idea:

This isn't just random chaos. It's a sophisticated system built on a simple, but (if I do say so myself) pretty smart idea: what if, to test how good a "fixer" is, we first built the perfect "breaker"?

By simulating how humans make real, plausible errors, we can build the ultimate stress-test for any real autocorrect model out there. It's an entire NLP pipeline, built in reverse.

This system understands:

Physical Errors: Simulating "fat-finger" slips from an actual keyboard layout.

Cognitive Errors: Simulating "brain-fart" moments like homophone swaps (your vs. you're).

Semantic Errors: Simulating "near-miss" malapropisms like banking -> banker using NLP (NLTK) and word embeddings (GloVe).

Formatting Errors: Simulating real-world punctuation mistakes and random case-flipping.

🚀 Quick Start & Usage

This package is designed to be simple to use and easy to chain. The two main functions are auto_incorrect (for word errors) and corrupt_format (for punctuation/case errors).

# --- Import the main functions ---
# (Assuming all functions are in your package)

from auto_incorrect import auto_incorrect, corrupt_format, run_full_corruption

my_text = "I am running a test on my banking application for its creative standards. It's a beautiful day to see if your function works correctly."

# --- Option 1: Run the full chain with one function ---
# (This uses all default settings)

print("--- Full Corruption (Default) ---")
corrupted_text = run_full_corruption(my_text)
print(corrupted_text)


# --- Option 2: Manually chain functions for more control ---

print("\n--- Manual Chaining (Custom Settings) ---")

# 1. Apply word-based errors
# (Let's make errors common, with 70% typos and 30% smart errors)
custom_distribution = {
    'fat_finger': 0.7, 
    'brain_fart': 0.3, 
    'malapropism': 0.0
}
text_with_word_errors = auto_incorrect(
    my_text, 
    error_rate=0.3, # Corrupt 30% of words
    distribution=custom_distribution
)

# 2. Apply punctuation and case errors to that result
# (Let's be aggressive: remove all punctuation and flip 80% of caps)
final_corrupted_text = corrupt_format(
    text_with_word_errors,
    add_rate=0.0,
    replace_rate=0.0,
    remove_rate=1.0,         # 100% chance to remove punctuation
    case_corruption_prob=0.8 # 80% chance to flip a CAPITAL
)

print(f"Original:\n{my_text}\n")
print(f"Corrupted:\n{final_corrupted_text}")


Example Output (Manual Chaining):

Original:
I am running a test on my banking application for its creative standards. It's a beautiful day to see if your function works correctly.

Corrupted:
i am runnin a test on my bankin application for its creative standads it's a beutiful day to see if you're function works corectly


🛠️ Key Modules

auto_incorrect()

This function handles all word-based corruption.

⌨️ "Fat Finger" Module: Simulates physical keyboard mistakes.

adjacent_swap: standard -> stamdard (m near n)

transpose: standard -> standrad

delete_char: standard -> standad

insert_char: standard -> standfard

🧠 "Brain Fart" Module: Simulates cognitive "word choice" mistakes.

replace_homophone: your -> you're

replace_morphological: decision -> decide (uses NLTK/WordNet)

🎭 "Malapropism" Module: The smartest module. Creates "near-miss" semantic errors.

replace_semantic_neighbor: banking -> banker (uses GloVe embeddings to find related words with the same root).

corrupt_format()

This function handles all punctuation and case-based corruption.

Punctuation: Randomly adds, removes, or replaces punctuation marks.

Case: Randomly flips CAPITAL letters to lowercase based on a probability.

📦 Installation

Currently, you can install this package by cloning the repository:

git clone [https://github.com/YOUR_USERNAME/autoINcorrect.git](https://github.com/YOUR_USERNAME/autoINcorrect.git)
cd autoINcorrect
pip install -e .


(Coming soon to PyPI!)

pip install autoINcorrect
