###Move Zeroes

>Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.

>For example, given nums = [0, 1, 0, 3, 12], after calling your function, nums should be [1, 3, 12, 0, 0].

>Note:

* You must do this in-place without making a copy of the array.
* Minimize the total number of operations.


```
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int length = nums.size(),i=0,index,n=0;
        //如果是0，那么后面元素前移
        while (n<length)
        {
            if (nums[i] == 0){
                index = i;
                while (index<length - 1)
                {
                    nums[index] = nums[index + 1];
                    index++;
                }
                nums[length - 1] = 0;
                n++;
            }
            else{
                i++;
                n++;
            }
        }
            
        
        for (i = 0; i < length; i++){
            cout << nums[i]<< " ";
        }
    }
};
```

# 官方答案

```
#include <iostream>
#include <algorithm>
#include <vector>
 
int main()
{
    std::vector<int> v{0, 0, 3, 0, 2, 4, 5, 0, 7};
    std::stable_partition(v.begin(), v.end(), [](int n){return n>0;});
    for (int n : v) {
        std::cout << n << ' ';
    }
    std::cout << '\n';
}
```

stable_partition() 将函数遍历该参数，数组保持相对位置不变