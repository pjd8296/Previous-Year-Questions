## Ugly Numbers
<details>
  <summary>Code</summary>
  
```c++
class Solution {
public:
    int nthUglyNumber(int n) {
        if(n <= 0) return false; // get rid of corner cases 
        if(n == 1) return true; // base case
        int t2 = 0, t3 = 0, t5 = 0; //pointers for 2, 3, 5
        vector<int> k(n);
        k[0] = 1;
        for(int i  = 1; i < n ; i ++)
        {
            k[i] = min(k[t2]*2,min(k[t3]*3,k[t5]*5));
            if(k[i] == k[t2]*2) t2++; 
            if(k[i] == k[t3]*3) t3++;
            if(k[i] == k[t5]*5) t5++;
        }
        return k[n-1];
    }
};
```
</details>

## Scatter Palindrome

<details>
  <summary>Solution</summary>

```c++
#include<bits/stdc++.h>
using namespace std;
int ans = 0;
bool isPal(string& s) {
    unordered_map<char, int> m;
    for(char c: s)
        m[c]++;
    int count = 0;
    for(auto& k: m) {
        if(k.second == 1)
            count++;
        if((count > 1) or ((k.second > 1 and (k.second)%2 == 1)))
            return false;
    }
    return true;
}
void backtrack(string& s, int i, int n) {
    if(i == n) return;
    for(int j = 0; j < n-i; j++) {
        string str = s.substr(i, j+1);
        //cout << str<< endl;
        if(isPal(str)) ans++;
    }
    backtrack(s, i+1, n);
}
int main() {
    int n;
    cin >> n;
    vector<string> expr;
    for(int i = 0; i < n; i++) {
        string s;
        cin >> s;
        expr.push_back(s);
    }
    vector<int> dp(n);
    for(int i = 0; i < n; i++) {
        backtrack(expr[i], 0, expr[i].size());
        dp[i] = ans;
        ans = 0;
    }
    for(auto x: dp)
        cout << x << " ";
}
```
</details>
