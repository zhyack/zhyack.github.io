<section>
#Codeforces Educational Round #4
- [contest link](http://codeforces.com/contest/612)  
  

　　隐约感到了一大波低质量比赛在接近...  

- ##[612A-The Text Splitting](http://codeforces.com/contest/612/problem/A)  
题意：  
　　给一个长为n字符串，要求恰好拆成长为p或q的若干子串。 　　  
解法：  
　　其实就是n = xp+yq嘛，范围还这么小，枚举x求y，都是整数即可。　　
  　　  
  [code](https://github.com/zhyack/Codeforces/blob/master/612_Educational%20Round%234/612A.cpp)  

- ##[612B-HDD is Outdated Technology](http://codeforces.com/contest/612/problem/B)  
题意：  
　　硬盘n个扇区，各有标号1~n，从第i个移动到第j个需要`abs(i-j)`的时间，问按顺序遍历标号为1，2，3,..,n的扇区需要多长时间。　  
解法：  
　　记一下各标号的位置，扫一遍。  　　
  　　  
  [code](https://github.com/zhyack/Codeforces/blob/master/612_Educational%20Round%234/612B.cpp)  

- ##[612C-Replace To Make Regular Bracket Sequence](http://codeforces.com/contest/612/problem/C)  
题意：  
　　括号序列可能包含'{' , '}' , '(' , ')' , '[' , ']' , '<' , '>'这几种括号，任意的左括号都可以和右括号匹配，但是如果他们不是同一类型的就要花费一个单位的代价，问整体括号匹配的最小代价。　  
解法：  
　　只需要注意到这一点——每个右括号所能匹配的左括号是唯一的。所以按经典的括号匹配做，如果发现栈顶的左括号类型不一样那就ans++。 　　
  　　  
  [code](https://github.com/zhyack/Codeforces/blob/master/612_Educational%20Round%234/612C.cpp)  

- ##[612D-The Union of k-Segments](http://codeforces.com/contest/612/problem/D)  
题意：  
　　有n个区间，可能相互有重叠部分，问坐标轴上被重叠了k次的区间。　  
解法：  
　　裸的线段树，树状数组也可，当然还是要离散化一下。区间更新，单点询问。每次把区间[li,ri]都加1，最后扫描一遍各个点，看值是否大于等于k。需要注意的是这种情况——[1,3],[3,3],k=2,答案应该是[3,3]，这个要看边界处理的手法了，可参考我的代码。复杂度O(nlogn)。  
　　当然，这道题有更简单的做法，离散化之后排序，然后从左往右做类似于扫描线的事情，可以完美解决问题。复杂度还是O(nlogn)的，但编起来很容易了，边界也好处理。
  　　  
  [code](https://github.com/zhyack/Codeforces/blob/master/612_Educational%20Round%234/612D.cpp)  

- ##[612E-Square Root of Permutation](http://codeforces.com/contest/612/problem/E)  
题意：  
　　排列q的平方p的定义是p[i] = q[q[i]]。现给出p，问q是什么。    
解法：  
　　这题想了很久都没思路，结果看别人的做法是像找规律一样，真是醉了...  
code  
</section>