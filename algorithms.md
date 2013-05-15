Algorithms Exam TODO and Revision:
==================================

# To Do List

* Learn Tower of Hanoi and apply for n=5. State the algorithm in plain english. Prove there's no shorter algorithm. Find out how long it'd take for n=60.
* State and prove Warshall's algorithm for establishing the reachability matrix R of a boolean adjacency matrix M and apply it to matrix
*  State and prove Dijkstra's algorithm for finding the shortest path between two nodes in a positively weighted digraph.Is the assumption of positive weighting necessary and if so why? Apply it to the following graph to find the shortest distance and route from node f to node c.
*  Prove that, for any sorting algorithm applied to a list of length n, the worst case complexity is
proportional to nlog2n.
* Show worse case complexity for recursive algorithm in 5 (a).
* State conditions for valid recursive function definition. State why recursive function for weighted graph is valid and what it does. Evaluate the function for given letters.
* State why the function definition is valid for 4 (d) and what it does. Evaluate it a few times. Change it and say what would happen.

# Revision

## Tower of Hanoi formal algorithm in English:

Remember that in his example the letters used for the piles and the letter he uses to represent the stack positions are the same. This confused me for ages so I'm gonna use a, b and c for the piles and x, y and z for the peg position. When you do it out you should use x,y,z for the piles, but for explaining the algorithm it's easier to use a,b,c for now!

__Formal algorithm for Tn:__

n > 1: Tn-1(Swap middle y and last z)T(first x,second y)Tn-1(Swap first x and last z)
n = 1: T(first x,middle y)

So if we solve n = 4 using T4(a,b,c)

we get:

```
T4(a,b,c) = T3(a,c,b)T(a,b)T3(c,b,a)
```

for subsequent steps, remember that you'll be replacing any Tn-1 bits with three bits on the next line until n=1.

So next line is:

```
T2(a,b,c)T(a,c)T2(b,c,a)T(a,b)T2(c,a,b)T(c,b)T2(a,b,c)

T1(a,c,b)T(a,b)T1(c,b,a)T(a,c)T1(b,a,c)T(b,c)T1(a,c,b)T(a,b)T1(c,b,a)T(c,a)T1(b,a,c)T(c,b)T1(a,c,b)T(a,b)T1(c,b,a)
```

For final step, just take first x and second y for each T1!
```
(a,c),(a,b),(c,b),(a,c),(b,a),(b,c),(a,c),(a,b),(c,b),(c,a),(b,a),(c,b),(a,c),(a,b),(c,b)
```
If you're worried you missed a step, the total final moves is always 2 to the power of n minus 1, so 2 x 2 x 2 - 1 = 15 total moves.