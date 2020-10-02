## Length of the smallest sub-string consisting of maximum distinct characters
<details>
  <summary>Code</summary>
  
```c++
string findSubString(string str) 
{ 
    int n = str.length(); 
    int dist_count = 0; 
    bool visited[MAX_CHARS] = { false }; 
    for (int i = 0; i < n; i++) { 
        if (visited[str[i]] == false) { 
            visited[str[i]] = true; 
            dist_count++; 
        } 
    } 
    int start = 0, start_index = -1, min_len = INT_MAX; 
    int count = 0; 
    int curr_count[MAX_CHARS] = { 0 }; 
    for (int j = 0; j < n; j++) { 
        // Count occurrence of characters of string 
        curr_count[str[j]]++; 
        // If any distinct character matched, then increment count 
        if (curr_count[str[j]] == 1) 
            count++; 
  
        // if all the characters are matched 
        if (count == dist_count) { 
            while (curr_count[str[start]] > 1) { 
                if (curr_count[str[start]] > 1) 
                    curr_count[str[start]]--; 
                start++; 
            } 
            int len_window = j - start + 1; 
            if (min_len > len_window) { 
                min_len = len_window; 
                start_index = start; 
            } 
        } 
    } 
    return str.substr(start_index, min_len); 
} 
```
</details>

## Other Questions
<details>
  <summary>Images</summary>
  
![](https://i.imgur.com/tXUK53W.png)  
![](https://i.imgur.com/ztdeKAg.png)
![](https://i.imgur.com/fp5BNST.png)
![](https://i.imgur.com/xiEAiLF.png)
![](https://i.imgur.com/PuKZJXm.png)
![](https://i.imgur.com/qLd4dVo.png)
![](https://i.imgur.com/noecV9i.png)
![](https://i.imgur.com/hsDvGbR.png)
![](https://i.imgur.com/rVqvCU3.png)
![](https://i.imgur.com/VovUatW.png)
![](https://i.imgur.com/j6jXFFb.png)
![](https://i.imgur.com/8qmY6Fl.png)
</details>
