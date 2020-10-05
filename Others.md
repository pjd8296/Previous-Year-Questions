# Dream 11

1. **Paths to a Goal**
Given a string made of characters ‘l’ and ‘r’ you need to find out the no. of distinct subsequences of that string which will lead you to position ‘y’ from position ‘x’ on the number line of ‘n’ length, if ‘l’ moves you back and ‘r’ moves you front.
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
* Other quant questions on Bayes Theorem and JEE level probability and P&C. eg. 6 black chairs and 4 red chairs, three customers bought a chair. Probability that there were two or more than 2 black chairs out of them. 4 rotten apples and 11 normal apples in a bag. We take out them one by one without replacement, probability that 9th apple is the last rotten apple.
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
