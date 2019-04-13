# Number:680

--------------

题目：验证回文字符串，最多删除一个字符

思路：

第一种：直接暴力求解，对于每一个字符都进行删除判断

第二种：只遍历一次，当遍历到不相等时。

给左边增加右边的字符，或者给右边增加左边的字符再次进行判断即可



**C++**

``` C++
class Solution {
public:
    bool validPalindrome(string s) {
        switch(rand()%1 + 2)
        {
            case 1:
                return DelCheck(s);
            default:
                return Check1(s);
        }
    }
    
    bool Check(std::string s)
    {
        if (s.size() <= 1)
            return true;
        
        int left = 0, right = s.size() - 1;
        
        while (left < right)
        {
            if (s[left] != s[right])
                return false;
            
            left++;
		    right--;
        }
        
        return true;
    }
    
    //暴力求解，时间复杂度过大
    bool DelCheck(std::string s)
    {
        if (Check(s))
            return true;
        
        for (int i = 0; i < s.size(); i++)
        {
            std::string tmp = s;
            tmp.erase(i, 1);
            if (Check(tmp))
                return true;
        }
        
        return false;
    }
    
    //一次遍历,时间复杂符O(N)
    bool Check1(std::string s)
    {
        if (s.size() <= 1)
            return true;
        
        int left = 0, right = s.size() - 1;
        while (left < right)
        {
            if (s[left] != s[right])
            {
                //左边增加右边字符，或者右边增加左边字符
                std::string tmp1 = s, tmp2 = s;
                tmp1.insert(left, 1, s[right]);
                tmp2.insert(right + 1, 1, s[left]);
                if (Check(tmp1) || Check(tmp2))
                    return true;
                return false;
            }
            
            left++;
            right--;
        }
        
        return true;
    }
};
```

