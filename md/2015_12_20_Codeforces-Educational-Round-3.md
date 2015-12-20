<section>
#Codeforces Educational Round #3
- [contest link](http://codeforces.com/contest/609)  
  

　　这次倒是没什么hack点了，水题上演了一场排序大战，从D题开始教做码农...  

- ##[609A-USB Flash Drives](http://codeforces.com/contest/609/problem/A)  
题意：  
　　一个可拆分的文件往若干个U盘中放，最少用几个U盘。 　　  
解法：  
　　随便拆分，当然是尽可能放大容量U盘里，要不你让那些拿着1TU盘的少年们去哪里找装X的自信。　　
　　
  　　  
  [code](https://github.com/zhyack/Codeforces/blob/master/609_Educational%20Round%233/609A.cpp)  

- ##[609B-The Best Gift](http://codeforces.com/contest/609/problem/B)  
题意：  
　　m种物品，每样若干个（带序号），求从中挑出两个有多少种组合方式。　　  
解法：  
　　连long long 都不坑，不解释。  　　
  　　
  　　
  　　  
  [code](https://github.com/zhyack/Codeforces/blob/master/609_Educational%20Round%233/609B.cpp)  

- ##[609C-Load Balancing](http://codeforces.com/contest/609/problem/C)  
题意：  
　　物品体积均为1的负载均衡，每次可以调整一个物品的位置，问最少操作几次。　  
解法：  
　　设物品总数为sum，那么负载均衡的方案一定是`sum%N * (sum/N+1)` + `(N-sum%N) * sum/N` 　　
  　　  
  [code](https://github.com/zhyack/Codeforces/blob/master/609_Educational%20Round%233/609C.cpp)  

- ##[609D-Gadgets for dollars and pounds](http://codeforces.com/contest/609/problem/D)  
题意：  
　　小明有S块钱，但他要代购，只能兑换成美元买米国的东西，或英镑买腐国的东西，汇率每天都在变，但他想买的东西在这可以预见的N天内在本地都是价钱不变的。问小明为了满足买买买的欲望，想从自己的购物清单M个物品中**尽早**买入K个的方案。　  
解法：  
　　假设我们在前day天买入K个物品——1.一定会要挑这day天最便宜的买；2.一定挑美元最便宜的时候买米国的东西，挑英镑最便宜的时候买腐国的东西——所以我们要知道的信息有，前day天美元英镑最便宜的分别是那一天，然后对应这两个值去挑选最便宜的物品集中在这两天买。贪心思路很直接，需要注意的只是一定要确定美元和英镑的汇率后才考虑物品的价格；还有就是挑最便宜的物品时可以分成米国和腐国两类分别排序，同一类的系数是一样的，所以乘完系数大小关系也不会变。  
　　当然的day有N个值可以选择，但注意到如果day = d时存在购买方案，那就代表着day > d时一定存在购买方案，即某种意义上的单调性，所以可以二分枚举day。
 　　
  　　  
  [code](https://github.com/zhyack/Codeforces/blob/master/609_Educational%20Round%233/609D.cpp)  

- ##[609E-Minimum spanning tree for each edge](http://codeforces.com/contest/609/problem/E)  
题意：  
　　对于图中所有的边，输出图中包含这条边的最小生成树的值。  
解法：  
　　包含某条边(u,v)的话，只要将其原本在全局MST中的u->v这条路上的最长边舍弃即可，因为最长边本来就是Kruskal中连接u，v的最后加入的一条割边，且是所有能将u，v割开的值最大的，把它替换掉对全局的增量最小。  
　　具体求法需要借助lca...  
　　未完待续...　　
  　　  
  [code](https://github.com/zhyack/Codeforces/blob/master/609_Educational%20Round%233/609E.cpp)  
</section>