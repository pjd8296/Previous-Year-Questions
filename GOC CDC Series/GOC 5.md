## Good Substrings 2
A binary string is a string which contains only 0s and 1s. A binary string is called a good string if it contains equal number of 0s and 1s and the all the 0s and 1s are contiguous.
For instance 0011,01,1100,111000,000111 are good binary strings. However 0101,110010 are not because even though they contain equal number of 0s and 1s but the 0s and 1s are not together.
A substring of a string is a contiguous subsequence of that string. So, string "forces" is substring of string "codeforces", but string "coder" is not.

You are given a binary string S of length N , You need to find the number of good substrings of the given string.
```c++
#include <bits/stdc++.h>

using namespace std;

int main() {
    int t; cin>>t; 
    while(t--){
        int n; cin>>n; 
        string s; cin>>s; 
        vector<int> cnt = {0};      // stores length of blocks of same character
        for(int i = 0;i < n; ++i){
            if(i == 0 || s[i] == s[i - 1])cnt.back()++; 
            else cnt.push_back(1); 
        }

        long long ans = 0; 
        for(int i = 0;i + 1 < cnt.size(); ++i)ans += min(cnt[i], cnt[i + 1]); 
        cout<<ans<<"\n"; 
    }

    return 0;
}
```

## Superstition
Ojasv is very superstitious. He believes in everthing from black magic to cats crossing your path.

Today his horoscope tells him to avoid number `k` as much as possible. He comes across a string of lowercase english letters which has multiple `k` consecutive occurances of the same character and starts panicking. Help him get rid of all such occurances from the string.

Formally, given a string of length `N` keeping on removing `k` consecutive appearances of any character.

```c++
#include <bits/stdc++.h>

using namespace std;

int main(){
    int n, k; cin>>n>>k; 
    stack<pair<char, int> > st;
    string s; cin>>s; 

    for(char ch: s){
        if(st.empty() || ch != st.top().first)st.push({ch, 1}); 
        else st.push({ch, st.top().second + 1}); 
        
        while(!st.empty() && st.top().second >= k){
            for(int i = 0;i < k; ++i)st.pop(); 
        }
    }

    string ans = ""; 
    while(!st.empty())ans += st.top().first, st.pop(); 
    reverse(ans.begin(), ans.end()); 
    cout<<ans<<"\n"; 
    return 0;
}
```
