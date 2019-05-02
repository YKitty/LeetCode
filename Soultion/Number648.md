# Number:648

-------------

**题目：**

在英语中，我们有一个叫做 `词根`(root)的概念，它可以跟着其他一些词组成另一个较长的单词——我们称这个词为 `继承词`(successor)。例如，词根`an`，跟随着单词 `other`(其他)，可以形成新的单词 `another`(另一个)。

现在，给定一个由许多词根组成的词典和一个句子。你需要将句子中的所有`继承词`用`词根`替换掉。如果`继承词`有许多可以形成它的`词根`，则用最短的词根替换它。

你需要输出替换之后的句子。

**示例 1:**

```
输入: dict(词典) = ["cat", "bat", "rat"]
sentence(句子) = "the cattle was rattled by the battery"
输出: "the cat was rat by the bat"
```

**注:**

1. 输入只包含小写字母。
2. 1 <= 字典单词数 <=1000
3. 1 <=  句中词语数 <= 1000
4. 1 <= 词根长度 <= 100
5. 1 <= 句中词语长度 <= 1000

**思路：**

暴力法：直接对于每一个词进行查找判断



**C++**

``` c++
class Solution {
public:
    string replaceWords(vector<string>& dict, string sentence) {
        string resStr = "";
        set<int> rootLenSet;//词根的长度集合
        vector<string> words;//存储sentence以空格分割结果
        //第一步：以空格为界进行分割
        spilt(words, sentence, ' ');
        //第二步：将词根容器转换为set容器，并且统计各个词根的长度
        set<string> dictSet(dict.begin(), dict.end());//转换为set
        for (auto &rootS : dict){
            rootLenSet.insert(rootS.size());
        }
        //第三步：开始搜索各个单词是否存在词根
        for (auto &word : words){
            bool flag = false;//是否找到词根的标志
            string rootStr = "";//已经找的词根
            int wordSize = word.size();
            //词根的长度必须是词根集合中的元素，并且不大于word自身的长度（由于集合是有序的，所以第一次找到的必定是最短的词根）
            for (auto it = rootLenSet.begin(); it != rootLenSet.end() && *it <= wordSize; ++it){
                rootStr = word.substr(0, *it);//获取word的前*it个字符
                if (dictSet.find(rootStr) != dictSet.end()){//判断这个是否是词根
                    flag = true;
                    break;
                }
            }
            if (flag){
                //如果是词根，则直接放入词根
                resStr += rootStr + " ";
            }
            else{
                //否则放入原单词
                resStr += word + " ";
            }
        }
        //最后需要去掉多余余的空格
        if (resStr.size() > 0){
            resStr.resize(resStr.size() - 1);
        }
        return resStr;
    }
    //将sentence字符串以ch为界进行分割
    void spilt(vector<string> &words, string &sentence, char ch){
        int sentenceSize = sentence.size(), index = 0;
        while (index < sentenceSize){
            string tempStr = "";//截取上一个ch到下一个ch之间的字符段
            while (index < sentenceSize && sentence[index] != ch){
                tempStr += sentence[index++];
            }
            words.push_back(tempStr);
            index += 1;
        }
    }
};
```

