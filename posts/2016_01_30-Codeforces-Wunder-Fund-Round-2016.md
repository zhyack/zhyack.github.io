<section>
#Codeforces #Wunder Fund Round 2016 (Div. 1 + Div. 2 combined)
- [contest link](http://codeforces.com/contest/618)  
  

　　Wunder Fund Round 2016，题目难度一般，还是比较坑。小号([zhy](http://codeforces.com/profile/zhy))继续踩雷，跪得比上一场还惨，不过服了，是在下输了。  

- ##[618A-Slime Combining](http://codeforces.com/contest/618/problem/A)  
题意：  
　　每次往序列尾部添加一个1，如果序列尾部两个数相同均为x，就合并为一个x+1。  
解法：  
　　模拟，如题意所述。  
  [code](https://github.com/zhyack/Codeforces/blob/master/618_Wunder%20Fund%20Round%202016/618A.cpp)  

- ##[618B-Guess the Permutation](http://codeforces.com/contest/618/problem/B)  
题意：  
　　给出矩阵a， `a[i][j] = min{p[i],p[j]}`， `a[i][i] = 0`，求排列p。  
解法：  
　　数一数一行出现最多的数出现了几次，计为m，那么对应的`p[i]=N-m`。特殊的是，m等于1的时候可能是`p[i] = N-1`，也可能是`p[i] = N`。  
  [code](https://github.com/zhyack/Codeforces/blob/master/618_Wunder%20Fund%20Round%202016/618B.cpp)  

- ##[618C-Constellation](http://codeforces.com/contest/618/problem/C)  
题意：  
　　给N个点，求三个点组成的三角形，满足其他N-3个点均不在此三角形上或内部。  
解法：  
　　难得尝试一下计算几何，又坑精度...精度务必设小，实测atan2求角度精度设到1e-20能过...  
　　具体操作——找左下角的点，以此点为原点，极角排序(atan2+距离)，排序后锁定前两个点为所求三角形的一条边，只需找到第三个点，与这两点不在一条直线上，且尽量靠前。正确性可以反证——如果存在反例，那么反例的第三个点一定极角较小或距离较短，与排序处理结果相悖。  
  [code](https://github.com/zhyack/Codeforces/blob/master/618_Wunder%20Fund%20Round%202016/618C.cpp)  

- ##[618D-Hamiltonian Spanning Tree](http://codeforces.com/contest/618/problem/D)  
题意：  
　　完全图G中有N个点，所有的边长为Y，现选出一生成树，树上边长均变为X，求一条哈密尔顿路径的最小值。  
解法：  
　　X>=Y的时候：当然是避免树上的边咯，然而树上的边才N-1条，最多也就封死一个点。所以先检查是否有哪个点的度是N-1，有的话即被封死，答案是`(N-2)*Y+X`；否则原边一定是可以找到一条哈密尔顿路径的，答案是`(N-1)*Y`。  
　　X<Y的时候：要尽量选择树上的边，沿着树上的路径走，走到绝路时才考虑走一个边权为Y的路从而可以切换到树上的另外一条没走过的路径。所以——要求出这棵树最少可以划分成几条路径。  
　　树形dp，`dp[i][1]`表示节点i及其子树最少划分几条路径，且节点i可以与父节点连接成一条路径；`dp[i][0]`表示节点i及其子树最少划分几条路径，且节点i不与父节点连接成一条路径。显然`dp[i][1] >= dp[i][0]`。  
　　如果 i 的子节点 j 中存在一个可以与之相连的，也就是`dp[j][1]<=dp[j][0]`，那么节点 i 就可以顺其自然的连上 j ，此时`dp[i][1] = ∑min(dp[j][0],dp[j][1])`；否则`dp[i][1] = ∑min(dp[j][0],dp[j][1])+1`。 如果 i 的子节点 j 中存在两个可以与之相连的，那就可以两段通过节点 i 连成一段，比`dp[i][1]`还少了一段，只是这时节点 i 在段中间，不能在与其父节点相连，此时`dp[i][0] = dp[i][1]-1`；否则`dp[i][0] = dp[i][1]`。  
　　求出树上最少的分段数 n ，答案即为`(n-1)*X+(N-n)*Y`。  
  [code](https://github.com/zhyack/Codeforces/blob/master/618_Wunder%20Fund%20Round%202016/618D.cpp)  

</section>