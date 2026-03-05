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

### Game's Purpose
The Game's Purpose is a number guessing game where players try to identify a secret number in a limited number of attempts. The game offers three difficulty levels (Easy, Normal, Hard) that vary the number range and attempt limit. After each guess, players receive a hint telling them to go higher or lower with a score given with how fast the number was guessed

### Details of bugs founds and fixes applied
1. Hint Messages Were Swapped
Location: Lines 37–40 (check_guess function)
Problem
The hint messages were backwards:
When the guess was greater than the secret number, it said: "Go HIGHER!"
When the guess was less than the secret number, it said: "Go LOWER!"

Fix
The messages were swapped so that:
If guess > secret → it now says "Go LOWER!"
If guess < secret → it now says "Go HIGHER!"

2. New Game Did Not Fully Reset
Location: Around Lines 120–140 (New Game button handler)
Problem
When "New Game" was pressed:
The secret number reset, Attempts reset but status was not reset and history was not cleared
Because of this, the game sometimes stayed in a "won" or "lost" state and stopped immediately.

Fix
Added:
st.session_state.status = "playing"
st.session_state.history = []
Now the game fully resets when New Game is pressed.

3. Difficulty Ranges Were Swapped
Location: get_range_for_difficulty() function
Problem
The difficulty levels were incorrect:
Normal → 1–100
Hard → 1–50
They were reversed from the intended design.

Fix
Updated ranges to:
Easy → 1–20
Normal → 1–50
Hard → 1–100
Now difficulty increases the range correctly.

4. Guess Prompt Always Said 1–100
Location: Guess input section
Problem
The text always said: "Guess a number between 1 and 100"
This was incorrect for Easy and Normal modes.

Fix
Replaced the hardcoded text with:
f"Guess a number between {low} and {high}."
Now the displayed range matches the selected difficulty.

5. Secret Number Appeared to Change
Location: Lines 158–163
Problem
On even-numbered attempts, the code converted the secret number into a string before comparing it to the guess:
secret = str(st.session_state.secret)
This caused string comparison instead of number comparison.
Example of the issue: "9" > "50" → True (because strings compare left to right)
This made hints behave incorrectly, making it seem like the secret number changed.

Fix
Removed the string conversion and always passed the secret as an integer:
outcome, message = check_guess(guess_int, st.session_state.secret)
Now comparisons work correctly.

6. Attempts Started Too Low
Location: Session state initialization
Problem
attempts was initialized to 1 instead of 0:
st.session_state.attempts = 1
This caused "Attempts left" to show one fewer attempt than allowed.

Fix
Changed initialization to:
st.session_state.attempts = 0
Now the full number of allowed attempts is shown at the start of the game.

## 📸 Demo



## 🚀 Stretch Features

- [ ] [If you choose to complete Challenge 4, insert a screenshot of your Enhanced Game UI here]
