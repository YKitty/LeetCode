# Number:15

-----------

**题目**：

给定一个包含 *n* 个整数的数组 `nums`，判断 `nums` 中是否存在三个元素  *a，b，c ，* 使得  *a + b + c =*  0 ？找出所有满足条件且不重复的三元组。

**注意：** 答案中不可以包含重复的三元组。

```
例如, 给定数组 nums = [-1, 0, 1, 2, -1, -4]，

满足要求的三元组集合为：
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```

**思路**：

1. 判断边界条件，看元素个数是否小于3
2. 将数组进行排序，随后采用两个指针向中间查找的方法，查找数字

**代码**：

**C++**

``` C++
#include <iostream>
#include <vector>
#include <set>
#include <algorithm>

using namespace std;

class Solution {
public:
    vector<vector<int> > threeSum(vector<int>& nums) 
    {
        switch (rand() % 1)
        {
            case 0:
                return ThreeSum(nums);
        }
    }

    vector<vector<int> > ThreeSum(vector<int>& nums)
    {
        if (nums.size() < 3)
            return {};//列表初始化
        set<vector<int>> res;
        sort(nums.begin(), nums.end());
        int sum = 0;
        //小于size()-1，才会有k
        for (int j = 1, i , k; j < nums.size() - 1; j++)
        {
            i = 0;
            k = nums.size() - 1;
            while (i < j && j < k)
            {
                sum = nums[i] + nums[j] + nums[k];
                if (sum == 0)
                {
                    res.insert({nums[i], nums[j], nums[k]});
                    i++;

                    if (nums[j] == nums[k])
                        break;
                }
                else if (sum > 0) k--;
                else if (sum < 0) i++;
            }
        }
        
        return vector<vector<int>>(res.begin(), res.end());
    }
};

int main()
{
    vector<int> nums1 = {-1, 0, 1, 2, -1, -4};
    vector<vector<int>> res = Solution().threeSum(nums1);
    for( int i = 0 ; i < res.size() ; i ++ ){
        for( int j = 0 ; j < res[i].size() ; j ++ )
            cout<<res[i][j]<<" ";
        cout<<endl;
    }
    return 0;
}
```

