Download Link : https://programming.engineering/product/project-two-recursion/

# Project-Two-Recursion
Project Two: Recursion
Motivation

This project will give you experience in writing recursive functions that operate on recursively‐ defined data structures and mathematical abstractions.

Lists

A “list” is a sequence of zero or more numbers in no particular order. A list is well-formed if:

    It is the empty list, or

    It is an integer followed by a well‐formed list.

A list is an example of a linear‐recursive structure: it is “recursive” because the definition refers to itself. It is “linear” because there is only one such reference.

Here are some examples of well‐formed lists:

( 1 2 3 4 ) // a list of four elements ( 1 2 4 ) // a list of three elements

( ) // a list of zero element‐‐the empty list

The file recursive.h in the Project-2-Related-Files.zip defines the type list_t and the following operations on lists:

bool list_isEmpty(list_t list);

// EFFECTS: returns true if “list” is empty, false otherwise

list_t list_make();

// EFFECTS: returns an empty list

list_t list_make(int elt, list_t list);

    EFFECTS: given “list”, makes a new list consisting of

    the new element followed by the elements of the

    original list

int list_first(list_t list);

    REQUIRES: “list” is not empty

    EFFECTS: returns the first element of list

list_t list_rest(list_t list);

    REQUIRES: “list” is not empty

    EFFECTS: returns the list containing all but the first

    element of list

void list_print(list_t list);

    MODIFIES: cout

    EFFECTS: prints “list” to cout

Note: list_first and list_rest are both partial functions; their EFFECTS clauses are only valid for nonempty lists. To help you write your code, these functions actually check whether the list is empty or not‐‐if they are passed an empty list, they fail gracefully by warning you and exiting; if you are running your program under the debugger, it will stop at the exit point. Note that such checking is not required! It would be perfectly acceptable to write these in such a way that they fail quite ungracefully if passed empty lists. Note also that list_make is an overloaded function. If called with no arguments, it produces an empty list. If called with an element and a list, it combines them.

Given this list_t interface, you will write the following list processing procedures. Each of these procedures must be recursive. For full credit, your routines must provide the correct result and provide an implementation that is recursive. In writing these functions, you may use only recursion and selection. You are NOT allowed to use goto, for, while, do‐while, global variables, pointers (except function pointers), and references (including constant references).

Hint: in implementing some functions recursively, you may need to define some support functions (such as the recursive helper functions). If you define any functions yourself, be sure to declare them “static“, so that they are not visible outside this file. This will prevent any name conflicts in case you give a function the same name as one in the test cases. (For further information on “static” functions, please read some online tutorials/references. In the past, some students got a zero score simply because they forgot to declare their support functions as static functions. Be aware of this!)

Below is an example where we implement the factorial function with a recursive helper function.

Note that the function factorial_helper is defined as a static function.

static int factorial_helper(int n, int result)

    REQUIRES: n >= 0

    EFFECTS: computes result * n!

{

if (!n) {

return result;

}

else {

return factorial_helper(n-1, n*result);

}

}

int factorial(int n)

    REQUIRES: n >= 0

    EFFECTS: computes n!

{

factorial_helper(n, 1);

}

Below are the functions you are to implement. There are a number of them, but many of them are similar to one another, and the longest is at most tens of lines of code, including support functions.

int size(list_t list);

    EFFECTS: Returns the number of elements in “list”.

    Returns zero if “list” is empty.

bool memberOf(list_t list, int val);

    EFFECTS: Returns true if the value “val” appears in “list”.

    Returns false otherwise.

int dot(list_t v1, list_t v2);

    REQUIRES: Both “v1” and “v2” are non-empty

    EFFECTS: Treats both lists as vectors. Returns the dot

    product of the two vectors. If one list is longer

    than the other, ignore the longer part of the vector.

bool isIncreasing(list_t v);

    EFFECTS: Checks if the list of integers is increasing.

    A list is increasing if and only if no element

    is smaller than its previous element. By default,

    an empty list and a list of a single element are

    increasing.

//

// For example: (), (2), (1, 1), and (1, 2, 3, 3, 5) are

    all increasing. (2, 1) and (1, 2, 3, 2, 5) are not.

list_t reverse(list_t list);

    EFFECTS: Returns the reverse of “list”.

    For example: the reverse of ( 3 2 1 ) is ( 1 2 3 ).

list_t append(list_t first, list_t second);

    EFFECTS: Returns the list (first second).

    For example: append(( 2 4 6 ), ( 1 3 )) gives

    the list ( 2 4 6 1 3 ).

