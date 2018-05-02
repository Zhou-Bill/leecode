## Counting Bits

> Given a non negative integer number num. For every numbers i in the range 0 ≤ i ≤ num calculate the number of 1's in their binary representation and return them as an array.

>Example:
For num = 5 you should return [0,1,1,2,1,2].

>Follow up:

>It is very easy to come up with a solution with run time O(n*sizeof(integer)). But can you do it in linear time O(n) /possibly in a single pass?
Space complexity should be O(n).
Can you do it like a boss? Do it without using any builtin function like __builtin_popcount in c++ or in any other language.

题目的意思是输入一个数得到0 ~ num 之间的二进制数的1的个数


```
class Solution {
public:
    vector<int> countBits(int num) {
        vector<int> result(num+1,0);
        

    
        //cout << int(log10(5) / log10(2));

        /* 第一种
        int k = 0;
        for (int i = 1; i <= num; i++){
            if (fmod(log10(i) / log10(2), 1) == 0){
                k = 0;
                result.push_back(result[k] + 1);
                k++;
            }
            else{
                result.push_back(result[k]+1);
                k++;
            }
        }
        */
       
       //第二种 其实两种原理是一样的，只是
        for (int i = 1; i <= num; i++){
            // 这里的i&(i-1) 用来判断一下是不是2的幂数
            result[i] = result[i&(i - 1)] + 1;
        }
        

        return result;
    }
};
```

规律如下

| number  | bit    | 1的个数| i &(i-1) | i &(i-1)对应数字  |
|:-------:|:------:|:------:| :------- | :---------------: |
| 0       | 0000   | 0      |          |                   |  
| 1       | 0001   | 1      | 0000     | 0                 |
| 2       | 0010   | 1      | 0000     | 0                 |   
| 3       | 0011   | 2      | 0010     | 2                 |
| 4       | 0100   | 1      | 0000     | 0                 |
| 5       | 0101   | 1      | 0100     | 4                 |
| 6       | 0110   | 2      | 0100     | 4                 |
| 7       | 0111   | 3      | 0110     | 6                 |
| 8       | 1000   | 1      | 0000     | 0                 |
| 9       | 1001   | 2      | 1000     | 8                 |
| 10      | 1010   | 2      | 1000     | 8                 |
| 11      | 1011   | 3      | 1010     | 10                |
| 12      | 1100   | 2      | 1000     | 8                 |
| 13      | 1101   | 3      | 1100     | 12                |
| 14      | 1110   | 3      | 1100     | 12                |
| 15      | 1111   | 4      | 1110     | 14                |

可以看出
f(0) = 0
f(1) = f(0) + 1 // 这时候2是2的0 次幂
f(2) = f(0) + 1 // 这时候2是2的一次幂
f(3) = f(1) + 1 即 f(3) = f(0) + 1 + 1 
f(4) = f(0) + 1 // 这时候4是2的两次次幂
f(5) = f(1) + 1 
f(6) = f(2) + 1
f(7) = f(3) + 1 即 f(7) = f(0) + 1 + 1 + 1 = [f(6)+1] = f(0) + 1 + 1 +1 
f(8) = f(0) + 1 // 这时候8 是2的三次幂
f(9) = f(1) + 1
f(10) = f(2) + 1
f(11) = f(3) + 1
f(12) = f(4) + 1
f(13) = f(5) + 1
f(14) = f(6) + 1
f(15) = f(7) + 1


// 可以简化成第二种方法，通过i&(i-1) 判断一下当前i是不是2的幂次数,我们可以发现每个i值都是i&(i-1)对应的值加1，





