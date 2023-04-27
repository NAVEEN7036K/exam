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
	
**************************************************************************************************************************	
	
def Matrix(dr):
    m=len(dr)
    arr=[[0 for i in range(m)]for j in range(m)]
    k_matrix=[[0 for i in range(m)]for j in range(m)]
    n=len(arr)
    for d in range(1,n):
        for i in range(1,n-d):
            arr[i][i]=0
            j=i+d
            k=i
            mini=456465464
            for k in range(i,j):
                value = arr[i][k]+arr[k+1][j]+(dr[i-1]*dr[k]*dr[j])
                if value<mini:
                    mini=value
                    k_matrix[i][j]=k
            arr[i][j]=mini
    Display(arr)
    Display(k_matrix)
    print("cost of matrix: ",arr[1][n-1])
def Display(arr):
    n=len(arr)
    for i in range(n):
        for j in range(n):
            print(arr[i][j],end=" ")
        print()
    print()
arr=input().split()
arr=list(map(int,arr))
print(arr)
Matrix(arr)
