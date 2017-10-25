[数据结构算法可视化](http://www.cs.usfca.edu/~galles/visualization/Algorithms.html)
# 图
## 图的遍历算法
### 1.DFS(深度优先搜索)
流程:

1. 任取一顶点，访问之
2. 检查这个顶点的所有邻接顶点
3. 递归访问其中未被访问的顶点

伪代码:

```python
def DFS(v):
visited(V)<-true
 for (v,w) in E:
 if not visited(w):
   DFS(w)
   
```
c语言实现:

```c
int visit[MAX_SIZE];

void DFS(AGraph *G,int v)
{
  ArcNode *p;
  visit[v]=1; //置为已经访问
  Visit(v); //访问顶点V
  
  p = G->adjlist[v].firstArc;//p指向图的第一条边
  while(p!=NULL){
  
    if(visit[p->adjvex]==0){//如果该顶点没有被访问，则递归访问该顶点
     
     DFS(G,p->adjvex);
     
     }
      
      p=p->nextArc;
  
  }

}

```
与二叉树的先序遍历做对比记忆:
```c
void preorder(Btnode *p)
{
 if (p!=NULL){
  Visit(p);
  preorder(p->left);
  preorder(p->right);
 }


}

```
[DFS可视化过程](http://www.cs.usfca.edu/~galles/visualization/DFS.html)

### 2.BFS(广度优先搜索)
类似于树的层次遍历

算法执行流程(伪代码):
```python
def BFS(G,visit):
Q<-v#v是首个访问的顶点
visit[v]<-true
while ! Q.empty():
 u<-Dequeue(Q)
 for (u,v) in E:
  if visit[v]==false:
   Enqueue(Q,v)   
```
c语言实现:
```c

void BFS(AGraph *G,int v,int visit[MAX_SIZE]){
 ArcNode *p;
 int queue[MAX_SIZE],front=0,rear=0;
 p = G->adjlist[v].firstArc;
 
 Visit(v);
 visit[v] = 1;
 
rear = (rear+1)%MAX_SIZE;
queue[rear] = v;

 while(front!=rear)
 {
  front = (front+1)%MAX_SIZE;
  int u = queue[front];

  p = G->adjlist[u].firstArc;

  while(p!=NULL)
  {
    if(!visit[p->adjvex]){
      Visit(p->adjvex);
      visit[p->adjvex] = 1;
      rear = (rear+1)%MAX_SIZE;
      queue[rear] = p->adjvex;
    }
				
    p= p->nextArc;

  }

 }


}
```
[BFS可视化过程](http://www.cs.usfca.edu/~galles/visualization/BFS.html)
## 最小（代价）生成树(minimum cost spanning treeh)

### 1.普里姆算法(Prim)
>默认使用邻接矩阵作为存储结构
执行过程:
```python
def Prim(G,V0):
for all u in V: #初始化lowcost为各个边的权值
	lowcost[u]<-cost[u]
lowcost<-{e | e = (V0,Vi)(i=0...n-1)}
min<-INF
for all u in V:
	for (u,v) in E: # 选出侯选边中最小权值的边，并入最小代价树
		if u is not set and lowcost[u]<min:
			min<-lowcost[u]
			addToSpanningTreeh(u)  #并入最小代价树方式不固定
	for (v,z) in E: #更新与v相连的侯选边的权值
		if z is not set and cost[z]<lowcost[z]: #如果(v,z)的权值比lowcost[z]小，则用(v,z)的权值更新侯选边
			lowcost[z]<-cost[z]
```
c语言实现:
```c
void Prim(MGraph G,int v0,int tree[MAX_SIZE])
{
	int lowcost[MAX_SIZE],vset[MAX_SIZE],v;
	int i,j,k,min;
	v = v0;
	for (i = 0;i<G.n;i++)//初始化lowcost数组为各个边的权值
	{
		lowcost[i] = G.edges[v0][i];
		vset[i] = 0;
	
	}
	vset[v0] = 1;//将v0并入最小代价树
	tree[v0] = 0;
	
	for (i = 0;i<G.n-1;i++)
	{
		min = INF;//INF为比所有边权值都要大的正常数
		for (j = 0;j<G.n;j++)
		{
			if(vset[j]==0&&lowcost[j]<min)
			{
				min = lowcost[j];
				k = j;//保存权值最小的边
			}
		}
		vset[k] = 1;//将权值最小的边纳入最小代价树
		v = k;
		tree[v] = min;
		
			for (j = 0;j<G.n;j++)//从顶点v出发，更新其他侯选边的权值
		{
			if(vset[j]==0&&G.edges[v][j]<lowcost[j])
			{
				lowcost[j] = G.edges[v][j];
			}
		}
		
	}

}

```
时间复杂度:
<p>基本操作:min = lowcost[]处于二重循环中.</p>
<p>O(n^2)</p>
[Prim可视化过程](http://www.cs.usfca.edu/~galles/visualization/Prim.html)
### 2.克鲁斯卡尔算法(Kruskal)
执行过程:
```python
def kruskal(G):
 for all u in V:
   MakeSet(v)   #建立并查集
 X<-empty set #初始化最小代价树
 sort the edges E by weight
 for all {u,v} in E in non-decreasing weight order:
   if Find(u)!=Find(v):#检查两个顶点是否有同一个根,确保两者属于不同的连通分量(Connected Component)
     add{u,v} to X
 
```
c语言实现:
```c

```
时间复杂度:
