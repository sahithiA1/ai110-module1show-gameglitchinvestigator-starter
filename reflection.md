# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

When I first ran the game, it opened in Streamlit with a difficulty setting, a guessing box, and buttons to submit guesses or start a new game. I noticed that the game started with 7 attempts remaining even though Normal difficulty allowed 8 attempts, without me submitting a guess. After I guessed the correct number and clicked New Game, the game generated a new secret number but still said that I had already won, preventing me from playing again. While reviewing the code, I also found that the hints were backwards because a guess that was too high would tell the player to go higher instead of lower.

**Bug Reproduction Log**

| Input | Expected Behavior | Actual Behavior | Console Output / Error | Suspected Code Location |
|---|---|---|---|---|
| Start the game on Normal difficulty without guessing | Game should start with 8 attempts remaining | Game started with only 7 attempts remaining | No console error | `app.py` — `st.session_state.attempts = 1` |
| Guess 1 correctly, click New Game, then submit 20 when the new secret is 35 | Game should accept 20 and indicate that the guess is too low | Game displayed "You already won. Start a new game to play again." and did not process the guess | No console error; game displayed the previous win message | `app.py` — `if new_game:` block does not reset `status` |
| Enter 10, then 15 when the secret number is 6 | The game should tell the player to guess lower because 15 is greater than 6 | The game displayed "Go HIGHER!" after submitting 15 | No console error; incorrect hint displayed | `app.py` — `check_guess()` function |

## 2. How did you use AI as a teammate?

- Which AI tools did you use on this project (for example: ChatGPT, Gemini, Copilot)?
- Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result).
- Give one example of an AI suggestion you did not accept as written (including what the AI suggested, why you rejected or changed it, and how you verified your version). It does not have to be a suggestion that was wrong: over-engineered, out of scope, harder to read, or a poor fit for this codebase all count.

I used Claude Code in VS Code and ChatGPT to help investigate, understand, and fix bugs in my guessing game. ChatGPT helped me work through the assignment step by step, while Claude Code examined the project files, explained the buggy logic, and made code changes. I reviewed the changes and tested the game to make sure the fixes worked correctly.

Example of a correct AI suggestion:

Claude Code suggested fixing the New Game button by resetting the game status to "playing", setting attempts and score to 0, clearing the guess history, and generating a new secret number based on the selected difficulty. This was correct because the original game kept the previous "won" status even after starting a new game. I verified the fix by winning a game, clicking New Game, and checking that the attempts, score, and history were reset. The game also allowed me to play again.

Example of an AI suggestion I did not accept as written:

When the automated tests failed after moving check_guess() into logic_utils.py, Claude Code presented an alternative of changing the function to return only the outcome instead of both the outcome and hint message. I chose not to use this approach because app.py needs both values to display the correct hint to the player. Instead, I asked Claude to update the tests to check both the outcome and message without changing the function's return type. I verified this decision by running pytest, which passed all four tests, and by testing the HIGHER and LOWER hints in the Streamlit game.

---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?
I decided a bug was fixed by comparing the game's behavior before and after making changes. I checked whether the game produced the expected results and whether the original problem happened again. I also used automated tests and manually played the game in Streamlit to make sure the fixes worked correctly.
- Describe at least one test you ran (manual or using pytest)  
  and what it showed you about your code.
I tested the guessing hints by using a secret number of 8 and entering guesses of 5 and 10. When I guessed 5, the game correctly displayed "Go HIGHER!", and when I guessed 10, it displayed "Go LOWER!". I also tested the New Game button after winning and confirmed that attempts and score reset to 0 and the guess history was cleared. These tests showed that the hint logic and game reset functionality were working correctly.
- Did AI help you design or understand any tests? How?
Yes, Claude Code helped me understand why the original pytest tests were failing after moving check_guess() into logic_utils.py. The tests expected a single string, but the function returned both an outcome and a hint message. I asked Claude to update the existing tests and add a new test to verify that guessing 60 against a secret of 50 displays "Go LOWER!". Claude ran pytest, and all four tests passed, confirming that the updated logic behaved as expected.
---

## 4. What did you learn about Streamlit and state?

- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?

---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  - This could be a testing habit, a prompting strategy, or a way you used Git.
- What is one thing you would do differently next time you work with AI on a coding task?
- In one or two sentences, describe how this project changed the way you think about AI generated code.
