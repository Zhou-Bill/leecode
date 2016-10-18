# String to Integer (atoi)


```
class Solution {
public:
    int myAtoi(string str) {
        if (str.size() == 0){
            return 0;
        }
        int n = 0;
        stringstream ss;
        ss << str;
        ss >> n;
        if (str[0] == '-' && str.size() >1){
            return n;
        }
        else
        {
            if (str[0] == '+' && str.size() >1){
                return n;
            }
            else if (str.size() == 1 && str[0] == '+'){
                return 0;
            }
            else{
                return n;
            }
        }
        return 0;    
    }
};
```

# 题目考查的是一种 未知输入，以及一个正确的输出

* c++ 的字符串转换成int ，使用stringstream，把字符串送到stringstream中，在吧stringstream送到int，实现字符串转换int
