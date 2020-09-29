1. Given 2 strings, s1 and s2. Find a string s which is a concatenation of subsequence of s1 and subsequence of s2 and is longest possible palindrome and return its length.
```
Eg. s1 = ban, s2=ana. So answer is 5 ( ‘anana’).
Eg. s1 = abc, s2=abc.  So answer is 3 (‘aba’)
```
**Soln** :- Concat s1 and s2. Let s=s1+s2. t=reverse of s. Apply LCS on s and t, which is the answer. All test cases passed.

2. (Need to solve) Given a string s. Return substring of length 5 which occurs maximum times. If several of them exists, then you know what to do.
```
  Yes, return the lexicographically smallest one. 5<=N<=10^6.
  Eg. s= “bbbbbaaaaabbabababa. So answer is “ababa”.
  Eg. s=”heisagoodboy” So answer is “agood”.
```

3. **Floyd-Warshall Approach**
![](https://lh3.googleusercontent.com/SHXRtAcqOIAyhjnvJHfWFCFb4DpTVviSOzUNmVOU4fZoTpn04Ppzo5A1YQ1qr-GCkeBKfKI8M2MNzGTzusNmMmi7nHycJfJwXHKz7JnTOcqrfaqHd0C0IQH7s2y-0JfVRSc1n43L)

**`O(N^2)` Approach**
* Find distance of each node with other, which can be min(reaching other node from left, reaching other node from right)
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

4. Intersecting chords in a circle

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
