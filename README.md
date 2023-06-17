# QUESTION 2 (Algorithms)

## Metadata

Language: Python

Environment Setup: A virtual environment was not used as no modules were imported


## Background and Assumptions
This Binary Search Tree (BST) is made up of nodes which branch out to 2 lower nodes, with the left one being of a lower integer value and the right one being higher.


## Submission (main)

This method picks numbers at random from the numbers_list, and places them in an available location in the BST.

Since each node is given an ID, duplicate values can be handled.

The function for comparing and assigning child direction is externalised, so other metrics can be used.

### Steps

1. Initialise
2. Sort the list if needed
3. 


## Considerations and Issues Encountered

1. Duplicates are handled by just treating it as "lower" i.e. move to left child node.
2. At first I wanted to implement a list of "one-legged nodes", a priority FIFO list to jump to when inserting the next value. However, I realised that the BST has to be searched from the top sequentially, so parachuting a high value in a lower value branch will cause it to never be found.