## Jhul and Distinct numbers
Jhul has an array of `N` integers. His crush has challenged him to find the length of smallest sub-array that contains all the distinct elements of array. Jhul, being a dumb fellow, was unable to do that. So, now he seeks your help.
```
Sample Input 0
10
1 2 1 2 3 5 4 4 1 2
Sample Output 0
5
```
```c++
int main() {
    /* Enter your code here. Read input from STDIN. Print output to STDOUT */  
    ios_base::sync_with_stdio(false);
    cin.tie(NULL); cout.tie(NULL);
    int n;
    cin >> n;
    vector<int> A(n);
    for(int& x: A)
        cin >> x;
    unordered_map<int, int> m;
    for(int x: A)
        m[x]++;
    int mSize = m.size();
    m.clear();
    int Min = INT_MAX, i = 0, j = 0;
    while(j < n) {
        m[A[j]]++;
        while(mSize == (int)m.size()) {
            m[A[i]]--;
            if(!m[A[i]])
                m.erase(A[i]);
            i++;
            Min = min(Min, j-i+2);
        }
        j++;
        
    }
    cout << Min <<endl;
}
```
## Date with a crush
N x M grid, R - your location(start), E - crush's location, P - obstacle, O - valid
```c++
#include <bits/stdc++.h>
#define ll long long
using namespace std;

int main() {
    int n, m;
    cin >> n >> m;
    vector<string> A;
    for(int i = 0; i < n; i++) {
        string str;
        cin >> str;
        A.push_back(str);
    }
    queue<pair<int, int>> q;
    int offset[] = {0, -1, 0, 1, 0};
    pair<int, int> start, end;
    for(int i = 0; i < n; i++) {
        for(int j = 0; j < m; j++) {
            if(A[i][j] == 'R') {
                start = {i, j};
                q.push({i, j});
            }
            else if(A[i][j] == 'E')
                end = {i, j};
        }
    }
    vector<vector<int>> d(n, vector<int> (m, INT_MAX));
    d[start.first][start.second] = 0;
    while(!q.empty()) {
        int qSize = q.size();
        for(int i = 0; i <qSize; i++) {
            auto p = q.front(); q.pop();
            for(int j = 0; j < 4; j++) {
                int r = p.first+offset[j], c = p.second+offset[j+1];
                if(r>=0 and c >=0 and r<n and c<m and A[r][c] != 'P') {
                    if(d[r][c] > 1 + d[p.first][p.second]) {
                        d[r][c] = 1 + d[p.first][p.second];
                        q.push({r, c});
                    }
                }
            }
        }
    }
    cout << d[end.first][end.second] << endl;
}
```
