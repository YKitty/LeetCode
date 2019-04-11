# Number:888

----------

思路：

对于要进行平均糖果，两个的总数肯定是不一样的。

a的总和是sa，b的总和是sb

假设sa>sb，那么主要从a和b中找到一个数字，使用**a-b=(sa-sb)/2**即可



**C++**

``` C++
class Solution {
public:
    vector<int> fairCandySwap(vector<int>& A, vector<int>& B) {
        switch(2)
        {
            case 1:
                return CandySwap(A, B);
            default:
                return CandySwap1(A, B);
        }
    }
    
    //暴力求解，超出时间限制
    std::vector<int> CandySwap(std::vector<int> a, std::vector<int> b)
    {
        int sa = Sum(a);
        int sb = Sum(b);
        std::vector<int> ans;
        for (int i = 0; i < a.size(); i++)
        {
            for (int j = 0; j < b.size(); j++)
            {
                if (sa > sb && (a[i] - b[j]) == (sa - sb) / 2)
                {
                    ans.push_back(a[i]);
                    ans.push_back(b[j]);
                    
                    return ans;
                }
                else if (sa < sb && (b[j] - a[i]) == (sb - sa) / 2)
                {
                    ans.push_back(a[i]);
                    ans.push_back(b[j]);
                    
                    return ans;
                }
                
            }
        }
        
        return ans;
    }
    
    std::vector<int> CandySwap1(std::vector<int> a, std::vector<int> b)
    {
        int sa = Sum(a);
        int sb = Sum(b);
        std::unordered_set<int> usa(a.begin(), a.end());
        std::unordered_set<int> usb(b.begin(), b.end());

        std::vector<int> ans;
        if (sa > sb)
        {
            for (auto e : a)
            {
                int num = e - ((sa - sb) >> 1);
                if (usb.count(num) > 0)
                {
                    ans.push_back(e);
                    ans.push_back(num);
                    
                    return ans;
                }
            }
        }
        else 
        {
            for (auto e : b)
            {
                int num = e - ((sb - sa) >> 1);
                if (usa.count(num) > 0)
                {
                    ans.push_back(num);
                    ans.push_back(e);
                    
                    return ans;
                }
            }
        }
        
        return ans;
    }
    
    int Sum(std::vector<int> a)
    {
        int sum = 0;
        for (int i = 0; i < a.size(); i++)
        {
            sum += a[i];         
        }
        
        return sum;
    }
};
```