bool isArithmeticSequence(list_t v);

    EFFECTS: Checks if the list of integers forms an

    arithmetic sequence. By default, an empty list and

    a list of a single element are arithmetic sequences.

    For example: (), (1), (1, 3, 5, 7), and (2, 8, 14, 20)

    are arithmetic sequences. (1, 2, 4), (1, 3, 3),

    and (2, 4, 8, 10) are not.

list_t filter_odd(list_t list);

    EFFECTS: Returns a new list containing only the elements of the

    original “list” which are odd in value,

    in the order in which they appeared in list.

//

    For example, if you apply filter_odd to the list

    ( 3 4 1 5 6 ), you would get the list ( 3 1 5 ).

list_t filter(list_t list, bool (*fn)(int));

    EFFECTS: Returns a list containing precisely the elements of “list”

    for which the predicate fn() evaluates to true, in the

    order in which they appeared in list.

//

    For example, if predicate bool odd(int a) returns true

    if a is odd, then the function filter(list, odd) has

    the same behavior as the function filter_odd(list).

list_t unique(list_t list);

// EFFECTS: Returns a new list comprising of each unique element

    in “list”. The order is determined by the first

    occurrence of each unique element in “list”.

//

    For example, if you apply unique to the list

    (1 1 2 1 3 5 5 3 4 5 4), you would get (1 2 3 5 4).

    If you apply unique to the list (0 1 2 3), you would

    get (0 1 2 3)

list_t insert_list(list_t first, list_t second, unsigned int n);

    REQUIRES: n <= the number of elements in “first”.

    EFFECTS: Returns a list comprising the first n elements of

    “first”, followed by all elements of “second”,

    followed by any remaining elements of “first”.

    For example: insert(( 1 2 3 ), ( 4 5 6 ), 2)

    gives ( 1 2 4 5 6 3 ).

list_t chop(list_t list, unsigned int n);

    REQUIRES: “list” has at least n elements.

    EFFECTS: Returns the list equal to “list” without its last n

    elements.

Binary Trees

A binary tree is another fundamental data structure we will use in this project. A binary tree is well-formed if:

    It is the empty tree, or

    It consists of an integer element (called the root element), plus two children, called the left subtree and the right subtree, each of which is a well‐formed binary tree.

Additionally, we say a binary tree is a “leaf” if and only if both of its children are the EMPTY TREE.

The file recursive.h in Project-2-Related-Files.zip defines the type tree_t and the following operations on trees:

// EFFECTS: returns true if “tree” is empty, false otherwise

tree_t tree_make();

// EFFECTS: creates an empty tree

tree_t tree_make(int elt, tree_t left, tree_t right);

    EFFECTS: creates a new tree, with “elt” as its root element,

    “left” as its left subtree, and “right” as its right subtree

int tree_elt(tree_t tree);

    REQUIRES: “tree” is not empty

    EFFECTS: returns the element at the top of “tree”

tree_t tree_left(tree_t tree);

    REQUIRES: “tree” is not empty

    EFFECTS: returns the left subtree of “tree”

tree_t tree_right(tree_t tree);

    REQUIRES: “tree” is not empty

    EFFECTS: returns the right subtree of “tree”

void tree_print(tree_t tree);

    MODIFIES: cout

    EFFECTS: prints “tree” to cout.

    Note: this uses a non-intuitive, but easy-to-print format

There are several functions you are to write for binary trees. These must be recursive, and cannot use any looping structures. Once again, if you need to define any support functions, be sure to define them as static functions.

int tree_sum(tree_t tree);

    EFFECTS: Returns the sum of all elements in “tree”.

    Returns zero if “tree” is empty.

bool tree_search(tree_t tree, int val);

    EFFECTS: Returns true if the value “val” appears in “tree”.

    Returns false otherwise.

int depth(tree_t tree);

// EFFECTS: Returns the depth of “tree”, which equals the number of

    layers of nodes in the tree.

    Returns zero if “tree” is empty.

    For example, the tree

//
		

4

//
	

/
	

\

//
	

/
	

\

//
	

2
	

5

//
	

/ \
	

/ \

//
	

3
	

8

//
	

/ \
	

/ \

//
	

6
	

7

//
	

/\/\

//
		

    has depth 4.

    The element 4 is on the first layer.

    The elements 2 and 5 are on the second layer.

    The elements 3 and 8 are on the third layer.

    The elements 6 and 7 are on the fourth layer.

