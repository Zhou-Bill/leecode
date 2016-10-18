## Longest Substring Without Repeating Characters

```
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        int length = s.size(), i = 0,j=0,sum,max=1,pos,pos2;
        if (length == 0)
            return 0;
        //cout << s.find('b',2) << endl;
        for (i = 0; i < length; i++){
            pos = s.find(s[i], i + 1) == -1 ? length : s.find(s[i], i + 1);
            sum = 1;
            for (j = i + 1; j < pos; j++){
                pos2 = s.find(s[j], j + 1) == -1 ? length : s.find(s[j], j + 1);
                if (pos2 < pos){
                    pos = pos2;
                }
                sum++;
            }
            if (sum >max){
                max = sum;
            }
        }
        
        return max;
    }
};

```

> 实例为abcabcbb,他的最长不重复子串就是abc ，长度为3，"pwwkew" 它的最长不重复子串就是wke，或者是kew，长度为3

---

> 程序思想，例子为abcabcbb

* 首先以abcabcbb 做循环
* 找到 a ，a重复出现的下一个位置 是3,然后长度+1，b的下一个重复位置是4，如果重复的位置提前了（3<4,当然现在是不需要把pos值更换的，因为b的重复位置比a的重复位置出现更后一点），那么就更换重复位置的值
* 然后再对比一下最大值，如此类推

> 字符串操作用到了find

```
string name = "bill";
name.find('b'); // 若找不到则返回-1

//从下标第n个开始查找
name.find('b',2);


```
