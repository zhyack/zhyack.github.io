<section>
#Codeforces Round #340 (Div. 2)
- [contest link](http://codeforces.com/contest/617)  
  

　　CF#340，题目较简单，坑多。小号([zhy](http://codeforces.com/profile/zhy))踩雷，最近第一次跪得这么惨，总结一下——尝试先开了C导致心态不稳，重点还是So weak~  

- ##[617A-Elephant](http://codeforces.com/contest/617/problem/A)  
题意：  
　　从0走到x，每次只能+1~5，问最少多少步。  
解法：  
　　贪心地——能走+5就走+5，最后一步如果不足+5再微调，其实就是+5走`x/5`步，如果剩下的还有，就再走个+(`x%5`)。
  　　
  　　  
  [code](https://github.com/zhyack/Codeforces/blob/master/617_Round%20%23340(Div.%202)/617A.cpp)  

- ##[617B-Chocolate](http://codeforces.com/contest/617/problem/B)  
题意：  
　　把01序列分成若干段，保证每段中有且仅有一个1，问有多少种分法。  
解法：  
　　前缀0和后缀0都是没用的，肯定会跟着第一个1和最后一个1，其他的每两个1之间0的个数其实就是这两个1之间能划分的方案数，统计一下各个0串的长度，相乘即为答案。  
　　注意全0的情况，还有`1001001001001...`这种情况，会产生超过32位整型的答案。
  　　
  　　  
  [code](https://github.com/zhyack/Codeforces/blob/master/617_Round%20%23340(Div.%202)/617B.cpp)  

- ##[617C-Watering Flowers](http://codeforces.com/contest/617/problem/C)  
题意：  
　　给出两个圆心的位置，以及平面上的N个点的位置，要求两个圆覆盖所有的点，求最小的`r1^2+r2^2`。  
解法：  
　　要明确，r1和r2一定是相应圆心到某点的距离——因为再长了也并没有什么乱用。所以r1和r2都有**N+1**中选择，注意存在`r1,r2 = 0`的情况。所以就是求出所有的r1,r2取值(到N个点距离)，排序后，两个指针一个r1从小到大，一个r2从大到小，时刻满足恰好覆盖所有的点，找出 `r1^2+r2^2` 最小值即可，具体操作细节见代码。　　
  　　
  　　  
  [code](https://github.com/zhyack/Codeforces/blob/master/617_Round%20%23340(Div.%202)/617C.cpp)  

- ##[617D-Polyline](http://codeforces.com/contest/617/problem/D)  
题意：  
　　给出3个点，只能用平行于坐标轴的折线来连接，问折线至少几段。  
解法：  
　　刷新世界观，这是D题难度？虽然比较坑...  
　　`x1 = x2 = x3` 或 `y1 = y2 = y3` —— 1条直线即可。  
　　一条边平行于坐标轴，且这条边的一端是直角或钝角，也就是说第三个点在这条边“外侧” —— 2条折线即可。直角或钝角判断可以用 `a^2+b^2 <= c^2`，也可以通过坐标写出复杂的布尔表达式，见代码。  
　　其他情况 —— 3条折线。  
  [code](https://github.com/zhyack/Codeforces/blob/master/617_Round%20%23340(Div.%202)/617D.cpp)  


</section>