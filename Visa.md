1. Activity selection problem (start time and duration given. At any time only one activity can be done. Select the most number of activities.)

2. You are given two strings s and t. |s|>=|t|  You need to determine whether t can be concatenated multiple times to obtain s. Also if this is possible to do then you need to output the smallest string x such that both s and t can be obtained from x by some number of concatenations. (*Hint: Use KMP*)

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
