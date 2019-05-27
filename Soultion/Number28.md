# Number:28

题目：

实现 [strStr()](https://baike.baidu.com/item/strstr/811469) 函数。

给定一个 haystack 字符串和一个 needle 字符串，在 haystack 字符串中找出 needle 字符串出现的第一个位置 (从0开始)。如果不存在，则返回  **-1**。

**示例 1:**

```
输入: haystack = "hello", needle = "ll"
输出: 2
```

**示例 2:**

```
输入: haystack = "aaaaa", needle = "bba"
输出: -1
```

思路：

**第一种：**

暴力求解法：从 **src** 字符串中的每一个字符进行判断，是否存在 **des** 字符串

时间复杂度： **O(N * M)**

N：src字符串的长度

M：des字符串的长度

``` c++
int MystrStr(string src, string des)
{
    if(des.empty())
        return 0;

    for (int i = 0; i < src.size(); i++)
    {
        int index = i;
        int j = 0;
        for (; j < des.size(); j++)
        {
            if (des[j] != src[index++])
                break;
        }

        if (j == des.size())
            return i;
    }

    return -1;
}
```



**第二种：**

**两个指针 + 回滚**

``` c++
int MystrStr(string src, string des)
{
    if (des.empty())
        return 0;

    int first = 0;
    int second = 0;

    while (first < src.size() && second < des.size())
    {
        if (src[first] == des[second])
            second++;
        else 
        {
            first = first - second;
            second = 0;
        }

        first++;
    }

    return second == des.size() ? first - second : -1;
}
```

**第三种：**

**KMP算法**

参考资料：[博客：v_JUJY_v](https://blog.csdn.net/v_july_v/article/details/7041827)

``` c++
void GetNext(const string& des, int* next)
{
    //第一个位置为-1
    next[0] = -1;

    int cur_index = 0;
    int cal_index = -1;

    //每次计算的都是下一个数据元素
    while (cur_index < des.size() - 1)
    {
        if (cal_index == -1 || des[cal_index] == des[cur_index])
            next[++cur_index] = ++cal_index;

        else
            cal_index = next[cal_index];
    }
}

int Search(string src, string des, int* next)
{
    int i = 0;
    int j = 0;
    while (i < src.size() && j < (int)des.size())
    {
        if (j == -1 || src[i] == des[j])
        {
            i++;
            j++;
        }
        else
            j = next[j];
    }

    return j == des.size() ? i - j : -1;
}

/* KMP算法 */
int MystrStr(string src, string des)
{
    if (des.size() == 0)
        return 0;
    int* next = new int[des.size()];
    GetNext(des, next);

    return Search(src, des, next);
}
```

