## Palindrome Number

> 可以结合逆行整数去做，难度easy


```
class Solution {
public:
   bool isPalindrome(int x){
       //注意题目要求，负数不可以是回文数
        if (x < 0)
            return false;
        int oldValue = x,newValue = 0;
        int res = 0;
        while (x!=0)
        {
            newValue = res * 10 + x % 10;
            x = x / 10;
            //这里处理的是超出int范围的时候的处理
            if (newValue / 10 != res){
                return false;
                break;
            }

            res = newValue;
        }

        if (newValue == oldValue){
            return true;
        }
        else{
            return false;
        }
    }
};
```