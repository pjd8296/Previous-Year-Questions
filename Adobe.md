* Given 2 strings, s1 and s2. Find a string s which is a concatenation of subsequence of s1 and subsequence of s2 and is longest possible palindrome and return its length.
```
Eg. s1 = ban, s2=ana. So answer is 5 ( ‘anana’).
Eg. s1 = abc, s2=abc.  So answer is 3 (‘aba’)
```
**Soln** :- Concat s1 and s2. Let s=s1+s2. t=reverse of s. Apply LCS on s and t, which is the answer. All test cases passed.

* Given a string s. Return substring of length 5 which occurs maximum times. If several of them exists, then you know what to do.
```
  Yes, return the lexicographically smallest one. 5<=N<=10^6.
  Eg. s= “bbbbbaaaaabbabababa. So answer is “ababa”.
  Eg. s=”heisagoodboy” So answer is “agood”.
```

* **Bus Stops**
<details>
  <summary>Floyd-Warshall Approach</summary>
  
![](https://lh3.googleusercontent.com/SHXRtAcqOIAyhjnvJHfWFCFb4DpTVviSOzUNmVOU4fZoTpn04Ppzo5A1YQ1qr-GCkeBKfKI8M2MNzGTzusNmMmi7nHycJfJwXHKz7JnTOcqrfaqHd0C0IQH7s2y-0JfVRSc1n43L)

</details>

* Find distance of each node with other, which can be min(reaching other node from left, reaching other node from right)
<details>
  <summary>O(N^2) Approach</summary>
  
```c++
#include <bits/stdc++.h>
using namespace std;

int n;
vector<int> arr;

int main()
{
    cin >> n;
    arr = vector<int>(n);
    int sum=0;
    for(int i=0;i<n;i++){
        cin >> arr[i];
        sum += arr[i];
    }
    int ans=0;
    for(int i=0;i<n;i++){
        int curr = i+1;
        int temp=0;
        while(curr != i){
            ans = max(ans,min(arr[i],sum-temp-arr[i]));
            temp+=arr[i];
            curr = (curr +1)%n;
        }
    }
    cout << ans<< endl;

    return 0;
}
```
</details>

* **Intersecting chords in a circle**

<details>
  <summary>Code</summary>

![](https://lh4.googleusercontent.com/85ChceCXyy4GLediMPE7zC__dtruLsPIlVXBqD-qEcGmZ7_XVJ-f3KEfEUtVuBTwZyky1J7YMa7ujI_VOhkloQ63BXV3hymZ_OVIJy5nPiioRbEmhmVCZZbVjheRiIyY1KwBkh17)

Think in terms of DP.
Can we relate answer for `N` with smaller answers.

If we draw a chord between any two points, can you observe current set of points getting broken into two smaller sets `S_1` and `S_2`? Can a chord be drawn between two points where each point belong to different set?

If we draw a chord from a point in `S_1` to a point in `S_2`, it will surely intersect the chord we’ve just drawn.

So, we can arrive at a recurrence that `Ways(n) = sum[i = 0 to n-1] { Ways(i)*Ways(n-i-1) }`.
Here we iterate over `i`, assuming that size of one of the sets is `i` and size of other set automatically is `(n-i-1)` since we’ve already used a pair of points and `i` pair of points in one set.


```c++
int Solution::chordCnt(int A) {
    int n = 2*A;
    vector<long long int> dp(n+1);
    dp[0] = 1;
    dp[2] = 1;
    for(int i = 4; i <= n; i++) {
        for(int j = 0; j <= i-2; j++) {
            dp[i] += dp[j] * dp[i-j-2];
            dp[i] %= 1000000007;
        }
    }
    return dp[n]%1000000007;
}
```
</details>

* **Given, an array of size n. Find an element that divides the array into two sub-arrays with equal sum.**

 <details>
    <summary>Solution</summary>

**Method 1** (Simple) 
Consider every element starting from the second element. Compute the sum of elements on its left and sum of elements on its right. If these two sums are same, return the element.

**Method 2** (Using Prefix and Suffix Arrays)

We form a prefix and suffix sum arrays

```
Given array: 1 4 2 5
Prefix Sum:  1  5 7 12
Suffix Sum:  12 11 7 5
```
Now, we will traverse both prefix arrays. The index at which they yield equal result, is the index where the array is partitioned with equal sum.

```c++

#include <bits/stdc++.h>
using namespace std;
 
int findElement(int arr[], int n)
{
    // Forming prefix sum array from 0
    int prefixSum[n];
    prefixSum[0] = arr[0];
    for (int i = 1; i < n; i++)
        prefixSum[i] = prefixSum[i - 1] + arr[i];
 
    // Forming suffix sum array from n-1
    int suffixSum[n];
    suffixSum[n - 1] = arr[n - 1];
    for (int i = n - 2; i >= 0; i--)
        suffixSum[i] = suffixSum[i + 1] + arr[i];
 
    // Find the point where prefix and suffix
    // sums are same.
    for (int i = 1; i < n - 1; i++)
        if (prefixSum[i] == suffixSum[i])
            return arr[i];
 
    return -1;
}
```
</details>

* **Maximum Number of Events That Can Be Attended**
  https://leetcode.com/problems/maximum-number-of-events-that-can-be-attended/
<details>
  <summary>Code</summary>

```c++
    int maxEvents(vector<vector<int>>& A) {
        priority_queue <int, vector<int>, greater<int>> pq;
        sort(A.begin(), A.end());
        int i = 0, res = 0, n = A.size();
        for (int d = 1; d <= 100000; ++d) {
            //Already expired no need to keeep
            while (pq.size() && pq.top() < d)
                pq.pop();
            //see what events can be attended today
            while (i < n && A[i][0] == d)
                pq.push(A[i++][1]);
            //attend any one that will end earlier
            if (pq.size()) {
                pq.pop();
                ++res;
            }
        }
        return res;
    }
 ```
 </details>

* **Rescue Operation**

<details>
  <summary>Code</summary>
  
![](https://lh3.googleusercontent.com/QnLrqfi-YM2i-GLisuXoH9PeWbZGhWDgULY4lCR7GvQLCbqJEvUGCZe0SSbyb8OxvXd5PyqwYq1XT60zRNOQDv8gLjh-ADQKJpKDyXrCyomQx7GxovTwIUenbeuQ-pYEZgp-yKZh)

Soln: Apply dijkstra from source to all the nodes and then from destination to all the nodes with edges reversed(which will be equivalent to finding distance from all nodes to the destination).
Answer will be the maximum of (distance of source to node) + (distance of node to destination)
</details>

* **Selling Products**

same as [this](https://leetcode.com/problems/least-number-of-unique-integers-after-k-removals/)

<details>
  <summary>Solution</summary>

```c++
class Solution {
public:
    int findLeastNumOfUniqueInts(vector<int>& arr, int k) {
        unordered_map<int, int> m;
        for(int x: arr)
            m[x]++;
        vector<pair<int, int>> v;
        for(auto& [k, val]: m)
            v.push_back({val, k});
        sort(v.begin(), v.end());
        int count = 0;
        int n = v.size();
        for(int i = 0; i < n; i++) {
            if(v[i].first <= k) {
                k -= v[i].first;
                count++;
            }
        }
        return n-count;
    }
};
```
</details>

* **String Patterns**
See [here](https://stackoverflow.com/questions/62816143/how-many-words-of-length-n-have-at-most-k-consecutive-vowels)

<details>
  <summary>Solution</summary>
  
```c++
   #include<bits/stdc++.h>
   #define mod 1000000007
   using namespace std;

   int solve(int wordLen, int maxVowels){
       long long dp[wordLen+1][2];

       dp[0][1] = dp[0][0] = 1;
       dp[1][1] = 21;
       dp[1][0]  = 5;

       for(int i  = 2;i<=wordLen;i++){

           dp[i][1] = (21*(dp[i-1][1]+dp[i-1][0])%mod)%mod;

           int k  = i, j = 1, p = 5;
           dp[i][0] = 0;

           while(k>0 && j<=maxVowels){
               dp[i][0] = (dp[i][0] + (p*dp[i-j][1])%mod)%mod;
               p = (p*5)%mod;
               k--;
               j++;
           } 
       }

       return (int)(dp[wordLen][0]+dp[wordLen][1])%mod;
   }

   int main(){
       cout<<solve(5, 3); 
       return 0;
   }
   ```
   </details>

* **Shortest Path in a grid**

See [here](https://leetcode.com/problems/shortest-path-in-a-grid-with-obstacles-elimination/)
<details>
  <summary>Solution</summary>

```c++
class Solution {
public:
    vector<int> dirX{0, 1, 0, -1};
    vector<int> dirY{-1, 0, 1, 0};
    
    int shortestPath(vector<vector<int>>& A, int k) {
        int m = A.size(), n = m ? A[0].size() : 0;
        vector<vector<vector<bool>>> visited(m, vector<vector<bool>>(n, vector<bool>(k+1, false)));
        queue<vector<int>> q;
        
        if(A[0][0]) {
            q.push({0,0,1});
            visited[0][0][1] = true;
        }
        else {
            q.push({0,0,0});
            visited[0][0][0] = true;
        }
        int count = 0;
        
        while(!q.empty()) {
            int qSize = q.size();
            for(int i = 0; i < qSize; i++) {
                vector<int> v = q.front(); q.pop();
                if(v[2] == k+1) continue;
                int x = v[0], y = v[1];
                if(x == m-1 and y == n-1)
                    return count;
                
                for(int dir = 0; dir < 4; dir++) {
                    int x1 = x + dirX[dir], y1 = y + dirY[dir];
                    
                    if(x1 >= 0 and y1 >= 0 and x1 < m and y1 < n) {
                    
                        if(A[x1][y1] and !visited[x1][y1][v[2]+1]) {
                            q.push({x1, y1, v[2]+1});
                            visited[x1][y1][v[2]+1] = 1;
                        }
                        else if(!A[x1][y1] and !visited[x1][y1][v[2]]) {
                            q.push({x1,y1,v[2]});
                            visited[x1][y1][v[2]] = 1;
                        }
                    }
                }
            }
            count++;
        }
        return -1;
    }
};
```
</details>
