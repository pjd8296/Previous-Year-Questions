# Dream 11

1. **Paths to a Goal**
Given a string made of characters ‘l’ and ‘r’ you need to find out the no. of distinct subsequences of that string
which will lead you to position ‘y’ from position ‘x’ on the number line of ‘n’ length, if ‘l’ moves you back and ‘r’ moves you front.
(Refer SAP Labs for this question)
2. **Fun with Vowels**
Given a string consisting of only vowels, find the longest subsequence in the given string such that it consists of all five vowels in the alphabetical order.
eg - `aeiaaioooaauuaeiu`, o/p: 10
(Solution - [Fun with Vowels Geeksforgeeks](https://www.geeksforgeeks.org/longest-ordered-subsequence-of-vowels/))
```c++
int countSequencialVowels(char str[]){
	int A=0, E=0, I=0, O=0, U=0;
	int i=0;
	int length=strlen(str);
	//to scrap out leading non vowels or vowels other than 'a'
	for(i=0;i<length;i++){
		if(str[i]=='a')
			break;
	}
	while(i<length){
		if(str[i]=='a'){
			A++;
			}
		else if(str[i]=='e'){
			E = (max(A,E)) + 1; //maximum length of the sequence with E after A
			}
		else if(str[i]=='i'){
			I = (max(E,I)) + 1; //maximum length of the sequence with I after E
			}
		else if(str[i]=='o'){
			O = (max(I,O)) + 1; ////maximum length of the sequence with O after I
			}
		else if(str[i]=='u'){
			U = (max(O,U)) + 1; ////maximum length of the sequence with U after O
			}
		i++;
	}
	return U;
}
```
# Veritas
1 hour, 20 MCQ, 2 coding
Coding:
https://www.geeksforgeeks.org/smallest-window-contains-characters-string/

https://www.programcreek.com/2014/05/leetcode-paint-house-java/

# Honda Japan
3 coding questions.

* Traversal of BST,
* finding the 4th digit in binary representation of the given number,
* printing things when a number is a multiple of 3 or 5 or both.

MCQs based on regression, ML, easy probability.

* Read sampling and confidence intervals and regression as some questions were asked from it. Also questions based on z-table were asked.
* A question on central limit theorem, one on finding pdf of exp(aY+b) if Y is normally distributed.
* Other quant questions on Bayes Theorem and JEE level probability and P&C.
  eg. 6 black chairs and 4 red chairs, three customers bought a chair. Probability that there were two or more than 2 black chairs out of them.
      4 rotten apples and 11 normal apples in a bag. We take out them one by one without replacement, probability that 9th apple is the last rotten apple.
* Read about Variance, Bias, Cross Validation and Type 1 &2 errors.
* What happens to Confidence Intervals when Outliers are introduced? It increases.
* Which of the following are sensitive to Outliers. Options were 1)mean 2)median 3) mode 4) sd
range(1000-9999), find numbers divisible by 11W that are not palindromes. Ans 729

# Fractal
1. **Consecutive Numbers Sum**
[Click Here](https://www.google.com/url?q=https://leetcode.com/problems/consecutive-numbers-sum/&sa=D&ust=1601697540103000&usg=AOvVaw3HOkA-DoU0m4tTjVvw50YE)
2. **Equilibrium Index**
Equilibrium index of an array is an index such that the sum of elements at lower indexes is equal to the sum of elements at higher indexes
```c++
int equilibrium(int arr[], int n)  
{  
    int sum = 0; // initialize sum of whole array  
    int leftsum = 0; // initialize leftsum  
  
    /* Find sum of the whole array */
    for (int i = 0; i < n; ++i)  
        sum += arr[i];  
  
    for (int i = 0; i < n; ++i)  
    {  
        sum -= arr[i]; // sum is now right sum for index i  
  
        if (leftsum == sum)  
            return i;  
  
        leftsum += arr[i];  
    }  
  
    /* If no equilibrium index found, then return 0 */
    return -1;  
}  
```
# Salesforce
1. Given two string find if 1st string is present as a subsequence in the second string.
	Eg:   1st string: `butl`, 2nd string: `beautiful`. Print ‘`true`’.
  			1st string: `btel`, 2nd string: `beautiful`. print ‘`false`’.
      
**Solution**
```c++
class Solution {
public:
    bool isSubsequence(string s, string t) {
        int j = 0;
        for(int i = 0; i < t.length() and j < s.length(); i++) {
            if(t[i] == s[j]) 
                j++;
        }
        if(j == s.length()) return true;
        return false;
    }
};
```
2. Given a string `S` and a pattern `k`, you need to find the shortest length substring of `S` which contains all the character of pattern.
And also the string is cyclic in which you can come back to the starting position when you have reached the end in cycling order.

Eg.-
1) s=abgeasd, k=eag; return gea
2) s=jainummsm, k=jam; return mja

