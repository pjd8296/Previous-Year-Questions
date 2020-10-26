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
