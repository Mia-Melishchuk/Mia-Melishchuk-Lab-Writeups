# Lab 2 Writeup by Mia Melishchuk
### Code
```
class Solution:
    def mergeTrees(self, root1: TreeNode | None, root2: TreeNode | None) -> TreeNode | None:
        root3 = TreeNode()

        def recursiveMethod(root1, root2, root3):
            if root1 != None and root2 != None:
                root3 = TreeNode(root1.val + root2.val)
                root3.left = recursiveMethod(root1.left, root2.left, root3.left)
                root3.right = recursiveMethod(root1.right, root2.right, root3.right)
            elif root1 == None and root2 != None:
                root3 = TreeNode(root2.val)
                root3.left = recursiveMethod(None, root2.left, root3.left)
                root3.right = recursiveMethod(None, root2.right, root3.right)
            elif root1 != None and root2 == None:
                root3 = TreeNode(root1.val)
                root3.left = recursiveMethod(root1.left, None, root3.left)
                root3.right = recursiveMethod(root1.right, None, root3.right)
            else:
                root3 = None

            return root3

        root3 = recursiveMethod(root1, root2, root3)

        return root3
```
### Description
The goal of this exercise was to merge two binary trees by adding the keys of nodes in equivalent positions in each tree and returning a tree with the sums as the keys of the nodes. 
To do this, I created a recursive method that would traverse down each tree simultaneously with each new recursive call. 
(In retrospect, I could've used the given mergeTrees method at the top, but that misstep does not affect the time or space complexity since I would've been calling the original method the same number of times.)
I created a root3 reference for the head of the solution tree and had my recursive method take three parameters: a node from the first tree, a node from the second tree, and a node from the solution tree.
I wanted to do a pre-order traversal of the two trees, so in the cases where at least one the nodes from the two given trees wasn't null, I set the value of the corresponding node in the solution tree first before making any recursive calls.
The recursive calls set the left and right children of each node of the solution tree, or just set the node of the solution tree to null in the case where both nodes from the given trees were null (this is the base case).
After it reaches the base case and all of the recursive calls are completed, the method returns the original root3 that was passed in as the head of the solution tree. 
### Analysis
If *n* is the combined number of nodes in the two given trees, and since at each node two recursive calls are made, we are making 2*n* calls in the worst case. With the initial call, that means we are making 2*n*+1 recursive calls at worst. 
Assigning values and doing addition are both constant time operations, so the time complexity is O(2*n*+1), which simplifies to O(*n*). 

For space complexity, we are initializing a new TreeNode every time we traverse to a new node and at least one of the nodes at that level of the two given trees is not null. 
In the worst-case, we are initializing *n* new TreeNodes, leading to O(*n*) space complexity. In the best case, which is having the two given trees be identical, we are initializing *n*/2 new TreeNodes, still leading to O(*n*) space complexity.
