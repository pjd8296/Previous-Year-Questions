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
