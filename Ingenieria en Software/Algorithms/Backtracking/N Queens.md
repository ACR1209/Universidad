# N Queens
The N Queen is the problem of placing N chess queens on an N×N chessboard so that no two queens attack each other. As shown bellow for an 8 Queens problem

![[Pasted image 20220902152717.png|400]]

## How to solve the N Queens problem using backtracking? 

The solution is found by trying to iterate through all the rows of the *n x n* chessboard and place the queen checking if it's attacked by the queens placed before hand, then using recursion for the rest of the rows. The pseudocode looks like this:

```
PlaceQueens(Q[1..n], r):
if r = n + 1
	print Q[1..n]
else
	for j <- 1 to n
		legal <- True
		for i <- 1 to r - 1
			if (Q[i] = j) or (Q[i] = j + r - i) or (Q[i] = j - r +i)
				legal <- False
		if legal
			Q[r] <- j
			PlaceQueens(Q[1..n, r + 1])
```

### Implementation in Python
```jupyter
from typing import List


class Solution:
    def solve_N_queens(self, n: int) -> List[List[str]]:
        
        # Create set of the already used columns, positive and diagonals 
        col = set()
        posDiagonal = set() #(r + c)
        negDiagonal = set() #(r - c)

        # List of list of string that are all posible solutions
        res = []

        # Creates the board of n x n representing an empty space as a dot
        board = [['.'] * n for i in range(n)]

        def backtrack(r):
            # If we are on r = n, that means we don't have to put more queens down, thus this is a valid solution
            # and we should save it in the response array
            if r == n:
                copy = [''.join(row) for row in board ]
                res.append(copy)
                return

            # Iterate through all columns in the current row
            for c in range(n):
                
                # If that column, positive and negative diagonal has been used go to the next 
                # column till you find a suitable column.
                if c in col or (r + c) in posDiagonal or (r - c) in negDiagonal:
                    continue
                    
                # Add the column, positive and negative diagonal as used
                col.add(c)
                posDiagonal.add(r + c)
                negDiagonal.add(r - c)
                board[r][c] = "Q"

                # Explore all the posibilities bellow this row using this column
                backtrack(r + 1)

                # We will go to the next column, thus clean the current column as used
                col.remove(c)
                posDiagonal.remove(r + c)
                negDiagonal.remove(r - c)
                board[r][c] = "."

        backtrack(0)
        return res

solve = Solution()

print(solve.solve_N_queens(4))

```


