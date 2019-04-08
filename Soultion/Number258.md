# Number:258

-------------

思路：

一：使用两个循环，内部循环进行每次++操作，外部循环进行判断，是否结束

二：找规律

1	1

2	2

...

9	9

10	1

11	2

...

22	4

...

101	2

可以看到对于大部分的数字都是**直接num%9**就可以得到累加和，但是也有着特例那就是对于**9的倍数**，9,18,等等num%9之后等于0，实际上是9。

1. **小于9，直接返回**
2. **大于9进行取余**
3. **不等于0，直接返回num%9**
4. **等于0，返回9即可**

三：**（num-1）% 9 + 1**

使用这个公式直接，将是9的倍数也变成了常用的情况了

举例：9

(9 - 1) % 9 = 8

8 + 1= 9


```c++
class Solution {
public:
    int addDigits(int num) {
        
        switch(rand() % 3 + 1)
        {
            case 1:
                return Solution1(num);
            case 2:
                return Solution2(num);
            default:
                return Solution3(num);
        }
        
    }
    
    int Solution1(int num)
    {
        while (num > 9)
        {
            int sum = 0;
            while (num)
            {
                sum += num % 10;
                num /= 10;
            }
            
            num = sum;
        }
          
        return num;
    }
    
    int Solution2(int num)
    {
        return num / 9 == 0 ? num : (num % 9 == 0 ? 9 : (num % 9));
    }
    
    int Solution3(int num)
    {
        return (num - 1) % 9 + 1;
    }
    
};
```

