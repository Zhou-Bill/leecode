#Happy Number

> 尝试 从 2-9 中做测试。 如果不是happy number ，那么他循环就会有4，,16,37,58,85,20,145，这几个数，所以我们可以区域判定一下newValue 是否含有这几个数就行了，有的话，就不是Happy Number 。 难度Easy

```

#include <iostream>
#include <cmath>
using namespace std;

class Solution {
public:
    bool isHappy(int n) {
        int newValue = 0,  res = 0;

        if (n == 2 || n == 3)
            return false;
        int oldValue = n;
        
        while (res !=1)
        {
            newValue = 0;
            
            while (n != 0){
                newValue = newValue + pow(n % 10, 2);
                n = n / 10;
                
            }
            if (newValue == 1){
                return true;
            }
            res = newValue;
            n = res;
            if (res == 4 ||res==16 ||res==37 ||res==58 ||res==85 || res == 20 || res==42|| res == 145){
                return false;
            }
            
        }
        return false;
    }
};

int main(){
    Solution solution;
    bool result = solution.isHappy(9);
    cout << result;
}
```


> 但是以上对于我来说，毫无算法的意义，经查看discuss ,发现一个判断周期性的东西,用的c

```
int digitSquareSum(int n) {
    int sum = 0, tmp;
    while (n) {
        tmp = n % 10;
        sum += tmp * tmp;
        n /= 10;
    }
    return sum;
}

bool isHappy(int n) {
    int slow, fast;
    slow = fast = n;
    do {
        slow = digitSquareSum(slow);
        fast = digitSquareSum(fast);
        fast = digitSquareSum(fast);
    } while(slow != fast);
    if (slow == 1) return 1;
    else return 0;
}
```

* 比如 1，2 ，3，4, 1,2,3,4, 这样是1,2,3,4是一个周期，上面的解决办法就是 上面的一个周期对应的是两个周期，
* 即 1，对应另一个是1,2； 2的时候，对应的是3,4；如此类推，上面过了一个周期，下面即过了两个周期，那么等他周期头相等的时候，就退出循环