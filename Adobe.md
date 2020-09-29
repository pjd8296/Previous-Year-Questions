1. Given 2 strings, s1 and s2. Find a string s which is a concatenation of subsequence of s1 and subsequence of s2 and is longest possible palindrome and return its length.
```
Eg. s1 = ban, s2=ana. So answer is 5 ( ‘anana’).
Eg. s1 = abc, s2=abc.  So answer is 3 (‘aba’)
```
**Soln** :- Concat s1 and s2. Let s=s1+s2. t=reverse of s. Apply LCS on s and t, which is the answer. All test cases passed.
2. (Need to solve) Given a string s. Return substring of length 5 which occurs maximum times. If several of them exists, then you know what to do.
```
  Yes, return the lexicographically smallest one. 5<=N<=10^6.
  Eg. s= “bbbbbaaaaabbabababa. So answer is “ababa”.
  Eg. s=”heisagoodboy” So answer is “agood”.
```
3. ![](https://lh3.googleusercontent.com/SHXRtAcqOIAyhjnvJHfWFCFb4DpTVviSOzUNmVOU4fZoTpn04Ppzo5A1YQ1qr-GCkeBKfKI8M2MNzGTzusNmMmi7nHycJfJwXHKz7JnTOcqrfaqHd0C0IQH7s2y-0JfVRSc1n43L)
