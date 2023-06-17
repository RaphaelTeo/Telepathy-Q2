# QUESTION 2 (Algorithms)

## Metadata

Language: Python

Environment Setup: A virtual environment was not used as no modules were installed. Only math was used to easily get the ceiling of calculations (7/2 ~= 4), but this could have been done manually as well.


## Background and Assumptions
This Binary Search Tree (BST) is made up of nodes which branch out to 2 lower nodes, with the left one being of a lower integer value and the right one being higher.


## Submission (main)

#### Sorting the inputs to create a balanced tree
To obtain a balanced tree (as much as possible), we first analyse some examples (see handwritten notes), and figure out the best order to start inserting values.

To get this best order of values for insertion, the raw number list is first sorted by values. Then this list is put into a First In Last Out (FILO) stack for processing.

The list is popped from the stack, and its middle value is put into the output list, while the list is split into 2, about this middle value. These 2 lists are putback into the stack. This then repeats until the stack is empty.

#### Creating the tree
After implementing a function to sort the list of values (also considering duplicates and an even number of numbers), we can start creating the BST.

First, initialise the top of the tree with the first value in the ordered list.

Then, iterate through the ordered list of values, searching through the BST and inserting the value with its ID once a suitable and empty node is found. Separate functions for Search and Insert are used. 

Since each node is given an ID, duplicate values can be handled.

The function for comparing and assigning child direction is externalised, so other metrics can be used (alphabetical, complex calculations, etc).

#### Tree Structure

The BST is a dictionary or dictionaries, like so: BST = {ID: {'value':value, 'left_child_ID':left_child_ID, 'right_child_ID':right_child_ID},
                                                    ...
                                                    } 

Each node is linked to its children by IDs. 

The search function uses the current node ID (starting from the origin node) to get the dictionary key, and reads the node's value to compare it with the current value that it is holding, in order to decide between the left or right child.

After which, it reads the child ID which will be used as the current node ID in the next iteration. This loops until there are no more children in the required side (left/right), at which point it inserts this value with its new ID. The current node's child ID is updated with this new ID.


## Considerations and Issues Encountered

1. Duplicates are handled by just treating it as "lower" i.e. move to left child node.
2. At first I wanted to implement a list of "one-legged nodes", a priority FIFO list to jump to when inserting the next value. However, I realised that the BST has to be searched from the top sequentially, so parachuting a high value in a lower value branch will cause it to never be found.

#### Input arrangement
=====
1 item(s) in stack: **[[1, 2, 3, 4, 5, 6, 7]]**
Processing 7 items: [1, 2, 3, 4, 5, 6, 7]
Added 4. Split [1, 2, 3] & [5, 6, 7]. Stack size 2
Ordered list: [4]
=====
2 item(s) in stack: [[1, 2, 3], [5, 6, 7]]
Processing 3 items: [1, 2, 3]
Added 2. Split [1] & [3]. Stack size 3
Ordered list: [4, 2]
=====
3 item(s) in stack: [[5, 6, 7], [1], [3]]
Processing 3 items: [5, 6, 7]
Added 6. Split [5] & [7]. Stack size 4
Ordered list: [4, 2, 6]
=====
4 item(s) in stack: [[1], [3], [5], [7]]
Processing 1 items: [1]
Added 1. No more splitting. Stack size 3
Ordered list: [4, 2, 6, 1]
=====
3 item(s) in stack: [[3], [5], [7]]
Processing 1 items: [3]
Added 3. No more splitting. Stack size 2
Ordered list: [4, 2, 6, 1, 3]
=====
2 item(s) in stack: [[5], [7]]
Processing 1 items: [5]
Added 5. No more splitting. Stack size 1
Ordered list: [4, 2, 6, 1, 3, 5]
=====
1 item(s) in stack: [[7]]
Processing 1 items: [7]
Added 7. No more splitting. Stack size 0
Ordered list: **[4, 2, 6, 1, 3, 5, 7]**

#### Input arrangement with a duplicate
=====
**1 item(s) in stack: [[1, 2, 3, 4, 4, 5, 6, 7]]**
Processing 8 items: [1, 2, 3, 4, 4, 5, 6, 7]
Added 4. Split [1, 2, 3] & [4, 5, 6, 7]. Stack size 2
Ordered list: [4]
=====
2 item(s) in stack: [[1, 2, 3], [4, 5, 6, 7]]
Processing 3 items: [1, 2, 3]
Added 2. Split [1] & [3]. Stack size 3
Ordered list: [4, 2]
=====
3 item(s) in stack: [[4, 5, 6, 7], [1], [3]]
Processing 4 items: [4, 5, 6, 7]
Added 5. Split [4] & [6, 7]. Stack size 4
Ordered list: [4, 2, 5]
=====
4 item(s) in stack: [[1], [3], [4], [6, 7]]
Processing 1 items: [1]
Added 1. No more splitting. Stack size 3
Ordered list: [4, 2, 5, 1]
=====
3 item(s) in stack: [[3], [4], [6, 7]]
Processing 1 items: [3]
Added 3. No more splitting. Stack size 2
Ordered list: [4, 2, 5, 1, 3]
=====
2 item(s) in stack: [[4], [6, 7]]
Processing 1 items: [4]
Added 4. No more splitting. Stack size 1
Ordered list: [4, 2, 5, 1, 3, 4]
=====
1 item(s) in stack: [[6, 7]]
Processing 2 items: [6, 7]
Added 6. Split [] & [7]. Stack size 1
Ordered list: [4, 2, 5, 1, 3, 4, 6]
=====
1 item(s) in stack: [[7]]
Processing 1 items: [7]
Added 7. No more splitting. Stack size 0
Ordered list: **[4, 2, 5, 1, 3, 4, 6, 7]**