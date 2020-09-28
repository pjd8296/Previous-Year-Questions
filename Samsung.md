## Coding Round
1. An array contains both positive and negative numbers in random order.
 Rearrange the array elements so that all negative numbers appear 
 before all positive numbers.
 https://www.geeksforgeeks.org/move-negative-numbers-beginning-positive-end-constant-extra-space/
 
 ```c++
 void rearrange(int arr[], int n)
{
    int j = 0;
    for (int i = 0; i < n; i++) {
        if (arr[i] < 0) {
            if (i != j)
                swap(arr[i], arr[j]);
            j++;
        }
    }
}
```

```c++
void shiftall(int arr[], int left, 
              int right)
{
   
  // Loop to iterate over the 
  // array from left to the right
  while (left<=right)
  {
    // Condition to check if the left
    // and the right elements are 
    // negative
    if (arr[left] < 0 && arr[right] < 0)
      left+=1;
     
    // Condition to check if the left 
    // pointer element is positive and 
    // the right pointer element is negative
    else if (arr[left]>0 && arr[right]<0)
    {
      int temp=arr[left];
      arr[left]=arr[right];
      arr[right]=temp;
      left+=1;
      right-=1;
    }
     
    // Condition to check if both the 
    // elements are positive
    else if (arr[left]>0 && arr[right] >0)
      right-=1;
    else{
      left += 1;
      right -= 1;
    }
  }
}
```

2. Given a Binary Tree where each node has positive and negative values.
  Convert this to a tree where each node contains the sum of the left and right sub trees in the original tree.
  The values of leaf nodes are changed to 0.
  https://www.geeksforgeeks.org/convert-a-given-tree-to-sum-tree/

3. Given a binary tree. Find its maximum depth – minimum depth.

4. https://www.careercup.com/question?id=5677905146281984
 
 **WormHole Question**(Very important)
 ```c++
 #include <iostream>
using namespace std;
struct grid {
	int x;
	int y;
};
int main()
{
	int n;
	cin >> n;
	grid s,d;
	cin >> s.x >> s.y >> d.x >> d.y;
	grid* vertex = new grid[2 * n + 2];
	int* a = new int[n];
	for (int i = 0;i < 2*n;i+=2) {
		cin >> vertex[i].x >> vertex[i].y;
		cin >> vertex[i+1].x >> vertex[i+1].y;
		cin >> a[i / 2];
	}
	vertex[2 * n] = s;
	vertex[2 * n + 1] = d;
	int** graph = new int* [2 * n + 2];
	for (int i = 0;i < 2 * n + 2;i++) {
		graph[i] = new int[2 * n + 2];
	}
	int V = 2 * n + 2;
	for (int i = 0;i < V;i++) {
		for (int j = 0;j < V;j++) {
			graph[i][j] = abs(vertex[i].x - vertex[j].x) + abs(vertex[i].y - vertex[j].y);
		}
	}
	for (int i = 0;i < n;i++) {
		if (a[i] < graph[2*i][2*i+1]) {
			graph[2 * i][2 * i + 1] = a[i];
			graph[2 * i + 1][2 * i] = a[i];
		}
	}
	for (int i = 0;i < V;i++) {
		for (int j = 0;j < V;j++) {
			cout << graph[i][j] << " ";
		}
		cout << endl;
	}
	for (int k = 0;k < V;k++) {
		for (int i = 0;i < V;i++) {
			for (int j = 0;j < V;j++) {
				if (graph[i][j] > graph[i][k] + graph[k][j]) {
					graph[i][j] = graph[i][k] + graph[k][j];
				}
			}
		}
	}
	cout << graph[2 * n][2 * n + 1];
	return 0;
}
```

## Technical Round
1. Given an array in which all numbers except two are repeated once.
  (i.e. we have 2n+2 numbers and n numbers are occurring twice and remaining two have occurred once).
  Find those two numbers in the most efficient way.
  https://www.geeksforgeeks.org/find-two-non-repeating-elements-in-an-array-of-repeating-elements/

2. Given a value N, if we want to make change for N cents, and we have infinite supply of each of S = { S1, S2, .. , Sm} valued coins,
  how many ways can we make the change? The order of coins doesn’t matter.
  https://www.geeksforgeeks.org/coin-change-dp-7/
