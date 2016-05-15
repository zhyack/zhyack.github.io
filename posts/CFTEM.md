###dp[j]:  j = h[i]
\\(dp\_{j} = \displaystyle\sum\_{k=0}^{h\_{i-1}}dp\_{i-1,k}\\)  
###dp[j]:  0<j<h[i]  
\\(dp\_{j} = \displaystyle\sum\_{k=1}^{h\_{i}-1}dp\_{i-1,k}+1\\)

###dp[j]:  j = h[i]
\\(dp\_{j} = \displaystyle\sum\_{k=0}^{h\_{i-1}}dp\_{i-1,k}\\)  
###dp[j]:  h[i-1]<=j<h[i]  
\\(dp\_{j} = 1\\)  
###dp[j]:  0<j<h[i-1]  
\\(dp\_{j} = \displaystyle\sum\_{k=1}^{h\_{i-1}-1}dp\_{i-1,k}+1\\)

\\(ans\_{i} = \displaystyle\sum dp\_{j}\\)