int tree_max(tree_t tree);

    REQUIRES: “tree” is non-empty.

    EFFECTS: Returns the largest element in “tree”.

list_t traversal(tree_t tree);

    EFFECTS: Returns the elements of “tree” in a list using an

    in-order traversal. An in-order traversal prints

    the “left most” element first, then the second-left-most,

    and so on, until the right-most element is printed.

//

    For any node, all the elements of its left subtree

    are considered as on the left of that node and

    all the elements of its right subtree are considered as

    on the right of that node.

//

    For example, the tree:

//
		

4

//
	

/
	

\

//
	

/
	

\

//
	

2
	

5

//
	

/ \
	

/ \

//
	

3
	

//
	

/ \
	

//
		

    would return the list

    (2345)

//

    An empty tree would print as:

    ( )

bool tree_hasMonotonicPath(tree_t tree);

    EFFECTS: Returns true if and only if “tree” has at least one

    root-to-leaf path such that all the elements along the

    path form a monotonically increasing or decreasing

    sequence.

//

    A root-to-leaf path is a sequence of elements in a tree

    starting with the root element and proceeding downward

    to a leaf (an element with no children).

//

    An empty tree has no root-to-leaf path.

    A monotonically increasing (decreasing) sequence is a

    sequence of numbers where no number is smaller (larger)

    than its previous number.

//

    For example, the tree:

//
		

4
	

//
		

/
	

\

//
	

/
		

//
	

8
		

//
	

/ \
		

//
	

3
	

16
	

//
	

/ \
	

/ \
	

//
			

    has two root-to-leaf paths: 4->8->3 and 4->8->16.

    Since the numbers on the path 4->8->16 form a monotonically

    increasing sequence, the function should return true.

    If we change 8 into 20, there is no such a path.

    Thus, the function should return false.

bool tree_allPathSumGreater(tree_t tree, int sum);

    REQUIRES: tree is not empty

    EFFECTS: Returns true if and only if for each root-to-leaf

    path of “tree”, the sum of all elements along the path

    is greater than “sum”.

//

    A root-to-leaf path is a sequence of elements in a tree

    starting with the root element and proceeding downward

    to a leaf (an element with no children).

//

    For example, the tree:

//
			

4

//
		

/
	

\

//
		

/
	

\

//
		

1
	

5

//
		

/ \
	

/ \

//
	

3
	

6
	

//
	

/\/\
	

//
			

    has three root-to-leaf paths: 4->1->3, 4->1->6 and 4->5.

    Given sum = 9, the path 4->5 has the sum 9, so the function

    should return false. If sum = 7, since all paths have the sums

// greater than 7, the function should return true.

We can define a special relation between trees “is covered by” as follows:

    An empty tree is covered by all trees.

    The empty tree covers only other empty trees.

    For any two non‐empty trees, A and B, A is covered by B if and only if the root elements of A and B are equal, the left subtree of A is covered by the left subtree of B, and the right subtree of A is covered by the right subtree of B.

For example, the tree:

4

        \

    \

2 5

/\ /\

3

/ \

covers the tree:

4

/ \

/

2

/ \

but not the trees:

4 5

/ / \

/ or

3

/ \

In light of this definition, write the following function:

bool covered_by(tree_t A, tree_t B);

// EFFECTS: Returns true if tree A is covered by tree B.

With the definition of “covered by”, we can define a relation “contained by”. A tree A is contained by a tree B if

    A is covered by B, or,

    A is covered by a subtree of B.

Note that in the above definition, a subtree of a tree T is an empty tree or a non-empty tree composed of a node S in T together with all downstream nodes of the node S in T (called the descendants of S in T).

For example, for the tree T

4

        \

    \

2 5

Based on the definition of “contained by”, the trees

4 5

/\ /\

/ and

2

/ \

are contained by the tree

4

        \

    \

2 5

/\ /\

3

/ \

but this tree is not:

4

/

/

3

/ \

Please write a function implementing the relation “contained by”:

bool contained_by(tree_t A, tree_t B);

    EFFECTS: Returns true if tree A is covered by tree B

    or a subtree of B.

There exists a special kind of binary tree, called the sorted binary tree. A sorted binary tree is well-formed if:

    It is a well-formed binary tree and

    One of the following is true:

        The tree is empty.

        The left subtree is a sorted binary tree, and any element in the left subtree is strictly less than the root element of the tree. The right subtree is a sorted binary tree, and any element in the right subtree is greater than or equal to the root element of the tree.

