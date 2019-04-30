# Number:102

-----------------

题目：给定一个二叉树，返回其按层次遍历的节点值。 （即逐层地，从左到右访问所有节点）。

例如:
给定二叉树: `[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7
```

返回其层次遍历结果：

```
[
  [3],
  [9,20],
  [15,7]
]
```



思路：层序遍历一般来说确实是用队列实现的，但是这里很明显用递归前序遍历就能实现呀，而且复杂度O(n)。。。

要点有几个：

- 利用`depth`变量记录当前在第几层（从0开始），进入下层时`depth + 1`；
- 如果`depth >= vector.size()`说明这一层还没来过，这是第一次来，所以得扩容咯；
- 因为是前序遍历，中-左-右，对于每一层来说，左边的肯定比右边先被遍历到，实际上后序中序都是一样的。。。



**C++**

``` C++
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        std::vector<std::vector<int>> ans;
        level(root, 0, ans);
        
        return ans;
    }
    
    void level(TreeNode* root, int depth, std::vector<std::vector<int>>& ans)
    {
        if (!root) return ;
        
        if (depth >= ans.size()) 
            ans.push_back(std::vector<int>());
        ans[depth].push_back(root->val);
        level(root->left, depth + 1, ans);
        level(root->right, depth + 1, ans);

    }
};
```

