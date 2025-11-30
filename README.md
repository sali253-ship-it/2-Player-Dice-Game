# 2-Player-Dice-Game
This project is a 2–player interactive dice game built in C++. Players take turns rolling dice, earning points, and triggering special powerups that can change the direction of the game. The program runs entirely in the terminal, focusing on clean game logic, modular functions, and user-friendly output.

How the Game Works — Step-by-Step
1. Game Start

The program welcomes the players and initializes both scores to zero.

The game randomly selects which player goes first using the rand() function.

2. Turn Structure

Each round follows the same pattern:

Step 1 — Roll the Dice

The active player rolls the dice (typically one or two dice depending on your version).

The roll result is displayed on the screen.

Step 2 — Add Points

The player’s score increases based on the dice result.

The updated score is shown after each roll.

3. Powerups (Special Effects)

Certain roll values or conditions can trigger powerups that make gameplay more exciting:

 Score Steal

Steals a portion of the other player’s points and adds it to your own.

 Turn Skip

Forces the opponent to miss their next turn.

 Bonus Roll

Allows the current player to roll again immediately.

These effects are all handled through separate functions to keep the logic clean and readable.

4. Switching Turns

After each roll (and any powerups), the game switches to the other player.

The program clearly displays which player is now active.

5. Ending the Game

The game continues until one player reaches the target score (you decide the number, such as 50 or 100).

The program announces the winner with a final score summary.

 Technical Features

Written entirely in C++ using functions, conditionals, loops, and clean modular structure.

Uses rand() and srand() for randomized dice rolls.

Carefully handles:

Score updates

Negative-score prevention

Edge cases in powerups

Turn tracking

Organized output to make round-by-round gameplay easy to follow.

 What I Learned

Designing a game loop and managing program state (turns, scores, win conditions).

Breaking a large program into small, reusable functions for readability.

Handling randomness, user input, and edge cases.

Testing and debugging interactive programs to make sure every scenario works correctly.

Writing a complete project from scratch without step-by-step instructions.
