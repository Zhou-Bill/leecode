##Climbing Stairs

> You are climbing a stair case. It takes n steps to reach to the top.

> Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?


```
#include<iostream>
using namespace std;


class Solution {
public:
    //  int climbStairs(int n) {
    //      // 递归，斐波拉契数列
    //      int i = 0,sum=0;
    //      if (n == 0 || n == 1){
    //          return 1;
    //      }
    //      else
    //      {
    //          return climbStairs(n - 1) + climbStairs(n - 2);
    //      }
    //  }
    int climbStairs(int n) {
        int i = 0, sum = 0, prev = 1, next = 1;
        for (i = 2; i <= n; i++){
            sum = prev + next;
            prev = next;
            next = sum;
        }
        return next;
    }
};

int main() {
    Solution solution;
    cout<<solution.climbStairs(43);
}
```

这道题很简单就是将前面两个数相加得到后面那个数，第一次我使用了递归，但是很遗憾，超时了，第二次用了两个变量去指定一下前和后 prev,和next，然后相加，然后后移

* 0 1 2 3 4 5 6
* 1 1 2 3 5 8 13

以上就是一些规律，也可以这样想，一个台阶的方法次数为1次，两个台阶的方法次数为2个。n个台阶的方法可以理解成上n-2个台阶，然后2步直接上最后一步；或者上n-1个台阶，再单独上一步。