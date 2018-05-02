##Intersection of Two Arrays II

>Given two arrays, write a function to compute their intersection.

>Example:
Given nums1 = [1, 2, 2, 1], nums2 = [2, 2], return [2, 2].

>Note:
Each element in the result should appear as many times as it shows in both arrays.
The result can be in any order.
Follow up:
What if the given array is already sorted? How would you optimize your algorithm?
What if nums1's size is small compared to nums2's size? Which algorithm is better?
What if elements of nums2 are stored on disk, and the memory is limited such that you cannot load all elements into the memory at once?
Subscribe to see which companies asked this question

题目要求去交集

```
#include<iostream>
#include<vector>
#include<map>
using namespace std;

class Solution {
public:
    vector<int> intersect(vector<int>& nums1, vector<int>& nums2) {
        map<int,int> temp;
        vector<int> result;

        for (int i = 0; i < nums1.size(); i++){
            temp[nums1[i]]++;
        }
        for (int j = 0; j < nums2.size(); j++){
            if (temp[nums2[j]] > 0){
                result.push_back(nums2[j]);
                temp[nums2[j]]--;
            }
        }
        return result;
    }
};

int main() {
    vector<int> data = { 1, 2, 2, 1 }, data2 = { 2, 2 };
    Solution solution;
    solution.intersect(data,data2);
}
```

>个人想法是用map的方法,将nums1 的元素有一个映射的关系 ,num1= [1,2,2,1],num2 = [2,2]

* 用map存就是 map[1] = 2 ,即元素值为1有2个元素，map[2] = 2 ,元素为2的个数有两个
* 在另一个数组中找到值为1的话，map[1]--,并且放入到vector中


```

class Solution {
public:
    vector<int> intersect(vector<int>& nums1, vector<int>& nums2) {
        sort(nums1.begin(), nums1.end());
        sort(nums2.begin(), nums2.end());
        vector<int> result;
        int length1 = nums1.size();
        int length2 = nums2.size();
        int j = 0, i = 0;
        while (j<length1 && i<length2)
        {
            if (nums1[j] == nums2[i]){
                result.push_back(nums1[j]);
                i++;
                j++;
            }
            else if (nums1[j] < nums2[i]){
                j++;
            }
            else
            {
                i++;
            }
        }
        return result;
    }
};
```

另一种解决方法就是先把两个数组排序好，然后对比，如果两个数组的值相等，那么就放到result中，如果不相等，比较小的那个数组的索引++
