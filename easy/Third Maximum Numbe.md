###Third Maximum Numbe

> Given a non-empty array of integers, return the third maximum number in this array. If it does not exist, return the maximum number. The time complexity must be in O(n).

给定一个非空数组，逆向排序，去除重复值，得到第三个数


```
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

class Solution {
public:
    int thirdMax(vector<int>& nums) {
        int length = nums.size(), max = nums[0], i, j;
        if (length < 3){
            for (i = 1; i < length; i++){
                if (max < nums[i])
                    max = nums[i];
            }
            return max;
        }

        sort(nums.rbegin(),nums.rend());
        vector<int> result;
        result.push_back(nums[0]);
        for (i = 1; i < length; i++){
            for (j = 0; j < result.size(); j++){
                if (nums[i] == result[j]){
                    break;
                }
            }
            if (j == result.size()){
                result.push_back(nums[i]);
            }
            if (result.size() == 3)
                break;
        }
        max = result[0];
        if (result.size() < 3){
            for (i = 1; i < result.size(); i++){
                if (max < result[i])
                    max = result[i];
            }
            return max;
        }
        return result[result.size() - 1];
    }

    
};

int main(){
    int array[] = { 1,1,2 };
    vector<int> value(array,array+3);
    Solution solution;
    int result = solution.thirdMax(value);
    cout << result;
}
```
 
> 我的做法是如果数组长度小于3，那么就返回数组的最大值，如果大于3，那么先排序，用到sort，然后再定义一个数组，遍历排序后的数组，如果排序后的数组的值在新定义的数组中没找到，那么说明没重复值，然后就把这个值放入到这个数组中，

假设原数组是 [1,3,2,5,5,3],那么排序后应该是[5,5,3,3,2,1],去重复后[5,3,2,1],
第三个值就是2

> 知识点 逆向排序 sort(nums.rbegin(),nums.rend()) ;降序


>

