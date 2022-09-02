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
def place_queens(q, r):
	if r == 
```


