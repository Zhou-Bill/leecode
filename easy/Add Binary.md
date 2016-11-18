##Add Binary

>Given two binary strings, return their sum (also a binary string).

>For example,
a = "11"
b = "1"
Return "100".

这道题就是字符串的二进制相加，我原本的方法是将他们两个转换成10进制，再相加，然后再转换成二进制，再从int 转为字符串

```
#include<iostream>
#include<vector>
#include<sstream>
using namespace std;

class Solution {
public:
    string addBinary(string a, string b) {
        int length1 = a.size() - 1, length2 = b.size() - 1;
        int i = 0, temp, temp2, num = 0;
        vector<int> data;
        string str = "", str2 = "";
        int length = length1 > length2 ? length2 : length1;
        for (i = 0; i <= length; i++){
            stringstream ss, ss2;
            ss << a[length1 - i];
            ss >> temp;
            ss2 << b[length2 - i];
            ss2 >> temp2;

            data.push_back((temp + temp2 + num) % 2);
            num = (temp + temp2 + num) / 2;

        }
        if (length1 > length2){
            for (i = length1-length2-1; i>=0; i--){
                stringstream s3;
                s3 << a[i];
                s3 >> temp;
                data.push_back((temp+num)%2);
                num = (temp + num) / 2;
            }
        }
        else
        {
            for (i = length2-length1-1; i >= 0; i--){
                stringstream s3;
                s3 << b[i];
                s3 >> temp;
                data.push_back((temp + num) % 2);
                num = (temp + num) / 2;
            }
        }
        if (num > 0){
            data.push_back(num);
            
        }

        reverse(data.begin(), data.end());
        for (vector<int>::iterator iter = data.begin(); iter != data.end(); ++iter)
        {
            stringstream ss;
            ss << *iter;
            ss >> str;
            str2 += str;
            //str += *iter;
        }
        for (i = 0; i < data.size(); i++){
            cout << data[i] << "  ";
        }

        return str2;
    }

};

int main() {
    string str1 = "110010";
    string str2 = "100";
    Solution solution;
    solution.addBinary(str1, str2);
}
```

* 另一个方法是找到最小的那个字符串长度，将共有的字符串相加，放入vector里面
* 然后长的那个字符串，判断一下有没有进位，有就相加，没有直接放入vector
* 翻转vector ，转换成string

第一种方法是不成功的，第二种方法太慢了

```
class Solution
{
public:
    string addBinary(string a, string b)
    {
        string s = "";
        
        int c = 0, i = a.size() - 1, j = b.size() - 1;
        while(i >= 0 || j >= 0 || c == 1)
        {
            c += i >= 0 ? a[i --] - '0' : 0;
            c += j >= 0 ? b[j --] - '0' : 0;
            s = char(c % 2 + '0') + s;
            c /= 2;
        }
        
        return s;
    }
};
```
