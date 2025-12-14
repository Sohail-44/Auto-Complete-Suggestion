# Comp128 Project: Auto-Complete

Your last assignment is to implement a new type of tree data structure. This is a data structure that we have not discussed in class (although it is similar to other trees), so this assignment is meant to simulate the sorts of problems you might encounter as a developer: implementing a new data structure for a particular task. You should be well prepared for this based on your existing knowledge of trees and ADT implementations.

The context for this assignment is a text auto-complete program. Auto-complete checkers, like the predictive ones on your phone that provide word suggestions once you start typing, need to store a spelling dictionary in a way that makes it as fast as possible to see what words start with a specific prefix. For example if you started typing the word "do", the auto-complete program should quickly be able to suggest longer words like "dog" or "doctor" that contain the prefix "do".

To make this work efficiently with a tree, rather than storing each word as a node in the tree. We will break the words into individual characters. Each character will correspond to a node in the tree. If the node corresponds with the last letter in the word, then we will mark it using a boolean value that it is the end of a word. Let's look at an example for how each letter gets added, assuming we want to add the words "do", "don", "cat", and "car" to the tree:

<img width="1210" height="863" alt="image" src="https://github.com/user-attachments/assets/cdc43ccf-1132-4a40-b687-110e56be9c57" />
<img width="1210" height="863" alt="image" src="https://github.com/user-attachments/assets/87ea701e-48b3-441a-a414-59035934a0e0" />
<img width="1210" height="863" alt="image" src="https://github.com/user-attachments/assets/d446514e-9d24-47ad-b9aa-c7f0fcb16a81" />
<img width="1210" height="863" alt="image" src="https://github.com/user-attachments/assets/48159485-6c89-426e-bc9b-3eb4acf1cbda" />
<img width="1210" height="863" alt="image" src="https://github.com/user-attachments/assets/30072b92-1278-41a9-a7b0-666c4c112268" />
<img width="1210" height="873" alt="image" src="https://github.com/user-attachments/assets/7f1d68a1-b12c-4192-af25-c0bb95e139f1" />
<img width="1210" height="863" alt="image" src="https://github.com/user-attachments/assets/721c1b5a-81d5-4b5c-b658-0c9b07e983c6" />
<img width="1210" height="863" alt="image" src="https://github.com/user-attachments/assets/cdd7041d-a506-4d1a-a6e8-38853070738a" />
<img width="1210" height="863" alt="image" src="https://github.com/user-attachments/assets/eb4fc5ae-ce05-439f-9cda-7a3639a60104" />
<img width="1210" height="863" alt="image" src="https://github.com/user-attachments/assets/1da324cf-a347-49a7-9847-900dd426fef6" />
<img width="1210" height="863" alt="image" src="https://github.com/user-attachments/assets/6b091698-5afa-47aa-ac3a-201bb1e3d511" />
<img width="1210" height="863" alt="image" src="https://github.com/user-attachments/assets/a38d1ffc-b168-4d66-b9e7-8ea8f36dbf8a" />
<img width="1210" height="863" alt="image" src="https://github.com/user-attachments/assets/7d60fc2b-d485-4d27-9563-4b1812ea8a5d" />
<img width="1210" height="863" alt="image" src="https://github.com/user-attachments/assets/02b21c11-d306-4e35-85b1-5f06d1ebcb20" />
<img width="1210" height="873" alt="image" src="https://github.com/user-attachments/assets/36abae88-8474-47fe-8564-a4c7183353c4" />
<img width="1210" height="873" alt="image" src="https://github.com/user-attachments/assets/9414e9c8-6757-4acb-a357-9ede9c92e3d8" />



It is very fast to check whether a word is in the tree: start from the root and trace out the word along the edges; if one ends up at a word-terminating node (a purple node in the images above), then the word is in the tree, otherwise it is not.

This tree can also efficiently support auto-completion. Given the prefix-based structure of the tree, it is straightforward to enumerate all of the words that begin with a given letter sequence: these will be represented by nodes that are descendants of the node corresponding to that prefix.

There are multiple ways you might implement the structure shown in the images. We will use a simple implementation that uses a lot of space, but is fast. Each node of the tree has a boolean variable indicating whether a string ending there is a word (corresponding to whether the node is purple or orange in the diagrams). Each node also contains a Map representing outgoing links to child nodes. The map keys are individual letters, and the values are references to other tree nodes. Notice that this is not a binary tree. Each node might have up to 26 children.

## Task

Explore the starter code that we have given you. We have included a `TreeNode` class to represent nodes in the tree. There is also a `PrefixTree` class where you will write your code, and an `AutoComplete` class to play with your completed tree.

In the `PrefixTree` class implement the tree structure defined above. Specifically, you should implement the following methods:

### add(String word)

This should add the word to the tree by creating nodes for each character in the word (if they don't already exist in the tree!), and linking the nodes together by correctly inserting them in the children maps stored at each node.
When the last character is reached, that node should be marked as the end of a word.
If the word does not already exist in the tree, the size variable should be incremented. If the word already exists, this method should not change the tree structure or size variable. 
 
 The string `charAt` method may be helpful to get individual characters from the word.
 Once you complete this, the testAdd method in the `TestPrefixTree` file should pass.

### contains(String word)

This should return true if the word is contained in the tree. Starting at the root, you can iterate through the word's characters searching down the path of nodes. If each character is found in the correct order and the last is marked as a word, then the word is contained in the tree.

Once you complete this, the testContains method should pass.

### getWordsForPrefix(String prefix)

This should return a list of words contained in the tree that start with the prefix characters, including the prefix if it is a word itself. These words can be found by traversing through the letters of the prefix and then traversing any child decendents of the last prefix node.

There are multiple ways to implement this, but probably the easiest is to write a separate helper, recursive method to preorder-traverse the child decendents. Look in the BST activity for an example of a recursive pre-order traversal; however, note that this tree is not binary.

Once you complete this, the testPrefix method should pass.

## Play!
Once your tree is working, run the `AutoComplete` class. Enter the text for a prefix and it will show you the results from a dictionary:

```
Enter text prefix to search, or 'stop'.
appl
========== Results =============
applause
applaud
applauds
apple
apples
applique
applier
appliers
applies
applied
apply
applying

Enter text prefix to search, or 'stop'.
compu
========== Results =============
compute
computer
computes
computed
