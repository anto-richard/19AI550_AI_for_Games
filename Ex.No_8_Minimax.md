## <p align="center"> EX.NO : 8 -- IMPLEMENTATION OF MINIMAX SEARCH... </p>

#### DATE : 12.09.2024                                                                          
#### REGISTER NUMBER : 212221240005

### AIM :

Write a mini-max search algorithm to find the optimal value of MAX Player from the given graph.

### ALGORITHM :

#### Step 1 : 

Start the program.

#### Step 2 :

Import the math package.

#### Step 3 : 

Specify the score value of leaf nodes and find the depth of binary tree from leaf nodes.

#### Step 4 : 

Define the minimax function.

#### Step 5 : 

If maximum depth is reached then get the score value of leaf node.

#### Step 6 : 

Max player find the maximum value by calling the minmax function recursively.

#### Step 7 : 

Min player find the minimum value by calling the minmax function recursively.

#### Step 8 : 

Call the minimax function  and print the optimum value of Max player.

#### Step 9 : 

Stop the program. 

### PROGRAM :

```python

import math
def minimax (curDepth, nodeIndex,
             maxTurn, scores,
             targetDepth):
    # base case : targetDepth reached
    if (curDepth == targetDepth):
        return scores[nodeIndex]
    if (maxTurn):
        return max(minimax(curDepth + 1, nodeIndex * 2,
                    False, scores, targetDepth),
                   minimax(curDepth + 1, nodeIndex * 2 + 1,
                    False, scores, targetDepth))
     
    else:
        return min(minimax(curDepth + 1, nodeIndex * 2,
                     True, scores, targetDepth),
                   minimax(curDepth + 1, nodeIndex * 2 + 1,
                     True, scores, targetDepth))
     
# Driver code
scores = [3, 5, 2, 9, 12, 5, 23, 20]
treeDepth = math.log(len(scores), 2) # calculate depth of node  log 8 (base 2) = 3)
print("The optimal value is : ", end = "")
print(minimax(0, 0, True, scores, treeDepth))

```

### OUTPUT :

![games-out-6](https://github.com/user-attachments/assets/c1e662f2-9cd7-4c9c-8438-3f2a4425c702)

### RESULT :

Thus, the optimum value of max player was found using minimax search.

