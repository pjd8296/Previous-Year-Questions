1. There are two players Wendy and Bob. Given a string of arrangement of white and black pieces( e.g, wwbbbwww), we have to find who wins the game given the following rules:

  a. Wendy goes first
  b. Wendy picks w and Bob picks b
  c. Wendy can pick a white piece only if it has at least one w on both sides. Same rule is for Bob.
  d. After, removing a piece, the other pieces to its left and right are now adjacent.
  e. The person who can’t make a move loses
        
Example:
input: `wwwbbbbwww` , answer: Bob wins
* first wendy picks a w from left, string is now `wwbbbbwww`
* then Bob picks a b, string is now, `wwbbbwww`
* then wendy picks a w from right, string is now `wwbbbww`
* then Bob picks a b, string is now, wwbbww, now Wendy can’t pick a piece so Bob wins.

**Solution:** For every block of consecutive w or b, count the number of w or b in that block. If the size of block>=3, number of chances for wendy or `bob += size of block-2`. If wendy has more chances, she wins, otherwise Bob wins.


2. Given an undirected unweighted graph of n nodes numbered from 1 to n and a source vertex, print all other vertex in increasing order of their distance from source. If multiple vertex have same distance, order them with their indices.

**Solution:** We need to apply a variant of Level order traversal, when you go to the next level, instead of accessing the element in the order they arrived(like in BFS), we have to first sort the next level nodes and then traverse them.


3. You are given n packets. These packets have to be sent from source to destination. Some packets are already sent given by two array of size k. `first_array[i]` to `second_array[i]` packets are already sent(The ranges are never overlapping). The remaining packets can be sent only in chunks of sizes of some powers of 2. the packets in a chunk have to be consecutive. Find minimum number of  chunks needed.

**Example:** if n=15, and (2,4), (7,8) and (14,15) are already sent, the answer will be  4. the chunks will be (1,1), (5,6), (9,12), (13,13).


**Solution:** sort the ranges that are already sent. Then find the block that is not sent. Find the number of chunks of size as some power of 2 this block has to be divided into(simply, the number of ones in the binary representation of the size of block). Do this for every unsent block and add the values for all the blocks.
