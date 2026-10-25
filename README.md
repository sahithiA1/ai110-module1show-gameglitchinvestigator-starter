# 🎮 Game Glitch Investigator: The Impossible Guesser

## 🚨 The Situation

You asked an AI to build a simple "Number Guessing Game" using Streamlit.
It wrote the code, ran away, and now the game is unplayable. 

- You can't win.
- The hints lie to you.
- The secret number seems to have commitment issues.

## 🛠️ Setup

1. Install dependencies: `pip install -r requirements.txt`
2. Run the broken app: `python -m streamlit run app.py`

## 🕵️‍♂️ Your Mission

1. **Play the game.** Open the "Developer Debug Info" tab in the app to see the secret number. Try to win.
2. **Find the State Bug.** Why does the secret number change every time you click "Submit"? Ask ChatGPT: *"How do I keep a variable from resetting in Streamlit when I click a button?"*
3. **Fix the Logic.** The hints ("Higher/Lower") are wrong. Fix them.
4. **Refactor & Test.** - Move the logic into `logic_utils.py`.
   - Run `pytest` in your terminal.
   - Keep fixing until all tests pass!

## 📝 Document Your Experience

- [x] **Describe the game's purpose.**

The Impossible Guesser is a number guessing game built with Python and Streamlit. The player selects a difficulty level and tries to guess a randomly generated secret number. The game provides higher or lower hints, tracks attempts, and updates the player's score.

- [x] **Detail which bugs you found.**

I found several bugs while testing the original game. The game started with one attempt already counted before the player made a guess. The higher and lower hints were reversed, and the game sometimes compared guesses incorrectly because the secret number was converted into a string. The New Game button also failed to reset the game status, preventing the player from playing again after winning.

- [x] **Explain what fixes you applied.**

I corrected the attempt counter to start at zero, fixed the higher and lower hints, and removed the unnecessary conversion of the secret number into a string. I also updated the New Game button to reset the status, attempts, score, and guess history while generating a new secret number within the selected difficulty range. With Claude Code's help, I moved the `check_guess()` function into `logic_utils.py` and updated the automated tests. All four pytest tests passed, and I manually verified the fixes in Streamlit.

## 📸 Demo Walkthrough

Describe your fixed game in numbered steps so a reader can follow along without watching a video:
1. The player opens the Streamlit game and selects a difficulty level. The game generates a random secret number and starts with 0 attempts used.
2. For this example, the secret number is 8, which can be checked using the Developer Debug Info section.
3. The player enters 5 and clicks Submit. The game displays "Go HIGHER!" because 5 is less than 8.
4. The player enters 10 and clicks Submit. The game displays "Go LOWER!" because 10 is greater than 8.
5. The player enters 8 and clicks Submit. The game displays "Correct!" and marks the game as won.
6. The player clicks New Game. The game resets the attempts to 0, clears the score and guess history, and generates a new secret number.
7. The player can now make guesses in the new game without seeing the previous game's winning message.

**Screenshot** *(optional)*: <!-- Insert a screenshot of your fixed, winning game here -->

## 🧪 Test Results

I used pytest to verify the guessing logic after refactoring the code into `logic_utils.py`.

Run the tests using:

```bash
python -m pytest -v
```

All four automated tests passed successfully:

```text
4 passed in 0.04s
```

## 🚀 Stretch Features

- [ ] [If you choose to complete Challenge 4, describe the Enhanced UI changes here — a screenshot is optional]
