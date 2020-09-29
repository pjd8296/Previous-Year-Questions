1.
Given 2 strings, s1 and s2. Find a string s which is a concatenation of subsequence of s1 and subsequence of s2 and is longest possible palindrome and return its length.
```
Eg. s1 = ban, s2=ana. So answer is 5 ( ‘anana’).
Eg. s1 = abc, s2=abc.  So answer is 3 (‘aba’)
```
**Soln** :- Concat s1 and s2. Let s=s1+s2. t=reverse of s. Apply LCS on s and t, which is the answer. All test cases passed.