**Solution:** You just need to find the pattern `k` in `s+s`(write `s` two times as repetition allowed for cyclic case).
O(n) solution required using sliding windows algorithm.

# Lynk Logistics
1. Minimum Cost Path with Left, Right, Bottom and Up moves allowed

```c++
#include <bits/stdc++.h> 
using namespace std; 

#define ROW 5 
#define COL 5 

// structure for information of each cell 
struct cell 
{ 
	int x, y; 
	int distance; 
	cell(int x, int y, int distance) : 
		x(x), y(y), distance(distance) {} 
}; 

// Utility method for comparing two cells 
bool operator<(const cell& a, const cell& b) 
{ 
	if (a.distance == b.distance) 
	{ 
		if (a.x != b.x) 
			return (a.x < b.x); 
		else
			return (a.y < b.y); 
	} 
	return (a.distance < b.distance); 
} 

// Utility method to check whether a point is 
// inside the grid or not 
bool isInsideGrid(int i, int j) 
{ 
	return (i >= 0 && i < COL && j >= 0 && j < ROW); 
} 

// Method returns minimum cost to reach bottom 
// right from top left 
int shortest(int grid[ROW][COL], int row, int col) 
{ 
	int dis[row][col]; 

	// initializing distance array by INT_MAX 
	for (int i = 0; i < row; i++) 
		for (int j = 0; j < col; j++) 
			dis[i][j] = INT_MAX; 

	// direction arrays for simplification of getting neighbour 
	int dx[] = {-1, 0, 1, 0}; 
	int dy[] = {0, 1, 0, -1}; 

	set<cell> st; 

	// insert (0, 0) cell with 0 distance 
	st.insert(cell(0, 0, 0)); 

	// initialize distance of (0, 0) with its grid value 
	dis[0][0] = grid[0][0]; 

	// loop for standard dijkstra's algorithm 
	while (!st.empty()) 
	{ 
		// get the cell with minimum distance and delete it from the set 
		cell k = *st.begin(); 
		st.erase(st.begin()); 

		// looping through all neighbours 
		for (int i = 0; i < 4; i++) 
		{ 
			int x = k.x + dx[i]; 
			int y = k.y + dy[i]; 

			// if not inside boundary, ignore them 
			if (!isInsideGrid(x, y)) 
				continue; 

			// If distance from current cell is smaller, then 
			// update distance of neighbour cell 
			if (dis[x][y] > dis[k.x][k.y] + grid[x][y]) 
			{ 
				// If cell is already there in set, then remove its previous entry 
				if (dis[x][y] != INT_MAX) 
					st.erase(st.find(cell(x, y, dis[x][y]))); 

				// update the distance and insert new updated cell in set 
				dis[x][y] = dis[k.x][k.y] + grid[x][y]; 
				st.insert(cell(x, y, dis[x][y])); 
			} 
		} 
	} 

	// uncomment below code to print distance 
	// of each cell from (0, 0) 
	/* 
	for (int i = 0; i < row; i++, cout << endl) 
		for (int j = 0; j < col; j++) 
			cout << dis[i][j] << " "; 
	*/
	// dis[row - 1][col - 1] will represent final 
	// distance of bottom right cell from top left cell 
	return dis[row - 1][col - 1]; 
} 

int main() 
{ 
	int grid[ROW][COL] = 
	{ 
		31, 100, 65, 12, 18, 
		10, 13, 47, 157, 6, 
		100, 113, 174, 11, 33, 
		88, 124, 41, 20, 140, 
		99, 32, 111, 41, 20 
	}; 
	cout << shortest(grid, ROW, COL) << endl; 
	return 0; 
} 
```
