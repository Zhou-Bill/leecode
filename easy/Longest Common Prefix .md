##Longest Common Prefix  

>Write a function to find the longest common prefix string amongst an array of strings.

给定一个数组，找出数组中每个元素共有的字符串前缀，["289", "25324", "22434", "232", "234" ] ,共有的前缀就是 “2”


```
#include <iostream>
#include <vector>
#include <string>
using namespace std;

class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {
        int length = strs.size(),i=0,j,commonSize;

        if (length < 1) {
            return "";
        }
        string common = strs[0];
        commonSize = common.size();
        for (i = 1; i < length; i++){
            for (j = 0; j < commonSize; j++){
                if (strs[i][j] == common[j])
                    continue;
                else
                {
                    commonSize = j;
                    break;
                }
                if (j == commonSize)
                    return "";
            }
        }
        return  common.substr(0, commonSize);
        
    }
};
int main() {
    Solution solution;
    vector<string> strs = { "289" };
    cout << solution.longestCommonPrefix(strs);
}
```

* 这道题很简单，首先把数组中的第一个值作为他们的共同前缀，然后去遍历后面的值，如果他们相等，就continue，没有就break，那么这个共有前缀的数组在这个下标就已经结束了，然后就记录这个下标，做后续的判断，最后就是在这个共有前缀的数组中截取下标前的值