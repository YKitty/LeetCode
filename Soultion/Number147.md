# Number:147

------------------

思路：

一：创建一个数组一个一个的向里面插入数据，然后拿出来就好了

二：创建一个辅助链表，采用双指针，prev和cur进行寻找插入位置然后进行插入即可



``` c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* insertionSortList(ListNode* head) {
        switch(1)
        {
            case 1:
                return GetList(head);
            default:
                return GetList2(head);
        }
    }
    
    //运行失败
    ListNode* GetList(ListNode* head)
    {
        if (head == nullptr)
        {
            return nullptr;
        }

        //只有一个结点
        if (head->next == nullptr)
        {
            return head;
        }

        //进行插入排序
        std::vector<ListNode*> v;
        v.push_back(head);
        ListNode* cur = head->next;
        while (cur)
        {
            int i = 0;
            for (i = v.size() - 1; i >= 0; i--)
            {
                if (cur->val > v[i]->val)
                {
                    //最后一个位置
                    if (i == (v.size() - 1))
                    {
                        v.insert(v.begin(), cur);
                        break;
                    }
                    else 
                    {
                        auto index = std::find(v.begin(), v.end(), v[i + 1]);
                        v.insert(index, cur);
                        break;    
                    }
                }
            }
            
            //第一个位置
            if (i < 0)
            {
                v.insert(v.begin(), cur);
            }
            cur = cur->next;
        }
        
        ListNode* newList = nullptr;
        for (int i = v.size() - 1; i >= 0; i--)
        {
            v[i]->next = newList;
            newList = v[i];            
        }
        
        return newList;
    }
   
    //成功
    ListNode* GetList2(ListNode* head)
    {
        if (head == nullptr)
        {
            return nullptr;
        }
        
        if (head->next == nullptr)
        {
            return head;
        }
        
        //必须要新开辟一个结点，否则就会遍历以前的所有节点
        ListNode* newList = new ListNode(0);
        while (head)
        {
            ListNode* cut = newList->next;;
            ListNode* prev = nullptr;
            while (cut != nullptr && cut->val < head->val)
            {
                prev = cut;
                cut = cut->next;
            }
            
            //必须将原链表的下一个结点记录下来，否则就会导致丢失了下一个结点
            ListNode* oldNext = head->next;
            if (prev == nullptr)
            {
                head->next = cut;
                newList->next = head;
            }
            else 
            {
                head->next = cut;
                prev->next = head;
            }
            
            head = oldNext;
        }
        
        return newList->next;
    }
};
```

