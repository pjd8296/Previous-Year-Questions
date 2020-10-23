## Favorite Genre
Visit [here](https://www.google.com/url?q=https://leetcode.com/discuss/interview-question/373006&sa=D&ust=1602672883036000&usg=AOvVaw16XOb-wL6mszWwy96jQLKX) for explanation
<details>
	<summary>Solution</summary>

```c++
    unordered_map<string,vector<string>> songsAndGenre(unordered_map<string,vector<string>>& users, unordered_map<string,vector<string>>& genres){
    unordered_map<string,string> songToGenre;
    unordered_map<string,unordered_map<string,int>> userToGenre;
    unordered_map<string,vector<string>> result;
    unordered_map<string,int> max;
    for(auto genre:genres)
    {
        for(auto song: genre.second)
        {
            songToGenre[song] = genre.first;
        }
    }
    
    for(auto user:users)
    {
        for(auto item:user.second)
        {
            userToGenre[user.first][songToGenre[item]]++;
            auto tempMax = userToGenre.at(user.first).at(songToGenre[item]);
            max[user.first] = std::max(tempMax,max[user.first]);
        }
    }
    
    for(auto user:userToGenre)
    {
        for(auto genre:user.second)
        {
            if(genre.second==max.at(user.first))
            {
                result[user.first].push_back(genre.first);
            }
        }
    }
    
    return result;
}

int main() {
    unordered_map<string,vector<string>> users;
    users["David"] = {"song1", "song2", "song3", "song4", "song8"};
    users["Emma"] = {"song5", "song6", "song7"};
    
    unordered_map<string,vector<string>> songs;
    songs["Rock"] = {"song1", "song3"};
    songs["Dubstep"] = {"song7"};
    songs["Techno"] = {"song2", "song4"};
    songs["Pop"] = {"song5", "song6"};
    songs["Jazz"] = {"song8", "song9"};

    auto result = songsAndGenre(users,songs);
    for(auto x: result)
    {
        cout<<x.first<<" : ";
        for(auto song:x.second)
        {
            cout<<song<<" ";
        }
        cout<<endl;
    }
    
    users.clear();
    songs.clear();
    
    users["David"] = {"song1", "song2"};
    users["Emma"] = {"song3", "song4"};
    
    result = songsAndGenre(users,songs);
    for(auto x: result)
    {
        cout<<x.first<<" : ";
        for(auto song:x.second)
        {
            cout<<song<<" ";
        }
        cout<<endl;
    } 
}
```
</details>

## Subtree of another tree
<details>
    <summary>Solution</summary>

```c++
class Solution {
public:
    bool inorder(TreeNode* s, TreeNode* t) {
        if(!s and !t) return true;
        if(!s or !t) return false;
        bool b1 = inorder(s->left, t->left);
        if(s->val!= t->val)
            return false;
        bool b2 = inorder(s->right, t->right);
        return b1 and b2;
    }
    bool isSubtree(TreeNode* s, TreeNode* t) {
        if(!s) return false;
        bool b1 = isSubtree(s->left, t);
        if(s->val == t->val and inorder(s, t)) return true;
        bool b2 = isSubtree(s->right, t);
        return b1 or b2;
    }
};
```
</details>

## Critical Connections
<details>
    <summary>Solution</summary>

```c++
class Solution {
public:
    vector<vector<int>> graph;
    vector<int> ranks;

    vector<vector<int>> criticalConnections(int n, vector<vector<int>>& connections) {
        graph.resize(n);
        for (auto& conn : connections) {
            graph[conn[0]].push_back(conn[1]);
            graph[conn[1]].push_back(conn[0]);
        }
        ranks.resize(n, -2);

        vector<vector<int>> res;
        dfs(0, 0, res);  
        return res;
    }

    int dfs(int node, int rank, vector<vector<int>>& res) {
        if (ranks[node] >= 0) return ranks[node];

        ranks[node] = rank;
        int minRank = rank;
        
        for (auto neighbor : graph[node]) {
            if (ranks[neighbor] == rank - 1 || ranks[neighbor] > rank) continue;
            int neighborRank = dfs(neighbor, rank + 1, res);
            minRank = min(minRank, neighborRank);
            if (neighborRank > rank) res.push_back({node, neighbor});
        }
        return minRank;
    }
};
```
</details>

## Count pairs with given sum
<details>
    <summary>Solution</summary>
    
```c++
int getPairsCount(int arr[], int n, int sum) {
    unordered_map<int, int> m; 
	int ans = 0;
  	for(int i = 0; i < n; i++) {
      if(m.count(sum - arr[i])) {
        ans += m[sum - arr[i]];
      }
      m[arr[i]]++;
    }
  	return ans;
}
```
</details>

## Clone a Linked List with random pointers
<details>
	<summary>Solution</summary>
	
```c++
/* Deep copies the linked list (along with random pointers) */
Node* Solution :: copyRandomList(Node* originalHead)
{
    // Handle the corner case
    if(!originalHead) return originalHead;
    
    // Create the head of the cloned linked list and store its reference permanently
    Node* clonedHead = new Node(originalHead->val, nullptr, nullptr);
    
    // Create iterators for both the linked lists
    Node* newHead = clonedHead;
    Node* oldHead = originalHead;
    
    // Create a map which facilitates going vertically down from the original to cloned node
    unordered_map<Node*, Node*> nodeJustBelow;
    
    /* Node to Node mapping is compulsory to deal with duplicates in the linked list */
    
    // Link the nodes vertically
    nodeJustBelow[oldHead] = newHead;
    
    // Check whether the next node exists or not
    while(oldHead->next)
    {
        // First, create the next node in the cloned list.
        newHead->next = new Node(oldHead->next->val, nullptr, nullptr);
        
        // After the node has been created, step on it by the new thread
        newHead = newHead->next;
        oldHead = oldHead->next;
        
        // After you've moved to the newly created node, connect it vertically
        nodeJustBelow[oldHead] = newHead;
    }
    
    /* The linked list has been cloned correctly (except the random pointers) */

    // Traverse both the lists together and fill the random pointers
    oldHead = originalHead;
    newHead = clonedHead;
    
    // As long as both the lists exist, correct the random pointers
    while(oldHead && newHead)
    {
        // Traverse the random pointer of the original list and go down vertically and connect it
        newHead->random = oldHead->random? nodeJustBelow[oldHead->random] : nullptr;
        
        // Move forward in both the lists
        oldHead = oldHead->next;
        newHead = newHead->next;
    }
    
    // Return the stored reference of the cloned list
    return clonedHead;
}
```
</details>

## URLify

<details>
	<summary>Solution</summary>

```c++
// Maximum length of string after modifications.
const int MAX = 1000;
 
// Replaces spaces with %20 in-place and returns
// new length of modified string. It returns -1
// if modified string cannot be stored in str[]
int replaceSpaces(char str[])
{
    // count spaces and find current length
    int space_count = 0, i;
    for (i = 0; str[i]; i++)
        if (str[i] == ' ')
            space_count++;
 
    // Remove trailing spaces
    while (str[i-1] == ' ')
    {
       space_count--;
       i--;
    }
 
    // Find new length.
    int new_length = i + space_count * 2 + 1;
 
    // New length must be smaller than length
    // of string provided.
    if (new_length > MAX)
        return -1;
 
    // Start filling character from end
    int index = new_length - 1;
 
    // Fill string termination.
    str[index--] = '\0';
 
    // Fill rest of the string from end
    for (int j=i-1; j>=0; j--)
    {
        // inserts %20 in place of space
        if (str[j] == ' ')
        {
            str[index] = '0';
            str[index - 1] = '2';
            str[index - 2] = '%';
            index = index - 3;
        }
        else
        {
            str[index] = str[j];
            index--;
        }
    }
 
    return new_length;
}
```
</details>

## Infix to Postfix
<details>
	<summary>Solution</summary>

```c++
//Function to return precedence of operators 
int prec(char c) 
{ 
    if(c == '^') 
    return 3; 
    else if(c == '*' || c == '/') 
    return 2; 
    else if(c == '+' || c == '-') 
    return 1; 
    else
    return -1; 
} 
// The main function to convert infix expression 
//to postfix expression 
void infixToPostfix(string s) 
{ 
    std::stack<char> st; 
    st.push('N'); 
    int l = s.length(); 
    string ns; 
    for(int i = 0; i < l; i++) 
    { 
        // If the scanned character is an operand, add it to output string. 
        if((s[i] >= 'a' && s[i] <= 'z')||(s[i] >= 'A' && s[i] <= 'Z')) 
        ns+=s[i]; 
  
        // If the scanned character is an ‘(‘, push it to the stack. 
        else if(s[i] == '(') 
          
        st.push('('); 
          
        // If the scanned character is an ‘)’, pop and to output string from the stack 
        // until an ‘(‘ is encountered. 
        else if(s[i] == ')') 
        { 
            while(st.top() != 'N' && st.top() != '(') 
            { 
                char c = st.top(); 
                st.pop(); 
               ns += c; 
            } 
            if(st.top() == '(') 
            { 
                char c = st.top(); 
                st.pop(); 
            } 
        } 
        //If an operator is scanned 
        else{ 
            while(st.top() != 'N' && prec(s[i]) <= prec(st.top())) 
            { 
                char c = st.top(); 
                st.pop(); 
                ns += c; 
            } 
            st.push(s[i]); 
        } 
    } 
    //Pop all the remaining elements from the stack 
    while(st.top() != 'N') 
    { 
        char c = st.top(); 
        st.pop(); 
        ns += c; 
    } 
    cout << ns << endl; 
}
```
</details>

## Evaluate Postfix

<details>
	<summary>Solution</summary>
	
```c++
int evalRPN(vector<string>& tokens) {
    stack<int> stn;
    for(auto s:tokens) {
        if(s.size()>1 || isdigit(s[0])) stn.push(stoi(s));
        else {
            auto x2=stn.top(); stn.pop();
            auto x1=stn.top(); stn.pop();
            switch(s[0]) {
                case '+': x1+=x2; break;
                case '-': x1-=x2; break;
                case '*': x1*=x2; break;
                case '/': x1/=x2; break;
            }
            stn.push(x1);
        }
    }
    return stn.top();
}
```
</details>

## Infix evaluation
Two methods:
1. Infix-to-postfix + postfix-evaluate
2. Using Two Stacks

<details>
	<summary>Explanation</summary>

In the usual arithmetic expressions the operator is written between the operands.  Such operators are called binary operators.
Such expressions are called infix expressions.  The operators + and - work as unary operators as well.
In the discussions below we consider all operators to be binary.

Assume,

1.  Permitted operands: A,B,C,D
2.  Permitted operators: +,-, *, /, ^(exponentiation)
3.  All values are float
4.  Blanks are permitted in expression
5.  Constants are not permitted in the expression
6.  Parenthesis are permitted

Given values of the operand A, B, C and D, the problem is to evaluate an expression of the form:  A+B*C-D.

Here is a simple algorithm:

We will use two stacks:

Operand stack: to keep values (numbers)  and
Operator stack: to keep operators (+, -, *, . and ^).  

In the following, “process” means, (i) pop operand stack once (value1) (ii) pop operator stack once (operator) (iii) pop operand stack again (value2) (iv) compute value1 operator  value2 (v) push the value obtained in operand stack.          

Algorithm:
```
Until the end of the expression is reached, get one character and perform only one of the steps (a) through (f):

(a) If the character is an operand, push it onto the operand stack.

(b) If the character is an operator, and the operator stack is empty then push it onto the operator stack.

(c) If the character is an operator and the operator stack is not empty, and the character's precedence is greater
    than the precedence of the stack top of operator stack,  then push the character onto the operator stack.

(d) If the character is "(", then push it onto operator stack.

(e) If the character is ")", then "process" as explained above until the corresponding "(" is encountered in operator stack.
    At this stage POP the operator stack and ignore "(."

(f) If cases (a), (b), (c), (d) and (e) do not apply, then process as explained above.
```
When there are no more input characters, keep processing until the operator stack becomes empty.
The values left in the operand stack is the final result of the expression.
```java
public class InfixEvaluation {

    public int evaluate(String expression){
        //Stack for Numbers
        Stack<Integer> numbers = new Stack<>();

        //Stack for operators
        Stack<Character> operations = new Stack<>();
        for(int i=0; i<expression.length();i++) {
            char c = expression.charAt(i);
            //check if it is number
            if(Character.isDigit(c)){
                //Entry is Digit, it could be greater than one digit number
                int num = 0;
                while (Character.isDigit(c)) {
                    num = num*10 + (c-'0');
                    i++;
                    if(i < expression.length())
                        c = expression.charAt(i);
                    else
                        break;
                }
                i--;
                //push it into stack
                numbers.push(num);
            }else if(c=='('){
                //push it to operators stack
                operations.push(c);
            }
            //Closed brace, evaluate the entire brace
            else if(c==')') {
                while(operations.peek()!='('){
                    int output = performOperation(numbers, operations);
                    //push it back to stack
                    numbers.push(output);
                }
                operations.pop();
            }
            // current character is operator
            else if(isOperator(c)){
                //1. If current operator has higher precedence than operator on top of the stack,
                //the current operator can be placed in stack
                // 2. else keep popping operator from stack and perform the operation in  numbers stack till
                //either stack is not empty or current operator has higher precedence than operator on top of the stack
                while(!operations.isEmpty() && precedence(c)<=precedence(operations.peek())){
                    int output = performOperation(numbers, operations);
                    //push it back to stack
                    numbers.push(output);
                }
                //now push the current operator to stack
                operations.push(c);
            }
        }
        //If here means entire expression has been processed,
        //Perform the remaining operations in stack to the numbers stack

        while(!operations.isEmpty()){
            int output = performOperation(numbers, operations);
            //push it back to stack
            numbers.push(output);
        }
        return numbers.pop();
    }

    static int precedence(char c){
        switch (c){
            case '+':
            case '-':
                return 1;
            case '*':
            case '/':
                return 2;
            case '^':
                return 3;
        }
        return -1;
    }

    public int performOperation(Stack<Integer> numbers, Stack<Character> operations) {
        int a = numbers.pop();
        int b = numbers.pop();
        char operation = operations.pop();
        switch (operation) {
            case '+':
                return a + b;
            case '-':
                return b - a;
            case '*':
                return a * b;
            case '/':
                if (a == 0)
                    throw new
                            UnsupportedOperationException("Cannot divide by zero");
                return b / a;
        }
        return 0;
    }

    public boolean isOperator(char c){
        return (c=='+'||c=='-'||c=='/'||c=='*'||c=='^');
    }

    public static void main(String[] args) {
        String infixExpression = "2 * (5 *(3+6))/15-2";
        InfixEvaluation i = new InfixEvaluation();
        System.out.println(i.evaluate(infixExpression));
    }
}
```

</details>

## Count Inversions

<details>
	<summary>Solution</summary>

```c++
#include <bits/stdc++.h> 
using namespace std; 

int _mergeSort(int arr[], int temp[], int left, int right); 
int merge(int arr[], int temp[], int left, int mid, int right); 

/* This function sorts the input array and returns the number of inversions in the array */
int mergeSort(int arr[], int array_size) 
{ 
	int temp[array_size]; 
	return _mergeSort(arr, temp, 0, array_size - 1); 
} 

/* An auxiliary recursive function that sorts the input array and returns the number of inversions in the array. */
int _mergeSort(int arr[], int temp[], int left, int right) 
{ 
	int mid, inv_count = 0; 
	if (right > left) { 
		/* Divide the array into two parts and call _mergeSortAndCountInv() for each of the parts */
		mid = (right + left) / 2; 

		/* Inversion count will be sum of 
		inversions in left-part, right-part 
		and number of inversions in merging */
		inv_count += _mergeSort(arr, temp, left, mid); 
		inv_count += _mergeSort(arr, temp, mid + 1, right); 

		/*Merge the two parts*/
		inv_count += merge(arr, temp, left, mid + 1, right); 
	} 
	return inv_count; 
} 

/* This funt merges two sorted arrays and returns inversion count in the arrays.*/
int merge(int arr[], int temp[], int left, int mid, int right) { 
	int i, j, k; 
	int inv_count = 0; 

	i = left; /* i is index for left subarray*/
	j = mid; /* j is index for right subarray*/
	k = left; /* k is index for resultant merged subarray*/
	while ((i <= mid - 1) && (j <= right)) { 
		if (arr[i] <= arr[j]) { 
			temp[k++] = arr[i++]; 
		} 
		else { 
			temp[k++] = arr[j++]; 

			// this is tricky
			inv_count = inv_count + (mid - i); 
		} 
	} 

	/* Copy the remaining elements of left subarray (if there are any) to temp*/
	while (i <= mid - 1) 
		temp[k++] = arr[i++]; 

	/* Copy the remaining elements of right subarray (if there are any) to temp*/
	while (j <= right) 
		temp[k++] = arr[j++]; 

	/*Copy back the merged elements to original array*/
	for (i = left; i <= right; i++) 
		arr[i] = temp[i]; 

	return inv_count; 
} 

int main() 
{ 
	int arr[] = { 1, 20, 6, 4, 5 }; 
	int n = sizeof(arr) / sizeof(arr[0]); 
	int ans = mergeSort(arr, n); 
	cout << " Number of inversions are " << ans; 
	return 0; 
} 
```
</details>
