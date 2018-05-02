##Number of 1 Bits

>Write a function that takes an unsigned integer and returns the number of ’1' bits it has (also known as the Hamming weight).

>For example, the 32-bit integer ’11' has binary representation 00000000000000000000000000001011, so the function should return 3.

求出1的个数

```
#include<iostream>
#include <stdint.h>
using namespace std;

class Solution {
public:
    int hammingWeight(uint32_t n) {
        // 与1进行与运算，如果是的话count++，然后将n右移一位
        int count = 0 ;
        while (n){
            if (n & 1)
                count++;
            n = n >> 1;
        }
        return count;
    }
};

int main()
{
    uint32_t n = 11;
    Solution solution;
    solution.hammingWeight(n);
}

```

```
class Solution {
public:
    int hammingWeight(uint32_t n)
    {
        int res = 0;
        while (n)
        {
            n &= n - 1;
            ++res;
        }
        return res;
    }
};
```