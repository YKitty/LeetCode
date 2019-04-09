# Number:236

-----------

思路：

一：

首先判断边界条件，树为空，或者一个结点直接就是根节点，然后在进行正常的情况

1. 判断树是否为空
2. 判断其中一个结点是否为根节点
3. 判断两个节点是在树的那一边
4. 如果是在两边的话，直接返回当前结点
5. 如果是在同一边，继续向下遍历，从步骤1向下开始

二：

直接根据两个节点，拿到两台从根节点到这两个节点的链表，然后对于这两个链表进行查找第一个不相同结点的前一个节点即可

找不同结点时，必须要注意如果两个链表不一样长，当一个跑完的时候，必须要记录下来最后一个结点

三：

在左子树和右子树中查找有没有p，q结点。

- 左子树没有，判断右子树
- 右子树没有，判断左子树
- 如果左右子树都存在，那就是root结点

**C++**

``` c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        switch(3)
        {
            case 1:
                return FindAimNode(root, p, q);
            case 2:
                return FindAimNode1(root, p, q);
            default:
                return FindAimNode2(root, p, q);
        }
    }
    
    bool IsSide(TreeNode* root, TreeNode* aimNode)
    {
        if (root == nullptr)
        {
            return false;
        }
        
        if (root == aimNode)
        {
            return true;
        }
        
        if (IsSide(root->left, aimNode))
        {
            return true;
        }
        
        if (IsSide(root->right, aimNode))
        {
            return true;
        }
        
        return false;
    }
    
    //一个一个的向下找进行遍历,判断位置
    TreeNode* FindAimNode(TreeNode* root, TreeNode* p, TreeNode* q)
    {
        if (root == nullptr || p == root || q == root)
        {
            return root;
        }
        
        bool pLeft = IsSide(root->left, p);
        bool pRight = IsSide(root->right, p);
        bool qLeft = IsSide(root->left, q);
        bool qRight = IsSide(root->right, q);
        
        if ((pLeft && qRight) || (pRight && qLeft))
        {
            return root;
        }
        
        if (pLeft && qLeft)
        {
            return FindAimNode(root->left, p, q);
        }
        
        if (pRight && qRight)
        {
            return FindAimNode(root->right, p, q);
        }
        
        return nullptr;
    }
    
    bool GetList(TreeNode* root, TreeNode* aimNode, std::vector<TreeNode*>& list)
    {
        if (root == nullptr)
        {
            return false;
        }
        
        if (root == aimNode)
        {
            list.push_back(root);
            return true;
        }
        
        list.push_back(root);
        if (GetList(root->left, aimNode, list)) return true;
        if (GetList(root->right, aimNode, list)) return true;

        list.pop_back();        
        return false;   
    }
    
    //找到两条链表，然后查找公共结点即可
    TreeNode* FindAimNode1(TreeNode* root, TreeNode* p, TreeNode* q)
    {
        if (root == nullptr || p == root || q == root)
        {
            return root;
        }
        
        std::vector<TreeNode*> firstList, secondList;
        if (!GetList(root, p, firstList))   return nullptr;
        if (!GetList(root, q, secondList))  return nullptr;
        
        int len = firstList.size() < secondList.size() ? firstList.size() : secondList.size();
        //进行遍历查找,第一个不是相同结点的前一个节点即是所求结点
        TreeNode* result = root;
        for (int i = 0; i < len; i++)
        {
            if (firstList[i] != secondList[i])
                return result;
            
            result = firstList[i];
        }
        
        //最后必须返回result，有可能是一个是另外一个的父亲，一个走完另一个还没有完成
        return result;
    }
    
    //进行递归查找，判断在左子树中有没有，右子树中有没有，然后进行判断
    TreeNode* FindAimNode2(TreeNode* root, TreeNode* p, TreeNode* q)
    {
        if (root == nullptr || p == root || q == root)
        {
            return root;
        }
        
        //在左子树中查找
        TreeNode* left = FindAimNode2(root->left, p, q);
        //在右子树中查找
        TreeNode* right = FindAimNode2(root->right, p, q);
        
        if (left == nullptr)    return right;
        if (right == nullptr)   return left;
        
        return root;
    }
};
```



**C**

``` c
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     struct TreeNode *left;
 *     struct TreeNode *right;
 * };
 */

struct TreeNoode* FindAimNode(struct TreeNode* root, struct TreeNode* aimNode)
{
    if (root == NULL)
    {
        return NULL;
    }
    
    if (root == aimNode)
    {
        return root;
    }
    
    struct TreeNode* ret = FindAimNode(root->left, aimNode);
    if (ret)
    {
        return ret;
    }
    
    ret = FindAimNode(root->right, aimNode);
    if (ret)
    {
        return ret;
    }
    
    return NULL;
}

struct TreeNode* lowestCommonAncestor(struct TreeNode* root, struct TreeNode* p, struct TreeNode* q) {
    if (root == NULL)
    {
        return NULL;
    }
    
    if (p == root || q == root)
    {
        return root;
    }
    
    struct TreeNode* p_left = FindAimNode(root->left, p);
    struct TreeNode* p_right = FindAimNode(root->right, p);
    struct TreeNode* q_left = FindAimNode(root->left, q);
    struct TreeNode* q_right = FindAimNode(root->right, q);
    
    //p和q一左一右
    if ((p_left && q_right) || (p_right && q_left))
    {
        return root;
    }
    
    //p和q都在左边
    if (p_left && q_left)
    {
        return lowestCommonAncestor(root->left, p, q);
    }
    
    //p和q都在右边
    if (p_right && q_right)
    {
        return lowestCommonAncestor(root->right, p, q);
    }
    
    return NULL;
}
```

