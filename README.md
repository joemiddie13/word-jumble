# ACS 2130 Core Data Structures
Joseph Paul

## Project - Word Jumble

### Course Concepts Applied

This Word Jumble solver demonstrates practical application of key data structures and algorithms concepts covered in this course:

1. **Hash Tables** - Used as the central data structure for efficient anagram lookup, enabling O(1) time complexity for word matching instead of brute force approaches.

2. **Algorithm Analysis** - Applied Big O notation to evaluate and optimize solution efficiency, particularly by avoiding O(n!) permutation approaches in favor of O(n log n) sorting-based methods.

3. **Sets** - Implemented for fast O(1) dictionary word lookups when validating potential solutions.

4. **Recursion Principles** - Applied recursion-like problem decomposition by breaking the final jumble into subproblems (finding valid 2-letter words, then using remaining letters for 6-letter words).

5. **Queues** - Used queue-like collection and processing of circled letters when building the final solution.

6. **Problem Decomposition** - Divided the complex word jumble into smaller, manageable subproblems, similar to techniques used in recursive problem-solving.

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
   - Create anagram lookup dictionary (hash table) for efficient matching

3. For each jumble:
   a. Generate all possible words by checking the jumbled letters against dictionary
      - Sort letters to create "fingerprint" - O(n log n)
      - Look up in anagram hash table - O(1)
   b. Output potential solutions
   c. Select the most likely solution (or let user choose)
   d. Extract the circled letters from the solution

4. Collect all circled letters to form a bank of letters for the final answer

5. For the final answer (format: 2 letters, hyphen, 6 letters):
   a. Try different valid word combinations using the letters
   b. Generate all possible 2-letter words from the letter bank
   c. For each valid 2-letter word, try to form a valid 6-letter word with remaining letters
   d. Return all possible solutions that match the format criteria
   e. Let the user select the most contextually appropriate solution

6. Additional validation:
   - Check if the solution makes sense in context of "FARLEY ROLLED ON THE BARN FLOOR BECAUSE OF HIS ___"
   - Consider puns and word play since it's a riddle
```

### Implementation Overview

I implemented a Word Jumble solver using Python that efficiently finds solutions for jumbled words and algorithmically derives the final answer from the circled letters, applying various data structures and algorithms learned in this course.

### Data Structures and Algorithms Used

#### Data Structures:

1. **Dictionary/Hash Table** (Python `defaultdict`):
   - Used to create an anagram lookup table for efficient word finding
   - Keys: Sorted letters of words (e.g., "aelpp" for "apple")
   - Values: Lists of valid English words that can be formed from those letters
   - This provides O(1) lookup time for potential solutions
   - **Course Connection**: Direct application of hash table concepts for optimizing lookups

2. **Counter** (from Python's collections module):
   - Used to count letter frequencies and manage letter inventory
   - Ensures we only use available letters when forming words
   - **Course Connection**: Implementation of counting and tracking elements, similar to queue processing

3. **Set** (Python `set`):
   - Used for fast word lookup in the dictionary
   - O(1) checking if a word exists
   - **Course Connection**: Practical application of set data structures for membership testing

#### Algorithms:

1. **Anagram Finding Algorithm**:
   - Preprocess the dictionary to group words by their sorted letters
   - For each jumbled word:
     - Sort its letters to create a "fingerprint"
     - Look up this fingerprint in our anagram dictionary
   - Time complexity: O(n log n) for sorting + O(1) for lookup
   - Much more efficient than generating all permutations (which would be O(n!))
   - **Course Connection**: Application of algorithm analysis to choose optimal approach

2. **Circled Letter Extraction**:
   - Extract letters at specified positions from solution words
   - Combine these letters to form the bank for the final jumble
   - **Course Connection**: Processing elements in a sequential manner, similar to queue operations

3. **Final Jumble Solving Algorithm**:
   - Use a two-level permutation approach to find valid word combinations
   - First generate valid 2-letter words from the letter bank
   - For each valid 2-letter word, try to form valid 6-letter words with remaining letters
   - Verify each potential solution against our dictionary
   - Present all valid solutions matching the specified format
   - **Course Connection**: Application of problem decomposition principles similar to recursion

### Solution Process

1. Loaded and preprocessed the dictionary for efficient anagram lookups
2. Solved each individual jumble:
   - TEFON → OFTEN (circled letters: T, N)
   - SOKIK → KIOSK (circled letters: K, I, S)
   - NIUMEM → IMMUNE (circled letter: N)
   - SICONU → COUSIN (circled letters: S, I)
3. Collected all circled letters: TNKISNSI
4. Used combinatorial algorithms to find valid 2-letter and 6-letter word combinations
5. Found the solution "IN-STINKS" which can be formed from the circled letters
6. Verified this fits the context of the riddle: "FARLEY ROLLED ON THE BARN FLOOR BECAUSE OF HIS IN-STINKS"
   - A clever pun on "instincts" (natural behavior) and "stinks" (smells)

### Time and Space Complexity

- **Time Complexity**:
  - Dictionary preprocessing: O(D × L log L) where D is dictionary size, L is average word length
  - Individual jumble solving: O(L log L) per jumble
  - Final jumble solution: O(C! / (C-8)!) where C is the number of circled letters
  - Uses optimization techniques to avoid generating all permutations
  - **Course Connection**: Direct application of Big O analysis to understand algorithm efficiency

- **Space Complexity**: O(D) where D is the total size of the dictionary
  - We store the entire dictionary organized by anagram patterns and in a set
  - This space trade-off significantly improves runtime performance
  - **Course Connection**: Understanding space-time tradeoffs in algorithm design

### Key Insights and Learnings

1. **Problem Transformation**: The key insight is transforming the anagram problem from "generate all permutations" (O(n!)) to "sort and lookup" (O(n log n)). This type of transformation is a fundamental skill in algorithm design.

2. **Space-Time Tradeoff**: By using additional memory to store preprocessed dictionary data, we significantly improved runtime performance - a classic space-time tradeoff example.

3. **Hash Table Efficiency**: This project demonstrates why hash tables are so powerful - they allowed us to check potential words in O(1) time instead of linear searching.

4. **Problem Decomposition**: Breaking the complex problem into manageable subproblems mimics the approach used in recursion and dynamic programming.

### Enhancements and Extensions

- **Fallback Mechanism**: Handles cases where standard dictionaries don't contain puzzle-specific words
- **Format Specification**: Supports specific formats for the final solution (e.g., 2-letter word + 6-letter word)
- **Multiple Solutions**: Generates all valid solutions and allows selecting the most contextually appropriate one
- **Graceful Degradation**: Uses a minimal built-in dictionary when external resources aren't available