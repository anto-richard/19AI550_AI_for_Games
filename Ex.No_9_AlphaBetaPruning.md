## <p align="center"> EX.NO : 9 -- IMPLEMENTATION OF ALPHA BETA PRUNING... </p>

#### DATE : 04.10.2024      
#### NAME : Anto Richard. S
#### REGISTER NUMBER : 212221240005
#### SLOT : 4H2-1

### AIM : 

Write a Alpha beta pruning algorithm to find the optimal value of MAX Player from the given graph.

### ALGORITHM :

#### Step 1 :

Start the program.

#### Step 2 : 

Initially  assign MAX and MIN value as 1000 and -1000.

#### Step 3 :

Define the minimax function  using alpha beta pruning.

#### Step 4 :

If maximum depth is reached then return the score value of leaf node. [depth taken as 3].

#### Step 5 :

In Max player turn, assign the alpha value by finding the maximum value by calling the minmax function recursively.

#### Step 6 :

In Min player turn, assign beta value by finding the minimum value by calling the minmax function recursively.

#### Step 7 :

Specify the score value of leaf nodes and Call the minimax function.

#### Step 8 :

Print the best value of Max player.

#### Step 9 :

Stop the program. 

### PROGRAM :

```python

# Define a large negative and positive value to represent infinity :

INF = float('inf')

# Alpha-Beta Pruning function :

def alpha_beta_pruning(depth, node_index, maximizing_player, values, alpha, beta):
    # Base case: leaf node is reached :

    if depth == 3:
        return values[node_index]
    
    if maximizing_player:
        max_eval = -INF
        # Recur for the two children of the current node :

        for i in range(2):
            eval = alpha_beta_pruning(depth + 1, node_index * 2 + i, False, values, alpha, beta)
            max_eval = max(max_eval, eval)
            alpha = max(alpha, eval)
            
            # Prune the branch :

            if beta <= alpha:
                break
        return max_eval
    else:
        min_eval = INF
        # Recur for the two children of the current node :

        for i in range(2):
            eval = alpha_beta_pruning(depth + 1, node_index * 2 + i, True, values, alpha, beta)
            min_eval = min(min_eval, eval)
            beta = min(beta, eval)
            
            # Prune the branch :

            if beta <= alpha:
                break
        return min_eval

# Driver code :

if __name__ == "__main__":
    # This is the terminal/leaf node values of the game tree :

    values = [3, 5, 6, 9, 1, 2, 0, -1]

    print("Optimal value:", alpha_beta_pruning(0, 0, True, values, -INF, INF))

```

### OUTPUT :

![games-out-7](https://github.com/user-attachments/assets/1f21de7a-399e-480e-b147-ac7b100eec04)

### RESULT :

Thus, the best score of max player was found using Alpha Beta Pruning.

