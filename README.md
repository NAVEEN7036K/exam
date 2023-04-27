# exam
if N >= 4:
	def clash(i, j):
		for k in range(0,N):
			if board[i][k]==1 or board[k][j]==1:
				return True
		for k in range(0,N):
			for l in range(0,N):
				if (k+l==i+j) or (k-l==i-j):
					if board[k][l]==1:
						return True
		return False
	def Nqueens(n):
		if n==0:
			return True
		for i in range(0,N):
			for j in range(0,N):
				if (not(clash(i,j))) and (board[i][j]!=1):
					board[i][j] = 1
					if Nqueens(n-1)==True:
						return True
					board[i][j] = 0
		return False
	Nqueens(N)
	print("The Solution is : ")
	for i in board:
		print (i)
elif N==1:
	print("It is a trivial case, as there is only one queen.")
else:
	print("No Solution because",N,"queens cannot be placed without clashing.")
