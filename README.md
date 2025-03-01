# ACS 2130 Core Data Structures
Joseph Paul

## Project - Word Jumble

### Pseudocode Solution

```
WORD JUMBLE SOLVER - PSEUDOCODE

1. Define the jumbles and their circle positions
   - TEFON with circles in positions 3 and 5
   - SOKIK with circles in positions 1, 2, and 4
   - NIUMEM with a circle in position 5
   - SICONU with circles in positions 4 and 5

2. Load dictionary of English words
   - Read from /usr/share/dict/words
   - Filter for words matching the length of each jumble

3. For each jumble:
   a. Generate all possible words by checking the jumbled letters against dictionary
   b. Output potential solutions
   c. Select the most likely solution (or let user choose)
   d. Extract the circled letters from the solution

4. Collect all circled letters to form a bank of letters for the final answer

5. For the final answer (format: 2 letters, hyphen, 6 letters):
   a. Try different combinations of the letters to form a meaningful phrase
   b. Focus on phrases that make sense in the context of the riddle
   c. Return the most likely solution

6. Additional validation:
   - Check if the solution makes sense in context of "FARLEY ROLLED ON THE BARN FLOOR BECAUSE OF HIS ___"
   - Consider puns and word play since it's a riddle
```

### Implementation Overview

I implemented a Word Jumble solver using Python that efficiently finds solutions for jumbled words and derives the final answer from the circled letters.

### Data Structures and Algorithms Used

#### Data Structures:

1. **Dictionary/Hash Table** (Python `defaultdict`):
   - Used to create an anagram lookup table for efficient word finding
   - Keys: Sorted letters of words (e.g., "aelpp" for "apple")
   - Values: Lists of valid English words that can be formed from those letters
   - This provides O(1) lookup time for potential solutions

2. **Counter** (from Python's collections module):
   - Used to count letter frequencies and verify solutions
   - Helps ensure we have the correct letters for forming words

#### Algorithms:

1. **Anagram Finding Algorithm**:
   - Preprocess the dictionary to group words by their sorted letters
   - For each jumbled word:
     - Sort its letters to create a "fingerprint"
     - Look up this fingerprint in our anagram dictionary
   - Time complexity: O(n log n) for sorting + O(1) for lookup
   - Much more efficient than generating all permutations (which would be O(n!))

2. **Circled Letter Extraction**:
   - Extract letters at specified positions from solution words
   - Combine these letters to form the bank for the final jumble

### Solution Process

1. Loaded and preprocessed the dictionary for efficient anagram lookups
2. Solved each individual jumble:
   - TEFON → OFTEN (circled letters: T, N)
   - SOKIK → KIOSK (circled letters: K, I, S)
   - NIUMEM → IMMUNE (circled letter: N)
   - SICONU → COUSIN (circled letters: S, I)
3. Collected all circled letters: TNKISNSI
4. Determined the final answer format: 2-letter word + hyphen + 6-letter word
5. Found that "IN-STINKS" can be formed from the circled letters
6. Verified this fits the context of the riddle: "FARLEY ROLLED ON THE BARN FLOOR BECAUSE OF HIS IN-STINKS"
   - A clever pun on "instincts" (natural behavior) and "stinks" (smells)

### Time and Space Complexity

- **Time Complexity**: O(n log n) where n is the length of the longest word
  - Sorting letters is the most expensive operation at O(n log n)
  - Dictionary lookups are O(1)
  - Overall much better than the naive approach of generating all permutations O(n!)

- **Space Complexity**: O(m) where m is the total size of the dictionary
  - We store the entire dictionary organized by anagram patterns
  - This space trade-off significantly improves runtime performance