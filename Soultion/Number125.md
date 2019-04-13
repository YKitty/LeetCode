# Number:125

------------

**题目：验证回文串**

思路：

左右指针，左指针向右走，右指针向左走。关键要注意一个点：

就是如果直接判断时，就会出现，0P出现出错的情况。

0的ASCII：48

P的ASCII：80

直接判断就会出现错误。



**C++**

``` C++
class Solution {
public:
    bool isPalindrome(string s) {
        switch(rand()%1 + 3)
        {
            case 1:
                return Check(s);
            default:
                return Check1(s);
        }
    }
    
    //思想简单，但是代码冗余
    bool Check(std::string s)
    {
        if (s.size() <= 1)
            return true;
        
        int left = 0;
        int right = s.size() - 1;
        while (left < right)
        {
            while (left < right && NotExist(s[left]))
                left++;
            while (left < right && NotExist(s[right]))
                right--;
            
            //不能直接这样判断会出现OP，这样的错误
            //0 ASCII:48
            //P ASCII:80
            if ((s[left] <= '9' && s[left] >= '0') &&\
                (s[right] >= 'A' && s[right] <= 'Z'))
                return false;
            else if ((s[right] <= '9' && s[right] >= '0') && \
                    (s[left] >= 'A' && s[right] <= 'Z'))
                return false;
            else if ((s[left] !=  s[right] && \
               s[left] != (s[right] + 32) && \
               s[left] != (s[right] - 32)))
                return false;
            left++;
            right--;
        }
        
        return true;
    }
    
    bool NotExist(char c)
    {
        if ((c >= 'A' && c <= 'Z') || \
            (c >= 'a' && c <= 'z') || \
            (c >= '0' && c <= '9'))
            return false;
        return true;
    }
    
    //使用库函数，代码简单
    bool Check1(std::string s)
    {
        if (s.size() <= 1)
            return true;
        
        //将大写都变成小写的，防止出现0P的错误
        int left = 0, right = s.size() - 1;
        while (left < right)
        {
            while (left < right && !isdigit(s[left]) && !isalpha(s[left]))
                left++;
            while (left < right && !isdigit(s[right]) && !isalpha(s[right]))
                right--;
            
            if (left < right && tolower(s[left]) != tolower(s[right]))
                return false;
            
            left++;
            right--;
        }
        
        return true;
    }
};
```

