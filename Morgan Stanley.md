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
# Maximize j-i such that A[j] >= A[i]
```c++
int maxIndexDiff(int arr[], int n)
{
    int maxDiff;
    int i, j;
 
    int* LMin = new int[(sizeof(int) * n)];
    int* RMax = new int[(sizeof(int) * n)];
 
    /* Construct LMin[] such that 
    LMin[i] stores the minimum value 
    from (arr[0], arr[1], ... arr[i]) */
    LMin[0] = arr[0];
    for (i = 1; i < n; ++i)
        LMin[i] = min(arr[i], LMin[i - 1]);
 
    /* Construct RMax[] such that 
    RMax[j] stores the maximum value from 
    (arr[j], arr[j+1], ..arr[n-1]) */
    RMax[n - 1] = arr[n - 1];
    for (j = n - 2; j >= 0; --j)
        RMax[j] = max(arr[j], RMax[j + 1]);
 
    /* Traverse both arrays from left to right
    to find optimum j - i. This process is similar to 
    merge() of MergeSort */
    i = 0, j = 0, maxDiff = -1;
    while (j < n && i < n) {
        if (LMin[i] < RMax[j]) {
            maxDiff = max(maxDiff, j - i);
            j = j + 1;
        }
        else
            i = i + 1;
    }
 
    return maxDiff;
}
```
