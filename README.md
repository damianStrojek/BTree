# B-Tree Algorithm with Cache

The goal of this project is to implement a "B-Tree" algorithm and, additionally, measure how much can we improve that structure using some amount of cache memory.

The tree is described as in the lecture, that is: *B-Tree is self-balancing tree data structure that maintains sorted data and enables searching, sequential access, insertions and deletions in logarithmic time. Tree of order t (where t is any count) can store a minimum of t-1 elements in each node (except the root) and a maximum of 2t-1.* 

## Basic Operations

- `I x` - Create a tree of order x.

- `A x` - Add the value of x to the tree, where x is a signed integer. The values we will add are unique, will not appear e.g. A 1, A 1 unless between these commands we remove 1 from the tree.

- `? x` - Check if the given x value is in the tree. If it is, we print "x: +", w otherwise, we print "x: -".

- `P` - We list all the elements that are in the ZN tree.

- `S` - We save the tree in the correct format, which I present below: (6 s) (0) "2((12)4(5))"-this is a tree with order 2, root value 4 and elements 1, 2, 5.

- `L t` - Load the tree with the given order t. Example of a proper tree: "(((1 2) 3 (4) 5 (6 7)) 8 ((8) 10 (11)))".

- `R x` - We remove the element with value x from the tree. The given element can be in the tree, but it may also not be there. Therefore, the operation may not change the elements in the tree, but it may force it reorganization.

- `#` - Ignore this line, comment.

- `X` - End the program.

- `C x q1,q2,[...]` - Calculate the impact of the hypothetical cache memory. Suppose at the entrance we get some q1, 42, 43 (the list q ends with a newline). The program can store the result of q in a cache of size x. Hence, if the next entry q has already been visited, program we don't need to visit the B-Tree, but it can just read the data from the cache.

## Cache theory

Because the cache size is much smaller than the B-Tree size, you can store only selected entries. The policy to be implemented is FIFO (i.e. the first element that was loaded into the cache is removed from it when we load another item, a the result is added to the cache). Note that the "No found" result valid result to be cached.

A measure of cache impact is the number of disk accesses (measured as B-Tree depth). As an example, consider the tree from point L and the series q given by: `C 2 1 2 1 1 3 1`.

The measure without cache is 17. The cached measure is : 3+3+0+0+2+3 = 11