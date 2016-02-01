<section>
#Codeforces Round #341 (Div. 2)
- [contest link](http://codeforces.com/contest/621)  
  

　　CF#341，难度一般，全是数学题！！！<img src="../emojis/joy.png" alt="joy_with_tears" height="30"><br>  
　　最近对于这种非常规的出题方式实在是感到很无力，不过比赛时确实是智商感人，什么都想不到。涉及的数学知识不难，D题比较坑，其他题都是会者不难。  

- ##[621A-Wet Shark and Odd and Even](http://codeforces.com/contest/621/problem/A)  
题意：  
　　给出N个数，求其最大偶数和。  
解法：  
　　`奇+偶=奇`，`偶+偶=偶`，`奇-偶=奇`，`奇-奇=偶`  
　　如果总和是奇数，那么至少N个数中有一个奇数；然后要知道从这N个数中剔除偶数是没有意义的。所以做法就是从总和中减去最小奇数，没有奇数的话就不减了。
  　　
  　　  
  [code](https://github.com/zhyack/Codeforces/blob/master/621_Round%20%23341(Div.%202)/621A.cpp)  

- ##[621B-Wet Shark and Bishops](http://codeforces.com/contest/621/problem/B)  
题意：  
　　1000*1000的棋盘，放N个国际象棋的象，求其相互攻击的象的对数。  
解法：  
　　N^2两两判断当然是不行的，但注意相互攻击的象必然是一条斜线上的，那就遍历棋盘中所有的斜线，也就2000条左右，对于某条斜线上有x个象的话，`ans+=(x-1)*x/2`，当然这样写起来很蠢的。  
　　要注意到每条斜线要么是x+y一致，要么是x-y一致，所以根据这两个值统计即可。附上我智商不够只能用复制粘贴弥补的渣代码。
  　　
  　　
  　　  
  [code](https://github.com/zhyack/Codeforces/blob/master/621_Round%20%23341(Div.%202)/621B.cpp)  

- ##[621C-Wet Shark and Flowers](http://codeforces.com/contest/621/problem/C)  
题意：  
　　N个人坐成圆桌，每个人可以随机一个[li,ri]的数字，对于每两个相邻的人来说，如果任一个人的数字可以整除P，则两个人均可获得1000刀的奖励。问所有人的期望奖励值。  
解法：  
　　单独就每个人的期望考虑，然后加和即可。比如对于第`i`个人，如果他持有的数字可以被P整除，那么无论是`(i,i+1)`，还是`(i,i-1)`，他都可以获得1000；如果他持有的数字不能被P整除，那么只有第`i+1`个人持有的数字可以被P整除，第`i`个人才能获得`(i,i+1)`提供的1000，只有第`i-1`个人持有的数字可以被P整除，第`i`个人才能获得`(i,i-1)`提供的1000。  
　　所以我们要求出的是对于每个人来说，他持有的数字可以被P整除的概率`p[i]`，显然`p[i] = (r[i]/P-(l[i]-1)/P)/(r[i]-l[i]+1)`。然后对于第i个人，他获得奖励的期望即是`p[i]*2000 + (1-p[i])*p[i+1]*1000 + (1-p[i])*p[i-1]*1000`。  　　
  　　
  　　  
  [code](https://github.com/zhyack/Codeforces/blob/master/621_Round%20%23341(Div.%202)/621C.cpp)  

- ##[621D-Rat Kwesh and Cheese](http://codeforces.com/contest/621/problem/D)  
题意：  
　　给出0.1<=x,y,z<=200，求题目中的12个式子的最大值对应的式子。  
解法：  
　　废话不多说，基本上就是对每个式子求两遍log，然后就能把数值控制在可接受范围内。需要注意的是：比如第一个式子两次log之后是`z*log(y)+log(log(x))`，如果`x<=1`的话`log(x)<=0`，`log(log(x))`就呵呵了，所以需要注意各种`<=1`的情况。  
　　还好情况不算很复杂，因为如果`x<=1,y<=1,z<=1`，还log什么，直接pow算不就得了。否则只要存在任一x或y或z大于1，比如`x>1，y<=1，z<=1`，那么x为底的式子一定是值大于1的，而y,z对应的式子都是小于等于1的，所以y，z的式子都不予考虑，其他类似情况如法炮制。具体操作见代码。  
　　不过话说我之前把各种`<=1`写成`<1`竟然也过了，log(0)，嗯<img src="../emojis/anguished.png" alt="anguished" height="30">...
  　　
  　　
  　　  
  [code](https://github.com/zhyack/Codeforces/blob/master/621_Round%20%23341(Div.%202)/621D.cpp)  

- ##[621E-Wet Shark and Blocks](http://codeforces.com/contest/621/problem/E)  
题意：  
　　给N个数字，每次从中挑出一个数字，共挑B次，依次组成一个大数，如果大数除X后等于K，那么算是一种合法情况，求合法情况的个数。  
解法：  
　　`dp[i][j]`表示前i个数字组成的大数除X后等于j的方案数，`a[i]`表示给出的N个数中数字i的个数，显然`dp[i][j] = ∑dp[i-1][k]*a[d]`，其中`(k*10+d)%X = j`。但是B太大了，这个dp需要优化。  
　　这种形式(\* 和∑)很容易可以想到矩阵乘法，所以向量v(1\* X)，`v[i]`表示当前求得余数i的方案数，矩阵mat(X\* X)，`mat[k][j]`表示从当前状态余数k转移到下一个状态余数j的方案数，显然`mat[k][j] = ∑a[d]`，其中`(k*10+d)%X = j`。所以B次转移之后的结果应该是初始向量v0(只有`v0[0] = 1`，其他均是0)，`vB = v0*(mat)^B`，答案要的是`vB[K]`。`(mat)^B`用快速幂来做，不再赘述。总体复杂度是O(K^3*logN)。
  　　
  　　  
  [code](https://github.com/zhyack/Codeforces/blob/master/621_Round%20%23341(Div.%202)/621E.cpp)  
</section>