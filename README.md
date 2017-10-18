[数据结构算法可视化](http://www.cs.usfca.edu/~galles/visualization/Algorithms.html)
# 图
## 图的遍历算法
### 1.DFS
流程:

1. 任取一顶点，访问之
2. 检查这个顶点的所有邻接顶点
3. 递归访问其中未被访问的顶点

伪代码:

```python
def DFS(v)
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
  visit[v]=1;
  Visit(v);
  
  p = G->adjlist[v].firstArc;
  
  while(p!=NULL){
  
    if(visit[p->adjvex]==0){
      DFS(G,p->adjvex);
      }
      
      p=p->nextArc;
  
  }

}

```
[DFS可视化过程](http://www.cs.usfca.edu/~galles/visualization/DFS.html)
