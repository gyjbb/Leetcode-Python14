# Leetcode-Python14
Binary Tree 3

## 104. Maximum Depth of Binary Tree, 111. Minimum Depth of Binary Tree, 222. Count Complete Tree Nodes

June 01, 2023  4h

Congratulations!\
This is the fourteenth day for leetcode python study. Today we will learn more about the Binary Tree!\
The challenges today are about using recursion and postorder traversal to solve problems.\
We will focus on **recursion** to solve all the three challenges today and escape 迭代法 for now. 二刷有精力的时候 再去掌握迭代法。


## 104. Maximum Depth of Binary Tree
[Reading link](https://github.com/youngyangyang04/leetcode-master/blob/master/problems/0104.%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E6%9C%80%E5%A4%A7%E6%B7%B1%E5%BA%A6.md)\
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
# ways 1: recursion and postorder traversal simple version
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
       

#### 559. Maximum Depth of N-ary Tree
```python
# ways 1: recursion and postorder traversal simple version
"""
# Definition for a Node.
class Node:
    def __init__(self, val=None, children=None):
        self.val = val
        self.children = children
"""
class Solution:
    def maxDepth(self, root: 'Node') -> int:
        if not root:
            return 0

        max_depth = 1

        for child in root.children:
            max_depth = max(max_depth, self.maxDepth(child)+1)
        
        return max_depth
```
```python
# ways 2: 迭代法，层序遍历with queue：
class Solution:
    def maxDepth(self, root: 'Node') -> int:
        if not root:
            return 0
        
        depth = 0
        queue = collections.deque([root])

        while queue:
            depth += 1
            for _ in range(len(queue)):
                node = queue.popleft()
                for child in node.children:
                    queue.append(child)

        return depth
```
```python
# ways 3: simply use stack:
class Solution:
    def maxDepth(self, root: 'Node') -> int:
        if not root:
            return 0
        
        max_depth = 0
        stack = [(root, 1)]

        while stack:
            node, depth = stack.pop()
            max_depth =  max(max_depth, depth)
            for child in node.children:
                stack.append((child, depth+1))

        return depth
```

## 111.Minimum Depth of Binary Tree
[leetcode](https://leetcode.com/problems/minimum-depth-of-binary-tree/)\
[reading](https://github.com/youngyangyang04/leetcode-master/blob/master/problems/0111.%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E6%9C%80%E5%B0%8F%E6%B7%B1%E5%BA%A6.md)\
[video](https://www.bilibili.com/video/BV1QD4y1B7e2/?spm_id_from=pageDriver&vd_source=63f26efad0d35bcbb0de794512ac21f3)\
二叉树的最小深度 （优先掌握递归）\
和最大深度 看似差不多，其实 差距还挺大，有坑。\
最小深度是根节点和最近的叶子节点的最小距离。此处我们也用后续遍历去求深度， 因为深度就等于根节点的高度。
```python
# ways 1: recursion and postorder traversal:
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def getDepth(self, node):
        if node is None:
            return 0
        leftDepth = self.getDepth(node.left)   # 左
        rightDepth = self.getDepth(node.right)   # 右

        # 当一个左子树为空，右不为空，这时并不是最低点
        if node.left is None and node.right is not None:
            return 1+rightDepth
        # 当一个右子树为空，左不为空，这时并不是最低点
        if node.left is not None and node.right is None:
            return 1+leftDepth    

        result = 1 + min(leftDepth, rightDepth)
        return result

    def minDepth(self, root: Optional[TreeNode]) -> int:
        return self.getDepth(root)
```
```python
# ways 1: recursion and postorder traversal simpler solution:
class Solution:
    def minDepth(self, root):
        if root is None:
            return 0
        if root.left is None and root.right is not None:
            return 1 + self.minDepth(root.right)
        if root.left is not None and root.right is None:
            return 1 + self.minDepth(root.left)
        return 1 + min(self.minDepth(root.left), self.minDepth(root.right))
```

## 222. Count Complete Tree Nodes
[leetcode](https://leetcode.com/problems/count-complete-tree-nodes/)\
[reading](https://github.com/youngyangyang04/leetcode-master/blob/master/problems/0222.%E5%AE%8C%E5%85%A8%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E8%8A%82%E7%82%B9%E4%B8%AA%E6%95%B0.md)\
[video](https://www.bilibili.com/video/BV1eW4y1B7pD/?spm_id_from=pageDriver&vd_source=63f26efad0d35bcbb0de794512ac21f3)\
完全二叉树的节点个数（优先掌握递归）\
需要了解，普通二叉树 怎么求，完全二叉树又怎么求。\
We use postorder traversal and recusion to finish this question.
```python
# ways 1:普通二叉树 递归法 postorder traversal：
class Solution:
    def countNodes(self, root: TreeNode) -> int:
        return self.getNodesNum(root)
        
    def getNodesNum(self, cur):
        if not cur:
            return 0
        leftNum = self.getNodesNum(cur.left) #左
        rightNum = self.getNodesNum(cur.right) #右
        treeNum = leftNum + rightNum + 1 #中
        return treeNum
```
```python
# ways 1:精简版本
class Solution:
    def countNodes(self, root: TreeNode) -> int:
        if not root:
            return 0
        return 1 + self.countNodes(root.left) + self.countNodes(root.right)
```

```python
# ways 2:完全二叉树, 节点数是2的n次方-1， n是二叉树的深度。
class Solution:
    def countNodes(self, root: TreeNode) -> int:
        if not root:
            return 0
        left = root.left   # define two pointers
        right = root.right
        leftDepth = 0  #这里初始为0是有目的的，为了下面求指数方便
        rightDepth = 0
        while left: #求左子树深度
            left = left.left
            leftDepth += 1
        while right: #求右子树深度
            right = right.right
            rightDepth += 1
        if leftDepth == rightDepth:
            return (2 << leftDepth) - 1 #注意(2<<1) 相当于2^2，所以leftDepth初始为0
        return self.countNodes(root.left) + self.countNodes(root.right) + 1       #精简版本， 左右中，是后序遍历。
```


