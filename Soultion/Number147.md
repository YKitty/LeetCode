# Number:147

------------------

思路：

创建一个辅助链表，采用双指针，prev和cur进行寻找插入位置然后进行插入即可



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
    
    //正在验证
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
            size_t i = 0;
            for (i = v.size() - 1; i >= 0; i--)
            {
                if (cur->val > v[i]->val)
                {
                    if (i == v.size() - 1)
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
            if (i < 0)
            {
                v.insert(v.begin(), cur);
            }
            cur = cur->next;
        }
        
        ListNode* newList = nullptr;
        for (size_t i = v.size() - 1; i >= 0; i--)
        {
            v[i]->next = newList;
            newList = v[i];            
        }
        
        return newList;
    }
   
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

