###Length of Last Word

>  Given a string s consists of upper/lower-case alphabets and empty space characters ' ', return the length of last word in the string.

>If the last word does not exist, return 0.

>Note: A word is defined as a character sequence consists of non-space characters only.

>For example, 
Given s = "Hello World",
return 5.

```
class Solution {
public:
    int lengthOfLastWord(string s) {
        int i = 0, length=s.size(), count = 0;
        bool flag = false;
        for (i = length-1; i >= 0; i--){
            if (s[i] == ' ' && flag){
                break;
            }
            else{
                if (s[i] == ' '){
                    continue;
                }
                count++;
                // 这里标记一下，表明一开始那个字符(s[length-1])不为空
                flag = true;
            }
        }
        return count;
        
    }
};

```

> 这道题很简单，只要从后面往前面找就可以了，但是要判定一下一开始那个字符是否为‘ ’,如果为‘ ’,是那么就继续往下找，不为空就count+1，知道中间出现‘ ’，就停止