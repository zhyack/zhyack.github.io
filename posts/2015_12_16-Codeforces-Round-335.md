<section>
#Codeforces Round #335
- [contest link](http://codeforces.com/contest/606)  
  

　　CF#335，Virtual participation，题目简单，只有E题让人眼前一亮，然而并不想实现E题...  

- ##[606A-Magic Spheres](http://codeforces.com/contest/606/problem/A)  
题意：  
　　三种颜色的球，分别有a1,a2,a3个，但是想要得到b1,b2,b3个，兑换规则是两个相同颜色的球可以换一个与之不同颜色的球，问是否能成功。  
解法：  
　　只需知道每种球缺几个，富裕几个就可以了，富裕的全部用来补足缺的，看是否够。  　　  
  [code](https://github.com/zhyack/Codeforces/blob/master/606_Round%20%23335(Div.%202)/606A.cpp)  

- ##[606B-Testing Robots](http://codeforces.com/contest/606/problem/B)  
题意：  
　　一个机器人按指定步骤在格子中上下左右走，全局只有一个雷，埋在哪里不确定（共row*col种情况），机器人踩到雷会炸，执行完所有命令也会炸。然后对于机器人每一步，都要给出机器人能导致机器人在此爆炸的情况的总数。  
解法：  
　　模拟题，记录好每个格点是否已经踩过，如果这一步踩到了之前踩过的格点，那肯定不会有雷，即不可能有那种布局导致机器人爆炸；反之，则有一种布局，即这一步踩到的刚好是雷点；当然还有最后一步要注意，执行完所有命令也会爆炸，也就是在所有踩过的地方都没有雷的格局也都会导致最后一步爆炸。  　　  
  [code](https://github.com/zhyack/Codeforces/blob/master/606_Round%20%23335(Div.%202)/606B.cpp)  

- ##[606C-Sorting Railway Cars](http://codeforces.com/contest/606/problem/C)  
题意：  
　　N的一个排列，每次操作只能将其中一个数放到最前面或最后面，问使之有序的最少操作数。  
解法：  
　　`最少操作数=N-最多不动数`，不动的子序列一定是上升且**值连续**的,所以并不是LIS问题。注意到值是连续的，所以可以将其转化为位置关系上的连续上升子串问题，也就是先记录所有数出现的位置，存在映射表中，然后求映射表的最长上升子串的长度，O(N)复杂度。  
　　当然，如果N个数不局限于1~N，或者会有值相同的数，这些都有类似的解法，但是复杂度就要是O(NlogN)了。  
  [code](https://github.com/zhyack/Codeforces/blob/master/606_Round%20%23335(Div.%202)/606C.cpp)  

- ##[606D-Lazy Student](http://codeforces.com/contest/606/problem/D)  
题意：  
　　给出图G中所有的边权及其是否在图G的MST中，求图G。  
解法：  
　　要说关于MST出题的各种trick，几乎所有的都是和Kruskal算法（聚类）相关的。为了构造出图G，我们要考虑Kruskal求最小生成树时的做法：

> 先按边权排序，从小到大考虑是否属于MST，如果当前边两段分属不同聚类，则属于MST，否则不属于。　　

　　于是很容易想到其逆向构造的方法：

> 按边权排序，如果其属于MST，则分属不同聚类，否则属于同一聚类。  


　　当然，为了构造的简便，我们可以只考虑两种聚类，也就是当前在MST中的，和未考虑的孤立的点。于是构造算法如下:
> 标记为属于MST的，就向MST中加入一个点，并连接MST中最大的两个点，也就是这个边是(nodecnt,nodecnt-1)，此时注意，(nodecnt,nodecnt-k),k>=2均未使用，且是MST内部的点连成的不属于MST的边，可供下一种情况使用。  
   
> 标记为不属于MST的，使用可用的(n,n-k),其中n<=nodecnt,k>=2,如果当前并没有可以使用的这样的边，那就是-1，不能构造出这样的图G。  

　　最后要注意一点的是，按边权排序时，如果边权相等，要把属于MST的边排在前面，因为早点往MST中加入点，才能有更多非MST边可用的点对，否则原本可以构造出的图G也会被判断成-1，第7组数据便是hack了这一点  
　　[code](https://github.com/zhyack/Codeforces/blob/master/606_Round%20%23335(Div.%202)/606D.cpp)  

  
- ##[606E-Freelancer's Dreams](http://codeforces.com/contest/606/problem/E)  
题意：  
　　N种途径为了完成两个指标(X,Y)，每种途径的速度是(vxi,vyi)，求最少时间。  
解法：  
　　求最少时间也即求最大速度，由于速度向量都已知，其线形组合可以表示出来各个方向上的最大速度，而各个方向的最大速度显然就是凸包上的点表示的向量，其中(X，Y)这个方向上的最大速度就是我们要求的。所以就是先在二维平面描出各向量的点，求凸包，然后求直线与凸包的交点，交点处即时最大速度的向量。需要注意的是要额外加上x和y轴单独的最大的向量（不考虑另一指标的影响）。  
code
</section>

- ##

