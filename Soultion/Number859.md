# Number:859

---------

思路：

考虑边界条件：

1. 当a和b的长度不一致，失败
2. 长度一样，a的长度小于2，不能交换失败
3. 正常情况，采用暴力求解法，对于任何的两个字符串都进行交换，并且在进行比较即可得出结果

``` c++
class Solution {
public:
    bool buddyStrings(string A, string B) {
        switch(rand()%1 + 1)
        {
            case 1:
                return Equal1(A, B);
            default:
                //return Equal2(A, B);
                return false;
        }
    }
    
    bool Equal1(string a, string b)
    {
        //边界条件
        if (a.size() != b.size())
        {
            return false;
        }
        if (a.size() < 2)
        {
            return false;
        }
        
        //暴力求解,一个一个改变
        for (size_t i = 0; i < a.size(); i++)
        {
            for (size_t j = i; j < a.size(); j++)
            {
                swap(a[i], a[j]);
                if (a == b)
                {
                    return true;
                }
                else 
                {
                    swap(a[i], a[j]);
                }
            }  
            
        }
        return false;
    }
};
```

