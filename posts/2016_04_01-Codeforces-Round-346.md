<section>
#Codeforces Round #346 (Div. 2)
- [contest link](http://codeforces.com/contest/659)  
  	

CF#346，难度偏简单，题目读起来比较费劲，毕竟不是Russian-English Speaker...  
好久没做题了的说...这周做了345和346两场，感觉题目都不算难，至少不是像过年那段时间那样神坑。正好在其他地方被虐了来做比赛找自信，论消遣的正确姿势。  
另外最近消停了挺久了，看了看访客统计还是有持续的访问，感人肺腑。  

- ##[659A-Round House](http://codeforces.com/contest/659/problem/A)  
题意：  
在一个圈上顺时针或逆时针走若干步之后在哪儿。  
解法：  
加，然后模。  
  [code](https://github.com/zhyack/Codeforces/blob/master/659_Round%20%23346(Div.%202)/659A.cpp)  

- ##[659B-Qualifying Contest](http://codeforces.com/contest/659/problem/B)  
题意：  
若干个region中，每个region选出2个成绩最好的队员。问每个region的方案是否唯一。  
解法：  
region方案是否唯一其实看得就是第2名和第3名是不是相同。  
  [code](https://github.com/zhyack/Codeforces/blob/master/659_Round%20%23346(Div.%202)/659B.cpp)  

- ##[659C-Tanya and Toys](http://codeforces.com/contest/659/problem/C)  
题意：  
有K元钱，买i号玩具需要花i元，给出已有的玩具，问最多可以有多少种玩具。  
解法：  
水水的贪心，尽量小就是了。  
  [code](https://github.com/zhyack/Codeforces/blob/master/659_Round%20%23346(Div.%202)/659C.cpp)  

- ##[659D-Bicycle Race](http://codeforces.com/contest/659/problem/D)  
题意：  
用有向边围成一个封闭多边形，问有几个有向边指向多边形内部。  
解法：  
计算几何唉，好激动~  
我的做法比较投机，就是将边(x1,y1)->(x2,y2)按期方向延伸一个单位，也就是(x2,y2)->(x2+dx,y2+dy)，看一下这个边在其垂直的负方向上存在于几个多边形的边上，其实和验证点在几何图形内部还是外部是一个道理(做射线，与图形交奇数个点，则在内部，否则在外部)。不过复杂度刚好是O(N^2)唉，虽然借助线段树显然可以把复杂度做到O(NlogN)。没看题解，不知道官方是怎么做的。  
  [code](https://github.com/zhyack/Codeforces/blob/master/659_Round%20%23346(Div.%202)/659D.cpp)  

- ##[659E-New Reform](http://codeforces.com/contest/659/problem/E)  
题意：  
N个点M条边，要求将每条边变成一个有向边，求最终最少有几个点没有入度。  
解法：  
这种题往聚类上想总是错不了= =。  
想想一棵树的话，变有向边，无论怎么变肯定都是有且仅有根没有入度，如果在树上随便加一条边，那就会构成一个环，以环内的任何一点为根，均可实现所有的点都有入度。所以问题就变成了求连通块，如果连通块中只能构成树，那么答案+1。并查集搞定。    
  [code](https://github.com/zhyack/Codeforces/blob/master/659_Round%20%23346(Div.%202)/659E.cpp)  

- ##[659F-Polycarp and Hay](http://codeforces.com/contest/659/problem/F)  
题意：  
要求将原矩阵中的数减小，使至少一个位置不变，非零数都相同且所在格子连通，所有数的和为K。  
解法：  
所有的条件就把出题人的意图表达的很清楚了，其实就是找到一个格子，让这个格子的数`val`不变(`K mod val = 0`)，然后只要这个格子存在一个连通块中的所有格子的原始值均大于等于`val`，且格子数大于等于`K/val`即可。  如果原始矩阵规模较小的话完全可以暴力做，但显然出题人是不会把暴力的题目放在F的。  
考虑我们要求的连通块的要求是“所有格子的原始值均大于等于`val`”，于是可以想到将所有格子按值从大到小排序，逐个加入与周围四个方向的满足值大于等于`val`的要求的格子求并查集，这样只要加入处理完某个格子(i,j)之后发现这个格子所在的并查集的格子总数满足大于等于`K/val`，就代表找到了一个可行解，此时应输出YES。时间复杂度只是O(N*M*log(N*M))。  
但这个时候这个格子(i,j)所在的并查集并不一定是答案中非零的区域，因为其格子数可能大于`K/val`，此时为了构造出一种答案可以以(i,j)为起点进行dfs或bfs找`K/val`个连通点即可。  
显然此题的代码工程较大，而且各种细节及其容易WA，博主当时WA到第98个点上生无可恋...  
  [code](https://github.com/zhyack/Codeforces/blob/master/659_Round%20%23346(Div.%202)/659F.cpp) 

- ##[659G-Fence Divercity](http://codeforces.com/contest/659/problem/G)  
题意：  
题目扯的很麻烦，其实就是说保留最后一行的情况下，从顶部去掉一个连通块，去掉的部分必须是每个stack的顶部，问有多少种去法。  
解法：  
显然dp。让我们先不考虑数据范围，想最暴力的做法——设dp[i][j]表示前i堆都合法的情况下第i堆去掉顶后高度为j的时候有多少种方法，则一般情况`dp[i][j] = sigma(dp[i-1][k]),其中0<j<h[i] && 0<k<min(h[i-1],h[i])`，特例也好分析，这里不再赘述。  
但是上述dp暴力写起来的话无疑是O(NH)的，所以就要考虑有什么特点。于是规范地画一画就很容易得到下图：  
![CF659G](https://zhyack.github.io/pics/CF346G.png)  
其实画的很明白了，`h[i-1]==h[i]`的情况可以算是任何一种情况的特例，整个dp[i]其实也就最多分为4段，`dp[i][0]=0，dp[i][1~h[i-1]-1]=v1, dp[i][h[i-1]~h[i]-1]=v2, dp[h[i]]=ans[i-1]，而h[i-1]>h[i]时认为h[i-1]=h[i]就可以将两种情况归为一种`，所以每一次dp只需要记下来v1,v2即可，其他都不用记录，dp复杂度是线性的O(N)。说到这儿主要难度在于计算dp[i]时候的v1,v2时要涉及dp[i-1]的v1和v2，容易乱掉，这个仔细画一画就明白了。  
最终的\\(ans_{N}\\)即为答案，初始化见代码自行思考吧。      
  [code](https://github.com/zhyack/Codeforces/blob/master/659_Round%20%23346(Div.%202)/659G.cpp) 

</section>