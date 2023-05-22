
# What is Minimax?

Mini-max tree search is a decision-making algorithm commonly used in game theory to determine the best possible move for a player. It works by constructing a game tree that represents all possible game moves and outcomes, then using a recursive search algorithm to evaluate each potential move.

At each level of the game tree, the algorithm considers the possible moves that the current player can make, and for each move, it simulates the game by making a move and evaluating the resulting game state. The algorithm then recursively evaluates the game tree, alternating between maximizing the player's score and minimizing the opponent's score.

The name "mini-max" comes from the fact that the algorithm alternates between minimizing the opponent's score and maximizing the player's score, with the ultimate goal of finding the move that maximizes the player's score while minimizing the opponent's score.

![[Minimax Graphic.png]]

The mini-max algorithm can be used for various games, including chess, checkers, and tic-tac-toe. However, it is a computationally expensive algorithm since it requires evaluating every possible move in the game tree, which can be prohibitively expensive for complex games with many possible moves.


# How do I use this in my program?

In my chess agent, the mini-max tree search algorithm is used to evaluate the best possible move for the agent to make in a given game state. Here are the general steps I followed to create a  chess agent:

- Define the game state: The first step is to define the current game state, which includes the positions of all the pieces on the board and information about whose turn it is.
- Generate the game tree: The next step is to generate the game tree, which represents all possible moves and outcomes of the game. Each node in the game tree represents a game state, and the edges represent possible moves.
- Evaluate the game tree: Starting from the current game state, the algorithm will recursively evaluate the game tree, alternating between maximizing the agent's score and minimizing the opponent's score.
- Assign a score to each node: To evaluate a node, the algorithm will assign a score based on the value of the board state. This score can be calculated using various heuristics, such as the material balance or positional advantages.
- Choose the best move: Once the entire game tree has been evaluated, the algorithm will choose the move that leads to the highest score for the agent.
- Repeat the process: After making the move, the agent will repeat the process from step 1 to evaluate the next game state and choose the best move.

This insures that my agent makes the best possible move for how many moves it sees ahead however the hardest part is assigning a score to each node which requires my own board position evaluator.


# How does my agent evaluate the board position

At first my agent just used the material of each moveable(piece) to evaluate the board. The program would iterate over all the coordinates of the board and sum up the material. This would work be making one color(white) add positive material and the other color(black) add negative material. This makes it so that if the material is even, the position would be 0, if black was winning it would be negative and if white was winning it would be positive. 

After improving other parts of my code, I was able to increase the accuracy of the position evaluator to take where the piece is on the board is into account. So, if a pawn was isolated, there were no pawns in the ranks(columns) next to it, it would be worth less material than a pawn supported by another pawn. This would make my agent want to create 