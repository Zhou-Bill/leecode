##Rotate Function

```
#include <iostream>
#include <vector>
using namespace std;

class Solution{
public :
    int maxRotateFunction(vector<int>& A) {
        int length = A.size(),i,maxnum=0,sum=0;
        for (i = 0; i < length; i++){
            sum = 0;
            for (int j = 0; j < length; j++){
                if (i + j >= length){
                    sum += A[i + j - length] * j;
                }else{
                    sum += A[i + j] * j;
                }
            }
            // 这里保证了只有一位数的时候 它就是最大值，并且当数组中都是负数时，第一位作为最大值进行后续比较
            if (i == 0){
                maxnum = sum;
            }

            if (sum >= maxnum){
                maxnum = sum;
            }
        }
        cout << maxnum;
        
        return maxnum;

    }
};
int main(){

    
    int array[] = { 4, 3, 2, 6 };
    //cout << sizeof(array) / sizeof(array[0])<<endl;
    vector<int> mydata(array,array+4);
    Solution solution;
    solution.maxRotateFunction(mydata);
}
```

> 想法就是 ，比如上面{4,3,2,6} 这个数组

| i \ j      | 0       | 1     | 2     | 3     |
| ---------- |:-------:| -----:| -----:| -----:|
| 0          | 0       | 1     | 2     |  3    |
| 1          | 1       | 2     | 3     |  0    |  
| 2          | 2       | 3     | 0     |  1    |
| 3          | 3       | 0     | 1     |  2    |

* 上面横向代表 j 的下标，竖向表示 i 的下标，从上面可以看出数组下标的变化是0,1,2,3，然后是1,2,3,0，如此类推
*  那么发现的规律就是 当 i+j > 数组长度时，就会变成 i+j-length 的绝对值，i+j< 数组长度时，下标就是i+j,所以的出
``` 
    if (i + j >= length){
            sum += A[i + j - length] * j;
    }else{
            sum += A[i + j] * j;
    }
```

* 但是 在提交时，数据达到2w 个，就超时了，但是答案正确，执行时间是1529ms
* 当数据达到2w的时候，时间复杂度是20000 * 20000


> 在discuss 上面看到一个比较有趣的算法

```
class Solution{
public :
    int maxRotateFunction(vector<int>& A) {
        int n = A.size(), sum = 0, tmp1 = 0, tmp2;
        int ans = 0;
        for (int i = 0; i < n; i++){
            sum += A[i];
            tmp1 += i * A[i];
        }
        ans = tmp1;
        for (int i = 1; i < n; i++){
            tmp2 = sum + tmp1 - n * A[n - i];
            ans = max(ans, tmp2);
            tmp1 = tmp2;
        }

        return ans;
    }
};
```

> 思路 , 以{ 4, 3, 2, 6 }为例子

```
 f(0) = 0A[0] + 1A[1] + 2A[2] + 3A[3]
 f(1) = 0A[3] + 1A[0] + 2A[1] + 3A[2]
 F(2) = 0A[2] + 1A[3] + 2A[0] + 3A[1]
 F(3) = 0A[1] + 1A[2] + 2A[3] + 3A[0]

 f(n-1) = 0A[1] + 1A[2] + 2A[3] + .... + (n-2)A[n-1]+(n-1)A[0]

f(1) - f(0) = (0-3)A[3] + A[0] + A[1] + A[2] 
            = (0-4)A[3] + A[0] + A[1] + A[2] + A[3]
            = SUM - (0-4)A[3]
SUM = A[0] + A[1] + A[2] + A[3]

f(n-1) - f(n-2) = SUM - nA[n-(n-1)]  
```

* 所以一开始我们先把所有值全部加起来得到sum，和f(0) 的值
* 在通过 f(1) - f(0) = sum - nA(n-1) 这样的公式把f(1),f(2) 这样的值一个一个的算出来，对比最大值


