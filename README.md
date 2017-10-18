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
执行过程:
从V0开始执行
1.将边{e | e = (V0,Vi)(i=0...n-1)}当做侯选边.

c语言实现:
```c

```
[Prim可视化过程](http://www.cs.usfca.edu/~galles/visualization/Prim.html)
