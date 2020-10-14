# Minimum lines to cover all points

```c++
int gcd(int a, int b) 
{ 
    if (b == 0) 
        return a; 
    return gcd(b, a % b); 
} 
  
//    method returns reduced form of dy/dx as a pair 
pair<int, int> getReducedForm(int dy, int dx) 
{ 
    int g = gcd(abs(dy), abs(dx)); 
    //get sign of result 
    bool sign = (dy < 0) ^ (dx < 0); 
  
    if (sign) 
        return make_pair(-abs(dy) / g, abs(dx) / g); 
    else
        return make_pair(abs(dy) / g, abs(dx) / g); 
} 
  
/*  method returns minimum number of lines to 
    cover all points where all lines goes through (xO, yO) */
int minLinesToCoverPoints(int points[][2], int N, int xO, int yO) 
{ 
    //    set to store slope as a pair 
    set< pair<int, int> > st; 
    pair<int, int> temp; 
    int minLines = 0; 
  
    //    loop over all points once 
    for (int i = 0; i < N; i++) 
    { 
        //    get x and y co-ordinate of current point 
        int curX = points[i][0]; 
        int curY = points[i][1]; 
  
        temp = getReducedForm(curY - yO, curX - xO); 
  
        // if this slope is not there in set, increase ans by 1 and insert in set 
        if (st.find(temp) == st.end()) { 
            st.insert(temp); 
            minLines++; 
        } 
    } 
    return minLines; 
} 
```
# Largest Subarray of equal 0's and 1's
For explanation, visit [here](https://leetcode.com/problems/contiguous-array/solution/)
```c++
    int findMaxLength(vector<int>& A) {
        int n = A.size();
        unordered_map<int, int> m;
        m[0] = -1;
        int maxLen = 0, sum = 0;
        for(int i = 0; i < n; i++) {
            sum += (A[i] == 0) ? -1 : 1;
            if(m.count(sum))
                maxLen = max(maxLen, i - m[sum]);
            else
                m[sum] = i;
        }
        return maxLen;
    }
 ```
