# Number:143

--------------

思路：

1. 采用快慢指针，直到分开的位置。将链表分成两个部分。

【注意】：对于前面的链表最后一个结点要变成nullptr

2. 对于后面的链表进行逆置
3. 将两个链表进行合并

【注意】：有可能后面的链表长度大于前面的链表要进行特殊处理



**C++**

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
    void reorderList(ListNode* head) {
        switch(rand()%1 + 1)
        {
            case 1:
                ReOrderList(head);
            default:
                return;
        }
    }
    
    void ReOrderList(ListNode* head)
    {
        //如果为空，或者长度小于等于2直接排列即可
        if (head == nullptr || head->next == nullptr || head->next->next == nullptr)    
            return ;
        
        //大于2，进行重新排列
        //分成前后两部分，然后后面逆置，两个合并
        ListNode* prev = nullptr;
        ListNode* low = head;
        ListNode* fast = head;
        while (fast)
        {
            if (fast->next == nullptr)
                break;
            fast = fast->next->next;
            prev = low;
            low = low->next;
        }
        //将前面的链表和后面的断开
        prev->next = nullptr;
        
        //后面的链表
        ListNode* back = low;
        ListNode* newBack = nullptr;
        //进行逆置
        while (back)
        {
            ListNode* nextBack = back->next;
            back->next = newBack;
            newBack = back;
            
            back = nextBack;
        }
        
        //进行合并,注意最后一般有可能是back的链表长度长
        ListNode* nextBack = nullptr;
        ListNode* nextFront = nullptr;
        ListNode* front = head;
        while (front && newBack)
        {    
            nextBack = newBack->next;
            nextFront = front->next;
            newBack->next = front->next;
            front->next = newBack;
            if (nextFront == nullptr)
            {
                newBack->next = nextBack;
            }
            front = nextFront;
            newBack = nextBack;
        }
    }

};
```

