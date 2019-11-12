---
title: 897. Increasing Order Search Tree
categories: 
- LeetCode
tags:
- Coding
---

### Question：

给定一个二叉树，将树的节点重新排列，使当前树的最左子节点为根节点，排列顺序依照 in-order，且每个节点只有右孩子，没有左孩子。



### Solution：

#### Ⅰ 思路

result = inorder(root.left) + root + inorder(root.right)

令 next_ 为原树 in-order 遍历中的下一个节点， 新树的左子树为 linked list + root，新树的右子树为 linked list + next_。

<!--more-->

#### Ⅱ 关键代码

**C++**

```c++
    TreeNode* increasingBST(TreeNode* root, TreeNode* next_ = NULL) {
        if (!root) return NULL;
        TreeNode* res = increasingBST(root->left, root);
        root->left = NULL;
        root->right = increasingBST(root->right, next_);
        return res;
    }
```

**Java**

```java
    public TreeNode increasingBST(TreeNode root) {
        return increasingBST(root, null);
    }

    public TreeNode increasingBST(TreeNode root, TreeNode next_) {
        if (root == null) return null;
        TreeNode res = increasingBST(root.left, root);
        root.left = null;
        root.right = increasingBST(root.right, next_);
        return res;
    }
```

**Python**

```python
    def increasingBST(self, root, next_ = None):
        if not root: return None
        res = self.increasingBST(root.left, root)
        root.left = None
        root.right = self.increasingBST(root.right, next_)
        return res
```

