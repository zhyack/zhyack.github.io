<section>
#Codeforces Round #336
- [contest link](http://codeforces.com/contest/608)  
  
　　CF#336，题目较简单，个人感觉A-D没什么亮点，E题没看太懂= =。作死熬夜玩了一场，还是低分的小号([zhy](http://codeforces.com/profile/zhy))做的，涨了一些rating，不过rank 81才涨这么点分，真的是没有以前好上分了,估计想追上大号([Des_Payfor](http://codeforces.com/profile/Des_Payfor))还得再来一场rank前百的，争取GoodBye 2015上‘低分’大号。  

- ##[608A-Saitama Destroys Hotel](http://codeforces.com/contest/608/problem/A)  
题意：  
　　电梯从M层下到0层，给出N个人所在楼层，到达电梯口的时间，电梯每下一层需要1的时间，求电梯带上所有人下到0层所用时间。 　　  
解法：  
　　熟悉的电梯水题，电梯容量无限...对于第i个人来说，最早的到达0层的时间其实就是fi+ti，求一下max{fi+ti,M}就ok了，不过模拟一下过程也不费劲。  　　
  　　  
  [code](https://github.com/zhyack/Codeforces/blob/master/608_Round%20%23336(Div.%202)/608A.cpp)  

- ##[608B-Hamming Distance Sum](http://codeforces.com/contest/608/problem/B)  
题意：  
　　Hamming距离，也就是按位异或值的和。求串a对应串b中所有长尾|a|的子串的Hamming距离和。  
解法：  
　　误入歧途，做完D才想到怎么做这题...不要企图整串算值，可以按位考虑。a[i]能对答案的贡献，其实就是`a[i]`与`b[i],b[i+1]...b[i+ |b|-|a| ]`这些值异或的和，因为a[i]一位一位后移，总体能对应上的也就是b的这些位置。  
　　要求a[i]对答案的贡献，也就是如果`a[i]=='0'`那就要找`b[i],b[i+1]...b[i+ |b|-|a| ]`这些位置中'1'的个数，反之亦然。求个数的话，前缀和就可以搞定了——ones[i]表示`b[1]...b[i]`中'1'的个数(这里位置从1开始记)，求`b[i],b[i+1]...b[i+ |b|-|a| ]`中'1'的个数就是`ones[i+ |b|-|a|]-ones[i-1]`，zeros也同样处理。  
　　还有要吐槽的，这题怎么大家都long long了 →\_→ 一定是pretest太强...
  　　  
  [code](https://github.com/zhyack/Codeforces/blob/master/608_Round%20%23336(Div.%202)/608B.cpp)  

- ##[608C-Chain Reaction](http://codeforces.com/contest/608/problem/C)  
题意：  
　　N个新标，第i个信标位置a[i]，能量b[i]，从右向左放置，如果当前信标位置a[i]被其右边的信标能量范围覆盖[ a[i+1]-b[i+1] , a[i+1] ]，那么当前信标失效。现在，我们可以在最右侧任何位置添加一个能量范围任意大的信标，问最少能有几个信标失效。  
解法：  
　　很直观的dp，dp[i]表示第i个信标存活的情况下，前i个信标最多能有几个有效的。那么有转移方程`dp[i] = dp[j]+1`，其中j是不受i的能量影响的最靠右的信标，当然，如果j不存在，dp[j]应当替换为0。具体找j的方法就是二分查找，由于题目保证一个位置最多一个信标，所以lower\_bound和upper\_bound都可以啦。  
　　最后需要提醒的是，题目里可没有说给出的信标是按位置排好序的，然而做完这题我第一时间锁住题目，竟然从头到尾没有找到忘记sort的-\_-||，现在的参赛者们都这么警惕了吗...
  　　
  　　
  　　  
  [code](https://github.com/zhyack/Codeforces/blob/master/608_Round%20%23336(Div.%202)/608C.cpp)  

- ##[608D-Zuma](http://codeforces.com/contest/608/problem/D)  
题意：  
　　对于一个序列，每次操作可以消掉一个回文串，问最少多少次操作消掉全部序列。  
解法：  
　　这种题十有八九就是区间dp，再看看范围N<=500，那就确信是N^3的区间dp了。  
　　`dp[i][j]`表示[i,j]这个区间的序列最少多少操作能消掉，那么分解成子问题就是把序列切成2段，一段[i,p]是与i这个位置一起消掉的序列，其中`c[p]==c[i]`（因为如果`c[p]!=c[i]`，那么一定可以转化为`dp[i,p']+dp[p'+1,p]+dp[p+1,j] >= dp[i,p']+dp[p'+1][j]`,其中`p'<p且c[p']==c[i]`)；另一段是[p+1,j]，一定是之前求过的子问题。  
　　需要注意各种边界情况，比如，`i==p` 、 `p==j` 等。还有dp[i,p]这一段，如果`i+1==p`，也就是i和p之间没有回文子串，那么dp[i][p] = 1，否则dp[i][p] = dp[i+1][p-1]，因为内部如果已经有串的话，消掉(c[i],c[p])这个回文对，应该是“顺便”消掉的，可以自行理解一下最后一个样例。  
　　当然还有——如果对区间dp不熟悉的话，请参考代码，前两维并不是枚举左右边界，而是要枚举区间长度和左/右边界，这样才能一点一点拓宽区间。 　　　
  [code](https://github.com/zhyack/Codeforces/blob/master/608_Round%20%23336(Div.%202)/608D.cpp)  

- ##[608E-Marbles](http://codeforces.com/contest/608/problem/E)  
题意：  
　　待续吧... 　　  
解法：  
  　　
  　　
  　　
  　　  
  code  
</section>