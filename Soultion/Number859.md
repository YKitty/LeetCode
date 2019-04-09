# Number:859

---------

思路：

考虑边界条件：

1. 当a和b的长度不一致，失败
2. 长度一样，a的长度小于2，不能交换失败

方法一：正常情况。采用暴力求解法，对于任何的两个字符串都进行交换，并且在进行比较即可得出结果

​	对于采用暴力求解法时间复杂度高，无法通过

方法二：正常情况。

- 如果a==b的话，判断a中是否有重复的数字，如果有重复的数字，那就可以，否则就失败。判断重复时，可以先进行排序，然后在进行判断
- 如果a!=b的话，看不同的字符数是不是两个，如果是两个交换，判断是否相同
- 不是两个，就返回false

``` c++
class Solution {
public:
    bool buddyStrings(string A, string B) {
        switch(rand()%1 + 2)
        {
            case 1:
                return Equal(A, B);
            default:
                return Equal1(A, B);
        }
    }
    
    //暴力求解,一个一个改变
    //超出时间限制
    bool Equal(string a, string b)
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


        for (size_t i = 0; i < a.size(); i++)
        {
            for (size_t j = i + 1; j < a.size(); j++)
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

    bool Equal1(string a, string b)
    {
         if (a.size() != b.size() || a.size() < 2 || b.size() < 2)
         {
             return false;
         }

         //两个字符串相等判断有没有重复的
         if (a == b)
         {
             //进行一次排序，就可以比较相近的数据
             std::sort(a.begin(), a.end());
             for (size_t i = 0; i < a.size() - 1; i++)
             {
                 if (a[i] == a[i + 1])
                 {
                     return true;
                 }

                 return false;
             }
         }

         //不相等，看不相同的字符是不是两个
         //交换之后会不会相等
         std::vector<int> position;
         for (size_t i = 0; i < a.size(); i++)
         {
             if (a[i] != b[i])
             {
                 position.push_back(i);
             }
         }

         if (position.size() != 2)
         {
             return false;
         }
         std::swap(a[position[0]], a[position[1]]);
         if (a == b)
         {
             return true;
         }
         return false;  
    }
};
```

