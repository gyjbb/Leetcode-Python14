# Leetcode-Python14
Binary Tree 3

## 104. Maximum Depth of Binary Tree

June 01, 2023  4h

Congratulations!\
This is the fourteenth day for leetcode python study. Today we will learn more about the Binary Tree!\
The challenges today are about ~~need to delete later~~.\
We will escape 迭代法 for now. 二刷有精力的时候 再去掌握迭代法。


## 104. Maximum Depth of Binary Tree
[Reading link](https://github.com/youngyangyang04/leetcode-master/blob/master/problems/0104.%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E6%9C%80%E5%A4%A7%E6%B7%B1%E5%BA%A6.md）\
[leetcode](https://leetcode.com/problems/maximum-depth-of-binary-tree/)\
[video](https://www.bilibili.com/video/BV1Gd4y1V75u/?spm_id_from=333.788&vd_source=63f26efad0d35bcbb0de794512ac21f3)\
二叉树的最大深度 （优先掌握递归）\
什么是深度，什么是高度，如何求深度，如何求高度，这里有关系到二叉树的遍历方式。\
深度是任意一个节点到根节点的距离，求深度用前序遍历，根节点深度是1。高度是任意一个节点到叶子节点的距离，求高度用后序遍历，叶子节点高度是1.\
根节点的高度，就是二叉树的最大深度。可以用后序遍历去求深度了。\
In recursion, 中 是我们的处理逻辑。
```python
# ways 1: recursion and postorder traversal
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        return self.getdepth(root)
    
    def getdepth(self,node):
        if not node:
            return 0
        left_height = self.getdepth(node.left) #左
        right_height = self.getdepth(node.right) #右
        height = 1 + max(left_height, right_height)  #中
        return height
```
```python
# ways 1: recursion and postorder traversal simple versionn
class solution:
    def maxdepth(self, root: treenode) -> int:
        if not root:
            return 0
        return 1 + max(self.maxdepth(root.left), self.maxdepth(root.right))
```
```python
# ways 2: 迭代法，层序遍历with queue：
class Solution:
    def maxDepth(self, root: TreeNode) -> int:
        if not root:
            return 0
        
        depth = 0
        queue = collections.deque([root])
        
        while queue:
            depth += 1
            for _ in range(len(queue)):
                node = queue.popleft()
                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)
        
        return depth
```

#### 



## 111.
二叉树的最小深度 （优先掌握递归）\
和最大深度 看似差不多，其实 差距还挺大，有坑。\



## 222.
完全二叉树的节点个数（优先掌握递归）\
需要了解，普通二叉树 怎么求，完全二叉树又怎么求。\

