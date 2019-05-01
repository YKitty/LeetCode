# Number:79

-------------------

**题目：**给定一个二维网格和一个单词，找出该单词是否存在于网格中。

单词必须按照字母顺序，通过相邻的单元格内的字母构成，其中“相邻”单元格是那些水平相邻或垂直相邻的单元格。同一个单元格内的字母不允许被重复使用。

**示例:**

```
board =
[
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
]

给定 word = "ABCCED", 返回 true.
给定 word = "SEE", 返回 true.
给定 word = "ABCB", 返回 false.
```

**思路：**

和迷宫的回溯算法一样，进行四个方向进行遍历，当单词长度等于深度时，说明已经找到了，否则继续进行即可



**C++**

``` C++
class Solution {
public:
    bool exist(vector<vector<char>>& board, string word) {
        int sizex=board.size();
            if(sizex<=0||word.size()==0)
                return false;
            int sizey=board[0].size();
            vector<vector<int>> used(sizex,vector<int>(sizey,0));
            for(int i=0;i<sizex;i++)
                for(int j=0;j<sizey;j++)
                {
                    if(dfs(0,i,j,board,word,used))
                        return true;
                }
            return false;
        }

        bool dfs(int i,int posx,int posy,vector<vector<char>>& board,string word,vector<vector<int>>& used)
        {
            int len=word.size(),sizex=board.size();
            if(sizex==0)
                return false;
            int sizey=board[0].size();
            if(i>=len)
                return true;
            if(posx>=sizex||posx<0||posy>=sizey||posy<0)
                return false;
            if(board[posx][posy]!=word[i]||used[posx][posy]==1)
                return false;
            used[posx][posy]=1;
            if(dfs(i+1,posx+1,posy,board,word,used))
                return true;
            if(dfs(i+1,posx-1,posy,board,word,used))
                return true;
            if(dfs(i+1,posx,posy+1,board,word,used))
                return true;
            if(dfs(i+1,posx,posy-1,board,word,used))
                return true;
            used[posx][posy]=0;
            return false;
        }
};
```

