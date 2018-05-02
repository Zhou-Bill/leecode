#Contains Duplicate

>Given an array of integers and an integer k, find out whether there are two distinct indices i and j in the array such that nums[i] = nums[j] and the difference between i and j is at most k.

题目说明 在小于等于k的数内找到相同的值，则为true

```
#include<iostream>
#include<vector>
#include<set>
using namespace std;

class Solution {
public:
    bool containsNearbyDuplicate(vector<int>& nums, int k) {
        int length = nums.size();
        // 首先先判断一下数组是否有重复,解决超时
        set<int> myset;

        for (int i = 0; i < length; i++){
            myset.insert(nums[i]);
        }
        if (myset.size() == length)
            return false;
        
        for (int i = 0; i < length; i++){
            int min = 0;
            for (int j = i + 1; j <length; j++){
                if (min>k)
                    break;
                min++;
                if (nums[i] == nums[j]){
                    return true;
                }
            }
        }
        return false;
    }
    
};

int main() {
    vector<int> array = {99,99};
    Solution solution;
    cout<<solution.containsNearbyDuplicate(array,2);
}

```

* 首先先用set去判定一下数组是否有重复值，如果没，那么直接返回false
* 有就继续往下判断