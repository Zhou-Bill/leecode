#Roman to Integer

>Given a roman numeral, convert it to an integer.

>Input is guaranteed to be within the range from 1 to 3999.

###### 给定一个字符串，由罗马数字组成，返回数字，比如"VI",返回就是6

```
#include <iostream>
using namespace std;

class Solution {
public:
    int romanToInt(string s) {
        int length = s.size(),i,sum=0,y,tmp=0;
        for (i = 0; i < length; i++){
            switch (s[i])
            {
            case 'I':
                y = 1;
                break;
            case 'X':
                y = 10;
                break;
            case 'C':
                y = 100;
                break;
            case 'V':
                y = 5;
                break;
            case 'L':
                y = 50;
                break;
            case 'D':
                y = 500;
                break;
            case 'M':
                y = 1000;
                break;
            }

            if (tmp >= y || i==0){
                sum = sum + y;
                tmp = y;
            }
            else
            {   
                sum = sum + y-tmp;
                sum = sum - tmp;
            }
        
        }
        return sum;
    }
};

int main() {

    Solution solution;
    int result = solution.romanToInt("DCXXI");
    cout << result;
}
```

* 罗马数字对应数字
* I(1)， X(10) , C(100) , M(1000) , V(5) , L(50) , D(500)
* 思想就是对字符串数组进行遍历，用switch 将对应的值提取出来
* "DCXXI"  其实可以发现无论怎么样都是把所有值加起来，但有一点要注意的是前后值的大小，在罗马数字里面，遵循 "左减右增" 规则。
* 那么我就将（转换后）前一个数字与（转换后）当前的数字做比较，如果比他小，那么就直接加就行了
* 如果比他小，则前一个值-后面那个值，然后加起来，但是这里有个问题就是一开始首先就加了第一个值，所以必须减掉

> DCXXI 

* D转换后因为是第一个数就加起来了，当前sum 的值为500，保存D转换后的值
* C 转换后是100 ，比上一个数字要小，就直接加起来，当前sum 为600
* 如此类推

> XCIX

* X转换后因为是第一个数就加起来了，当前sum 的值为10，保存X转换后的值
* C转换后比前一个数要大，所以(C-X)转换后的值是 90 ,由于之前sum 的值为10，再加此时的值就为100，那么就要前去第一个数才合理
* 如此类推
* 其实就是两个两个数比较，但是中间有一个阶段性的改变，就是C 跟 I 不是同一级别的，就直接加就可以了