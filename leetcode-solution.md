# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    
    def __init__(self):
        self.values = []
    
    def isValidBST(self, root: TreeNode) -> bool:
        self.inorder(root)
        print(self.values)
        for i in range(len(self.values)-1):
            if self.values[i+1] <= self.values[i]:
                return False
        return True
        
        
    def inorder(self, root):
        if root:
            self.inorder(root.left)
            self.values.append(root.val)
            self.inorder(root.right)
        else:
            return
