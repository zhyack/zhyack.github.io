<section>
#倍增法求LCA
　　要说搞了这么久比赛还没学过倍增LCA，实在是惭愧。这次驱动我这个懒癌患者学习一下倍增LCA的是这道题——[CF609E-Minimum spanning tree for each edge](http://codeforces.com/contest/609/problem/E)。说起来有时候学习的动力就是这么产生的——Idea我有，工具不会用。
##LCA
####入门
　　先来扯一扯概念——LCA（Lowest Common Ancestor）,最近公共祖先。在一棵有根树中，节点v到根root的路径上所有的节点都叫v的“祖先”，LCA(u,v) 即两个点u,v，距离它们最近的公共祖先，也就是树中“最低”（深度最高，离root最远）的公共祖先。
####用途
* LCA & RMQ
* 树上任意两点间的距离/边权和
* 树上任意两点间的边权最大值
* etc.

####算法
　　求LCA有多种算法：  

* Tarjan——离线算法，必须事先知道所有的询问，O(N)。
* ST——LCA转RMQ，在线算法，当然对于比赛题目来说并没有什么区别，O(NlogN)。
* 倍增LCA——利用树深倍增，优点是不仅能知道LCA是谁，还能在O(logN)的复杂度内知道整个树上任意路径的状态，这是前两种算法所不能做到的，整体O(NlogN)。

##倍增LCA

* 记录各节点i的深度depth[i]。dfs一遍即可O(N)。  

<pre><code>
void dfs(int x,int d){
	depth[x] = d;
	visited[x] = true;
	for (vector&lt;int>::iterator it = edge[x].begin();it != edge[x].end();it++)
		if (!visited[*it]) dfs(*it,d+1);
}
</code></pre>

* 预处理出倍增数组，father[i][j]表示节点i往上(往根的方向)跳2^j步的祖先标号。-1表示不存在，也就是跳过根了。father[i][0]是节点i的父节点标号。
<pre><code>
void lcabinarylifting(int n){
	for (int j = 1;j < MAXB;j++)
		for (int i = 1;i <= n;i++)
			if (~father[i][j-1])
				father[i][j] = father[father[i][j-1]][j-1];
}
</code></pre>
* 对于点对(u,v)，设depth[u]>depth[v]，此时将u往上跳到和v在同一深度（此处请仔细揣摩代码）。u,v在同一深度时有两种情况——1.v本来就是u的祖先，此时u,v相同，lca(u,v) = v；2.v不是u的祖先，此时u和v距离其lca(u,v)的距离相同，一起往上跳（trick和之前的u上跳的代码一样，请仔细揣摩），停下来的位置即是lca(u,v)子节点上。
<pre><code>
int findlca(int u,int v){
	if (depth[u] < depth[v]) swap(u,v);
	for (int b = MAXB-1;b >= 0;b--)
		if (depth[father[u][b]] >= depth[v])
			u = father[u][b];
	if (u == v) return u;
	for (int b = MAXB-1;b >= 0;b--)
		if (father[u][b] != father[v][b])
			u = father[u][b],v = father[v][b];
	return father[u][0];
}
</code></pre>

###测试题目
[POJ1330](http://poj.org/problem?id=1330) 模板题，可供测试各种LCA算法。  
[code](https://github.com/zhyack/Non-classified-Codes/blob/master/POJ1330.cpp) 倍增求LCA参考代码。  
  
[CF609E](http://codeforces.com/contest/609/problem/E) 倍增LCA求任意两点路径上的最大边权。  
[blog entry](https://zhyack.github.io/posts/2015_12_20_Codeforces-Educational-Round-3.html) 题解链接。
</section>