
### 逆行整数

难度 easy

```
class Solution {
public:
    int reverse(int x) {
        int rev = 0, prev_num;
        while (x != 0){
            prev_num = rev * 10 + x % 10;
            x = x / 10;
            /* 对int 越界的操作，其实当逆向整数越界的时候，值会发生改变 ，例如 1000000003 ,理想状态下会变成3000000001，但已经超出了int的范围了，输出-1294967295，只是一个假设
            *  那么，我们的解决办法就是当已经 逆向的整数/10 是否等于他 之前没有乘10的数，如果等于，那么表示没有越界，不等于就表明越界了
            */
            if (prev_num / 10 != rev){
                rev = 0;
                break;
            }
            rev = prev_num;
        }
        return rev;
    }
};
```