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
        switch(rand()%2 + 1)
        {
            case 1:
                return FindAimNode(root, p, q);
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
    
    //一个一个的向下找进行遍历
    TreeNode* FindAimNode(TreeNode* root, TreeNode* p, TreeNode* q)
    {
        if (root == nullptr)
        {
            return nullptr;
        }
        
        if (p == root || q == root)
        {
            return root;
        }
        
        bool pLeft = IsSide(root->left, p);
        bool pRight = IsSide(root->right, p);
        bool qLeft = IsSide(root->left, p);
        bool qRight = IsSide(root->right, p);
        
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
        
        bool left = GetList(root->left, aimNode, list);
        if (left)
        {
            return true;
        }
        
        bool right = GetList(root->right, aimNode, list);
        if (right)
        {
            return true;
        }
        
        return false;   
    }
    
    //找到两条链表，然后查找公共结点即可
    TreeNode* FindAimNode2(TreeNode* root, TreeNode* p, TreeNode* q)
    {
        if (root == nullptr)
        {
            return nullptr;
        }
        
        if (p == root || q == root)
        {
            return root;
        }
        
        std::vector<TreeNode*> firstList;
        GetList(root, p, firstList);
        std::vector<TreeNode*> secondList;
        GetList(root, q, secondList);
        
        //进行遍历查找,第一个不是相同结点的前一个节点即是所求结点
        TreeNode* prev = firstList[0];
        for (size_t i = 1; i < firstList.size(); i++)
        {
            if (firstList[i] != secondList[i])
            {
                return prev;
            }
            
            prev = firstList[i];
        }
        
        return nullptr;
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

