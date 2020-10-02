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

## Angry Animals
`N` animals are standing in a row, in the order : `0, 1, 2, 3, … N-1`

And we are given `M` conflicts between animals as two arrays

`a [0, 1, 2, … M-1]` and `b[0, 1, 2, … M-1]`

Where `a[i]` has a conflict with `b[i]`

We have to come up with total number of interval `(x, y)` such that no animal within this is in conflict with the other.

<details>
  <summary>Solution</summary>

Consider an animal i, to get the maximum length of interval including animal i, we have to look at all animals between i and the minimum animal i has conflict with.

Suppose the least animal i has conflict with be least_animal.

So we can choose all animals `i, i+1, … (least_animal-1)` if all animals between `i` and `least_animal` have no conflicts with each other.

So maximum length of interval including `i` depends on `least_animal` and the maximum interval of animals including the animal `i+1`.

Which means recursion, which means Dynamic Programming.

```c++
public static void AngryAnimals(int N, int [] a, int [] b){ 
 
	/* The following array will contain the least animal  
	that animal i has conflict with */ 
 
	int [] conflicts = new int[N]; 
	int i = 0; 
	Arrays.fill(conflicts, N); 
	for(i = 0; i < a.length; i++){ 
		int l = Math.min(a[i], b[i]); 
		int h = Math.max(a[i], b[i]); 
		conflicts[l] = Math.min(conflicts[l], h); 
	} 
 
	/* The following array will contain at the index i the maximum length of  
	interval including the animal i, 
	Also note that the maximum interval including the animal i depends on the  
	least animal i has conflict with and also the maximum interval including  
	the animal i+1 */ 
 
	int [] aux_con = new int[N]; 
	 
	//Since N-1 animal wont have any conflicts with animal bigger than itself 
	aux_con[N-1] = N; 
	 
	int ways = 0; 
 
	for(i = N-2; i > -1; i-=1){ 
		aux_con[i] = Math.min(conflicts[i], aux_con[i+1]); 
 
		/* suppose i = 0, aux_con[i] = 3; 
			intervals are as follows : 
			[0, 1, 2] 
			[0, 1] 
			[0] 
			the number of possible intervals increases by aux_con[i] - i 
			which is the length of the interval 
		*/ 
 
		ways += aux_con[i] - i; 
	} 
 
	System.out.println("Total non-conflicting intervals are : "+ways); 
```
</details>
