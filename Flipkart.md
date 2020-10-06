## Maximum product of non overlapping palindromes
For input string `"acdapmpomp"`, we can choose `"aca"` and `"pmpmp"` to get a maximal product of score 3 * 5 = 15.

**Solution**

Firstly you should traverse the dp table to find out the length of longest palindromic subsequences using bottom up approach, then you can calculate the max product by multiplying `dp[i][j]` with `dp[j+1][n-1]`
```c++
int longestPalindromicSubsequenceProduct(string s){
int n = s.size();
vector<vector<int>> dp(n,vector<int>(n,0));
for(int i = n-1; i >= 0; i--) {
  dp[i][i] = 1;
  for(int j = i+1; j < n; j++) {
    dp[i][j] = (s[i] == s[j]) ? 2 + dp[i+1][j-1] : max(dp[i][j-1], dp[i+1][j]);
  }
}
int maxProd = 0;
for(int i=0;i<n;i++){
    for(int j=0;j<n-1;j++){
        maxProd = max(maxProd,dp[i][j]*dp[j+1][n-1]);
      }
   }
  return maxProd;
}
```
