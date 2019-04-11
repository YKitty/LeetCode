# Number:575

---------------

思路：

假设有a种糖果，b个糖果。首先给弟弟分出每类糖果减去一个的糖果b-a。

分为两种情况：

- 如果**b-a≥糖果总数的一半=b/2（也就是b≥2a）**。说明糖果种类小于糖果总数的一半。那么妹妹就可以分的所有种类的糖果。也就是**a种**。
- 如果**b-a＜糖果总数的一半=b/2（也就是b＜2a）**。说明糖果种类大于糖果总数的一半。此时对于弟弟没有分到一般的糖果，还需要加上**b/2-(b - a)=a- b/2**个糖果，妹妹也就在a种糖果的基础上少了**a-b/2**种，所以分得a-(a-b/2)种，即**b/2种**。



**C++**

``` c++
int distributeCandies(vector<int>& candies) {
        set<int> kind(candies.begin(),candies.end());//求出种类
    	//进行判断返回
        if(candies.size()>=2*kind.size())
            return kind.size();
        return candies.size()/2;
    }

//优化：每次返回的时候一定是种类数和糖果总数一半中的较小值
int distributeCandies(vector<int>& candies) {
        set<int> kind(candies.begin(),candies.end());
        return min(candies.size()/2,kind.size());
    }
```