For example, the following trees are all well-formed sorted binary trees:

        		

        4
        		

        1
        	

        /
        	

        \
        		

        / \
        	

        /
        		

        \
        	

        1
        	

        2
        		

        6
        	

        / \
        	

        / \
        		

        / \
        	

        2

        1
        	

        3
        	

        5
        	

        7
        	

        / \

/\/\/\/\

while the following trees are not:

1 1 4

    / \
    		

    / \
    	

    / \
    	

    1
    	

    2
    	

    3
    	

    3
    	

    6

    / \
    			

    / \
    	

    \
    		

    2
    	

    1
    	

    7

You are to write the following function for creating sorted binary trees:

tree_t insert_tree(int elt, tree_t tree);

    REQUIRES: “tree” is a sorted binary tree.

    EFFECTS: Returns a new tree with elt inserted at a leaf such that

    the resulting tree is also a sorted binary tree.

//

    For example, inserting 1 into the tree:

//
		

4

//
	

/
	

\

//
	

/
	

\

//
	

2
	

5

//
	

/ \
	

/ \

//
	

3
	

//
	

/ \
	

//
		

// would yield
		

//
			

4

//
		

/
	

\

//
		

/
	

\

//
		

2
	

5

//
		

/ \
	

/ \

//
	

1
	

3
	

//
	

/\/\
	

//
			

    Hint: There is only one unique position for any element to be

    inserted.

Files

There are several files located in the Project-2-Related-Files.zip on Canvas:

{

return false;

}

else if(list_first(l1) != list_first(l2))

{

return false;

}

else

{

return list_equal(list_rest(l1), list_rest(l2));

}

}

bool tree_equal(tree_t t1, tree_t t2)

// EFFECTS: returns true iff t1 == t2

{

if(tree_isEmpty(t1) && tree_isEmpty(t2))

{

return true;

}

else if(tree_isEmpty(t1) || tree_isEmpty(t2))

{

return false;

}

else

{

return ((tree_elt(t1) == tree_elt(t2))

    tree_equal(tree_left(t1), tree_left(t2))

    tree_equal(tree_right(t1), tree_right(t2)));

}

}

To test your code, you should create a family of test case programs that exercise the functions we ask you to write. Here is a simple illustration to get you started:

#include <iostream>

#include “recursive.h”

#include “p2.h”

using namespace std;

static bool list_equal(list_t l1, list_t l2)

// EFFECTS: returns true iff l1 == l2.

{

if(list_isEmpty(l1) && list_isEmpty(l2))

{

return true

}

else if(list_isEmpty(l1) || list_isEmpty(l2))

{

return false;

}

else if(list_first(l1) != list_first(l2))

{

return false;

}

else

{

return list_equal(list_rest(l1), list_rest(l2));

}

}

int main()

{

int i;

list_t listA, listA_answer;

list_t listB, listB_answer;

listA = list_make();

listB = list_make();

listA_answer = list_make();

listB_answer = list_make();

for(i = 5; i>0; i–)

{

listA = list_make(i, listA);

listA_answer = list_make(6-i, listA_answer);

listB = list_make(i+10, listB);

listB_answer = list_make(i+10, listB_answer);

}

for(i = 5; i>0; i–)

{

listB_answer = list_make(i, listB_answer);

}

listB = append(listA, listB);

listA = reverse(listA);

if(!list_equal(listA, listA_answer))

return -1;

if(!list_equal(listB, listB_answer))

return -1;

return 0;

}

Note that in the above test program, the return value will be -1 if there is any error in the function reverse and append. If the return value is 0, then you pass the above test case.

Suppose the above test code is written in the file test.cpp. Compile test.cpp with recursive.cpp and your p2.cpp using the following Linux command:

g++ -Wall -o test test.cpp recursive.cpp p2.cpp

To check the return value, you should first run the program in Linux by typing

./test

Then you can check the return value by typing

echo $?

If the return value is -1, it indicates an error.

You may also find it helpful to add error messages to your output or print out the list or tree using the functions list_print and tree_print. You can find two more test examples simple_test.cpp and treeins_test.cpp in the Project-2-Related-Files.zip.

Submitting and Due Date

You only need to submit your source code file p2.cpp (name it exactly like this!). The source code file should be submitted via the online judgment system. See TAs’ announcement for additional details.

Grading

Your program will be graded along three criteria:

    Functional Correctness

    Implementation Constraints

    General Style

An example of Functional Correctness is whether or not your reverse function reverses a list properly in all cases. An example of an Implementation Constraint is whether reverse() is recursive. General Style speaks to the cleanliness and readability of your code.
Solution
