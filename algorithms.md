Algorithms Exam TODO and Revision:
==================================


# To Do List

* Learn Tower of Hanoi and apply for n=5. State the algorithm in plain english. Prove there's no shorter algorithm. Find out how long it'd take for n=60.
* Practice horizontal scroll word document.
* Prove that, for any sorting algorithm applied to a list of length n, the worst case complexity is
proportional to nlog2n.
* Show worse case complexity for recursive algorithm in 5 (a).
* State conditions for valid recursive function definition. State why recursive function for weighted graph is valid and what it does. Evaluate the function for given letters.
* State why the function definition is valid for 4 (d) and what it does. Evaluate it a few times. Change it and say what would happen.

# Revision

## Tower of Hanoi formal algorithm in English:

__The Tower of Hanoi recursive function is valid because it contains the stopping condition of n=1, and each self-reference reduces n by 1 so the stopping condition will be reached after a finite number of steps.

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

## List Keywords and common representations

* [] - Empty list
* : - Compound operator, joins two things together eg. [1,2]:[3] -> [1,2,3] and [1,2,3]:4 -> [1,2,3,4]
* hd - Returns the first item in a list eg. hd[1,2,3] -> 1
* lst - Returns the last item in a list eg. tl[1,2,3] -> 3
* tl - Takes a list and returns it without it's first item eg. lst[1,2,3] -> [2,3]
* init - Takes a list and returns it without it's last item eg. lst[1,2,3] -> [1,2]
* # - Returns the length of a list eg. #[1,2,3] -> 3

Lists are denoted using uppercase and elements lowercase.

Other common representations include:
* MG - Merge Sort
* S - Sort
* GCD - Greatest common denominator


## Valid Recursive Function Definition

A recursive function is one which contains a self-reference. A valid recursive function must have a non-self referencing stopping condition and must reach this stopping condition after a finite number of steps.


## Graph Traversing Algorithm

This function definition is valid because there is a stopping condition and each self reference reduces the number of nodes in the graph by 1, so it will be reached in a finite number of steps.

The algorithm checks is there is a path between x and y in the graph G.

Plain English Representation:

The algorithm progresses by removing each node it comes in contact with from the graph and then continues with the children. The easiest way to keep track of path is with numbers for which path you are on eg. 111,112,1121.

Basically, start from the origin, get the children and use them to continue. If there's no child that hasn't already been visited stop because false. If the child ends up being the goal return true and backtrack to demonstrate this.
