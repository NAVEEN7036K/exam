# exam
N-queen
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
Matrix chain multiplican
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

************************************************************************************************************************
Job seq
n=int(input('enter the no.of.jobs:'))
job=[]
d=[]
p=[]
profit=0.0
for i in range(n):
    x=int(input('deadline:'))
    d.append(x)
    y=int(input('profit:'))
    p.append(y)
    job.append(i+1)
for i in range(n):
    for j in range(n-i-1):
        if p[j]<p[j+1]:
            p[j],p[j+1]=p[j+1],p[j]
            d[j],d[j+1]=d[j+1],d[j]
            job[j],job[j+1]=job[j+1],job[j]
Dmax=d[i]
for i in range(n):
    if d[i]>Dmax:
        Dmax=d[i]
status=[0]*Dmax
for i in range (n):
    k=min(Dmax,d[i])
    while(k>=1):
        if status[(k-1)]==0:
            status[(k-1)]=job[i]
            profit+=p[i]
            break
        k=k-1
print('jobs:',status)
print('profit:',profit)
********************************************************************************************************************************
Fractional knapsack
n=int(input('Enter the number of items: '))
K=int(input('enter the knapsack value: '))
v=[]
w=[]
r=[]
p=0.0
for i in range (n):
    x=int(input('value: '))
    v.append(x)
    y=int(input('weight: '))
    w.append(y)
    r.append(v[i]/w[i])
for i in range (n):
    for j in range (n-i-1):
        if r[j]<r[j+1]:
            r[j],r[j+1]=r[j+1],r[j]
            v[j],v[j+1]=v[j+1],v[j]
            w[j],w[j+1]=w[j+1],w[j]
for i in range (n):
    if w[i]<=K:
        K=K-w[i]
        p=p+v[i]
    else:
        x=v[i]/w[i]
        p+=K*x
print('Result:',r)
print('Weight and value after finding result:',w,v)
print('profit: ',p)

****************************************************************************************************************************************
0/1 Knap
n=int(input('Enter the range:'))
K=int(input('Knapsack size:'))
item=[]
v=[]
wt=[]
profit=0.0
for i in range(n):
    it=int(input('item:'))
    item.append(it)
    value=int(input('value:'))
    v.append(value)
    weight=int(input('weight:'))
    wt.append(weight)
x=len(item)
arr=[[0 for i in range(0,K+1)]for j in range(0,x+1)]
for i in range(0,x+1):
    for j in range(0,K+1):
        if i==0 or j ==0 :
            arr[i][j]=0
        elif wt[i-1]<=j:
            arr[i][j]=max(arr[i-1][j],arr[i-1][j-wt[i-1]]+v[i-1])
        else:
            arr[i][j]= arr[i-1][j]
for i in range(0,x+1):
    for j in range(0,K+1):
        print(arr[i][j],end=' ')
    print()
print()
print("profit",arr[n][K])
it=[]
for i in range(len(item), 0, -1):
    if arr[i][K] != arr[i - 1][K]:
        it.append(item[i - 1])
        K -= wt[i - 1]
print("Items Selected: ",it)

*********************************************************************************************************************
krushkals
def get_weight(edge):return edge[2]

def kruskal(graph):
    edges = sorted(graph, key=get_weight)
    parent = list(range(len(edges) + 1)) 
    for edge in edges:
        u, v, w = edge
        pu, pv = parent[u], parent[v]
        if pu != pv:
            print(u,"-",v,":",w)
            for i in range(len(parent)):
                if parent[i] == pv:
                    parent[i] = pu

print("Edge : Weight")
graph = [[0, 1, 2], [0, 3, 6], [1, 2, 3], [1, 4, 5], [2, 4, 7], [3, 4, 9]]
kruskal(graph)

-----------------------------------------------------------------------------------------------------------------------
floyds

MAX = 999999999999
def print_matrix(matrix):
for row in matrix:
print(row)
def get_distance(weight):
d = weight
n = len(weight)
p = [[0] * n for _ in range(n)]
for k in range(n):
for i in range(n):
20CS2018L – Design and Analysis of
Algorithms Lab
URK21CS7054
for j in range(n):
if d[i][j] > d[i][k] + d[k][j]:
d[i][j] = d[i][k] + d[k][j]
p[i][j] = k+1
return d,p
weight = [
[0,4,5],
[2,0,MAX],
[MAX,-3,0]
]
distance,intermediate = get_distance(weight)
print("Distance matrix: ")
print_matrix(distance)
print("Intermediate nodes : ")
print_matrix(intermediate)
----------------------------------------------------------------------------------------------------------------------
prims

def minimum(graph,vertices,current):
selected = [current]
total = 0
for i in range(len(vertices) - 1): index =
vertices.index(current)# print(index)
j = graph[index]
# print(f"j : {j}")
data = list(filter(lambda x: x!= 0 andvertices[j.index(x)]
not in selected, j))
# print(f"data : {data}")
# print(f"selected : {selected}")if len(data) > 0:
k = min(data) smallest =
j.index(k)
# print(vertices[smallest])total += k
print(f"{current} -> {vertices[smallest]} : {k}")current =
vertices[smallest] selected.append(vertices[smallest])
print(f"MST : {total}")
graph = [
[0,7,0,8,0,0],
[7,0,6,3,0,0],
[0,6,0,4,2,5],
[8,3,4,0,3,0],
[0,0,2,3,0,2],
[0,5,0,2,0,0]
]
vertices = ['S','A','B','C','D','T']
minimum(graph,vertices,current = "A")
