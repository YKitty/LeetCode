# Number:118

**题目：**

给定一个非负整数 *numRows，*生成杨辉三角的前 *numRows* 行。

![img](https://upload.wikimedia.org/wikipedia/commons/0/0d/PascalTriangleAnimated2.gif)

在杨辉三角中，每个数是它左上方和右上方的数的和。

**示例:**

```
输入: 5
输出:
[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]
```

**思路：**

- 先开辟一个二维数组，将其进行初始化
- 对于需要进行相加的数进行相加即可



**代码：**

**C++**

``` C++
class Solution {
public:
    vector<vector<int>> generate(int numRows) {
        vector<vector<int>> vvarray;
        
        //将该二维数组初始化为numRows行
        vvarray.resize(numRows);
        
        //开辟空间，并且全都置为1，左右两侧
        for (size_t row = 0; row < numRows; ++row)
        {
            vvarray[row].resize(row + 1);
            vvarray[row][0] = 1;
            vvarray[row][row] = 1;
        }
        
        //进行加
        for (size_t row = 0; row < numRows; ++row)
        {
            for (size_t col = 0; col < vvarray[row].size(); ++col)
            {
                if (vvarray[row][col] == 0)
                {
                    vvarray[row][col] = vvarray[row - 1][col - 1] + vvarray[row - 1][col];
                }
            }
        }
        
        return vvarray;
    }
};
```



