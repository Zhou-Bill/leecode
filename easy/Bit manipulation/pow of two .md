## Pos of two

> 该题判断n是否是2的幂数


```
class Solution {
public:
    bool isPowerOfTwo(int n) {
        return n > 0 && !(n&(n-1));
    }
};
```

其实很好理解，
8 1000
7 0111
与之后就是0  