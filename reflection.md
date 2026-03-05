# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

- What did the game look like the first time you ran it?
The first massive bug I noticed when I first played the game was the hints were all backward making the game impossible to win. I also noticed that the attempts that were said on the prompt was one lower than the attempts allowed.
---

## 2. How did you use AI as a teammate?

- Which AI tools did you use on this project (for example: ChatGPT, Gemini, Copilot)?
  I used Claude to help with debugging and Copilot to write commit messages.
- Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result).
  The first bug I located with the wrong hints was able to get fixed by CLaude AI
- Give one example of an AI suggestion that was incorrect or misleading (including what the AI suggested and how you verified the result).
  I only used AI for bugs I found in the game so all fixes it gave was correct.

---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?
I would run manual tests by playing the game each time after every fix  
- Did AI help you design or understand any tests? How?
  No, in this case I ran all tests manually.

---

## 4. What did you learn about Streamlit and state?

- In your own words, explain why the secret number kept changing in the original app.
  The secret number seemed to change because the app sometimes converted it to a string, causing incorrect string comparisons instead of proper numeric comparisons, which made the hints behave inconsistently.
- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?
  Streamlit “reruns” mean that every time you click a button or change an input, the entire script runs again from top to bottom, like restarting the program instantly.
- What change did you make that finally gave the game a stable secret number?
I removed the code that converted the secret number to a string on even attempts and made sure it was always compared as an integer, so the comparisons stayed consistent and the secret number remained stable throughout the game.
---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  Using AI as a companion for fixing bugs I locate during testing
- What is one thing you would do differently next time you work with AI on a coding task?
  I think I would use the same workflow I was using for this project as it was quite effective.
- In one or two sentences, describe how this project changed the way you think about AI generated code.
  It helped me realize that AI can make mots of mistakes and signifies the importance of having a human in the loop.
