1. Activity selection problem (start time and duration given. At any time only one activity can be done. Select the most number of activities.)
<details>
 <summary>Solution</summary>
 
 ```c++
 bool activityCompare(Activitiy s1, Activitiy s2) { 
    return (s1.finish < s2.finish); 
} 
// Returns count of the maximum set of activities that can 
// be done by a single person, one at a time. 
void printMaxActivities(Activitiy arr[], int n) { 
    // Sort jobs according to finish time 
    sort(arr, arr+n, activityCompare); 
    cout << "Following activities are selected n"; 
  
    // The first activity always gets selected 
    int i = 0; 
    cout << "(" << arr[i].start << ", " << arr[i].finish << "), "; 
  
    // Consider rest of the activities 
    for (int j = 1; j < n; j++) 
    { 
      // If this activity has start time greater than or 
      // equal to the finish time of previously selected 
      // activity, then select it 
      if (arr[j].start >= arr[i].finish) 
      { 
          cout << "(" << arr[j].start << ", "
              << arr[j].finish << "), "; 
          i = j; 
      } 
    } 
} 
```
___
```c++
void SelectActivities(vector<int>s,vector<int>f){ 
// Vector to store results. 
    vector<pair<int,int>>ans; 
// Minimum Priority Queue to sort activities in ascending order of finishing time (f[i]). 
  
    priority_queue<pair<int,int>,vector<pair<int,int>>,greater<pair<int,int>>>p; 
  
    for(int i=0;i<s.size();i++){ 
        // Pushing elements in priority queue where the key is f[i] 
        p.push(make_pair(f[i],s[i])); 
    } 
    auto it = p.top(); 
    int start = it.second; 
    int end = it.first; 
    p.pop(); 
    ans.push_back(make_pair(start,end)); 
  
    while(!p.empty()){ 
        auto itr = p.top(); 
        p.pop(); 
        if(itr.second >= end){ 
            start = itr.second; 
            end = itr.first; 
            ans.push_back(make_pair(start,end)); 
        } 
    } 
    cout << "Following Activities should be selected. " << endl << endl; 
  
    for(auto itr=ans.begin();itr!=ans.end();itr++){ 
        cout << "Activity started at: " << (*itr).first << " and ends at  " << (*itr).second << endl; 
    } 
} 
```
</details>

2. You are given two strings s and t. |s|>=|t|  You need to determine whether t can be concatenated multiple times to obtain s. Also if this is possible to do then you need to output the smallest string x such that both s and t can be obtained from x by some number of concatenations. (*Hint: Use KMP*)
<details>
 <summary>Solution</summary>
 
```c++
void computeLPSArray(char str[], int M, int lps[]) 
{ 
    int len = 0; //lenght of the previous longest prefix suffix 
    int i = 1; 
    lps[0] = 0; //lps[0] is always 0 
    // the loop calculates lps[i] for i = 1 to M-1 
    while (i < M) 
    { 
       if (str[i] == str[len]) 
       { 
           len++; 
           lps[i] = len; 
           i++; 
       } 
       else // (pat[i] != pat[len]) 
       { 
          if (len != 0) 
          { 
             len = lps[len-1]; 
             // Also, note that we do not increment i here 
          } 
          else // if (len == 0) 
          { 
             lps[i] = 0; 
             i++; 
          } 
       } 
    } 
} 
// Returns true if str is repetition of one of its substrings 
// else return false. 
bool isRepeat(char str[]) 
{ 
    // Find length of string and create an array to 
    // store lps values used in KMP 
    int n = strlen(str); 
    int lps[n]; 
    // Preprocess the pattern (calculate lps[] array) 
    computeLPSArray(str, n, lps); 
    // Find length of longest suffix which is also 
    // prefix of str. 
    int len = lps[n-1];
    // If there exist a suffix which is also prefix AND Length of the remaining substring divides total 
    // length, then str[0..n-len-1] is the substring that repeats n/(n-len) times (Readers can print substring 
    // and value of n/(n-len) for more clarity. 
    return (len > 0 && n%(n-len) == 0)? true: false; 
} 
```
</details>

3. You are given three types of moves of the form ‘./’ ‘../’ ‘x/’. These moves represent folder transitions. You are given a sequence of such moves. You need to output the minimum steps you need to take from the last location  to reach the root.

4. You are given two numbers a and b. Determine the sum s for which maximum numbers between a and b( inclusive) have their sum of digits equal to s and also the number of times this sum s occurs.
(Brute force won't pass. `a,b <=1e18`)
 Solution: [Digit DP](https://www.google.com/url?q=https://ide.geeksforgeeks.org/O3XN7ByK7J&sa=D&ust=1601697539873000&usg=AOvVaw23w_Ep5PkeyjIKRc8ONYAk)

5.  Array subset. Given an array, find a minimal subset of it such that the sum of its numbers is greater than the sum of numbers in the remaining subarray.

6. Shopping Budget. Arrays of prices of jeans, skirts, shoes, etc were given, and the budget. Have to figure out no. of ways in which we can buy all the items in given budget.
Eg. `a=[1,2,3] b=[2,3] c=[4] d=[1,2,3]` (Brute force did not pass 4/12 test cases)
(*Hint: Can be done using 4 sum. 2 loops for first 2 arrays and 3rd loop for rest 2 arrays. Passed all test cases.*)

7. Dodge the Ball. (Hard level question)
8. Question on string where you had to first apply regex and then count number of allowed substrings.
