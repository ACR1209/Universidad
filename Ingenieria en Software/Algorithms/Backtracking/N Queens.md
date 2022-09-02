# N Queens
The N Queen is the problem of placing N chess queens on an N×N chessboard so that no two queens attack each other. As shown bellow for an 8 Queens problem

![[Pasted image 20220902152717.png|400]]

## How to solve the N Queens problem using backtracking? 

The solution is found by trying to iterate through all the rows of the *n x n* chessboard and place the queen checking if it's attacked by the queens placed before hand, then using recursion for the rest of the rows. The pseudocode looks like this:

```
PlaceQueens(Q[1..n], r):
if r = n + 1
	return Q[1..n]
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
		col = set()
		posDiagonal = set() #(r + c)
		negDiagonal = set() #(r - c)
		res = []
		board = [['.'] * n for i in range(n)]
		def backtrack(r):
			if r == n:
				copy = [''.join(row) for row in board ]
				
				res.append(copy)
				return
			for c in range(n):
				if c in col or (r + c) in posDiagonal or (r - c) in negDiagonal:
					continue
				col.add(c)
				posDiagonal.add(r + c)
				negDiagonal.add(r - c)
				board[r][c] = "Q"
				backtrack(r + 1)
				col.remove(c)
				posDiagonal.remove(r + c)
				negDiagonal.remove(r - c)
				board[r][c] = "."
		backtrack(0)
		return res

  

solve = Solution()

  

print(solve.solve_N_queens(4))

```


