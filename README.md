# QUESTION 2 (Algorithms)

## Metadata

Language: Python

Environment Setup: A virtual environment was not used as no modules were installed. Only math was imported to easily get the ceiling of calculations (7/2 ≈ 4), but this could have been done manually as well.


## Background and Assumptions

This Binary Search Tree (BST) is made up of nodes which each branch out to 2 lower nodes, with the left one having a smaller integer value and the right one larger.


## Submission (main)

#### 1. Sorting the inputs to create a balanced tree

If the BST is created by picking random numbers for each node, it will be unbalanced and inefficient. To obtain a balanced tree (as much as possible), we first analyse some examples (see "Idea sketches.jpg"), and figure out the best order to start inserting values.

To get this best order of values for insertion, the raw number list is first sorted by values. Then this list is put into a First In Last Out (FILO) stack for processing.

The list is popped from the stack, and its middle value is put into the output list, while the list is split into 2, about this middle value. These 2 lists are put back into the stack. This then repeats until the stack is empty.


#### 2. BST Structure

After implementing a function to sort the list of values (also considering duplicates and an even number of integers), we can start creating the BST.

The BST is a dictionary or dictionaries, and each node is linked to its children by IDs like so: 
BST = {ID: {'value':value, 'left_child_ID': left_child_ID, 'right_child_ID': right_child_ID},
                                                    ...
                                                    } 

#### 3. Creating the BST

First, initialise the top of the tree with the first value in the ordered list.

Then, iterate through the ordered list of values, searching through the BST and inserting the value with its ID once a suitable and empty node is found. Separate functions for Search and Insert are used.

*In hindsight, the value and ID could have been inserted immediately before finding a home to adopt it, for flow simplicity.*


#### 4. Search Function

The search function uses the current parent node ID (starting from the origin node) and reads its value to compare it with this new value, in order to decide between the left or right child. After which, it reads the child's ID which will be used as the parent node ID in the next iteration. This keeps iterating until there is an empty child node in the required side (left/right), at which point it exits the loop and returns the ID of the parent node and the direction of this empty child node (left/right).


#### 5. Insert Function

This function will insert this new value as well as its new ID. The parent node's child data is updated with this new ID.

Since each node is given an ID, duplicate values or other data types can be handled. The function for comparing and assigning child direction is externalised, so other metrics can be used (alphabetical, complex calculations, etc).


## Considerations and Issues Encountered

1. Duplicates are handled by just treating it as "lower" i.e. move to left child node.
2. At first I wanted to implement a list of "one-legged nodes", a priority FIFO list to jump to when inserting the next value. However, I realised that the BST has to be searched from the top sequentially, so parachuting a high value in a lower value branch will cause it to never be found.