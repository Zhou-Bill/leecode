# Median of Two Sorted Arrays

> There are two sorted arrays nums1 and nums2 of size m and n respectively.
> Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).

**题目意思就是两个已经排好序的数组，连起来找中位数** 
**题目难度：难，耗时128ms**

```
#include <iostream>
#include <vector>
using namespace std;


class Solution {
public:
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
        int length1 = nums1.size(), length2 = nums2.size(),i;
        double middle;
        if (length1 == 0 && length2 == 0){
            return 0;
        }
        if (length1 == 0){
            middle = length2 % 2 == 0 ? (nums2[length2 / 2 - 1] + nums2[length2 / 2]) / 2.0 : nums2[length2 / 2];
            return middle;
        }
        if (length2 == 0){
            middle = length1 % 2 == 0 ? (nums1[length1 / 2 - 1] + nums1[length1 / 2]) / 2.0 : nums1[length1 / 2];
            return middle;
        }
        vector<int> data(length1+length2);
        //data.push_back(1);
        
        //如果数组中最前的那个数大于另一个数组最后的那个数，那么就直接插入
        if (nums1[length1 - 1] < nums2[0]){
            for (i = 0; i < length2; i++)
                nums1.push_back(nums2[i]);
            middle = (length1 + length2) % 2 == 0 ? (nums1[(length1 + length2) / 2 - 1] + nums1[(length1 + length2) / 2]) / 2.0 : nums1[(length1 + length2) / 2];
            return middle;
        }
        if (nums1[0] > nums2[length2 - 1]){
            for (i = 0; i < length1; i++)
                nums2.push_back(nums1[i]);
            middle = (length1 + length2) % 2 == 0 ? (nums2[(length1 + length2) / 2 - 1] + nums2[(length1 + length2) / 2]) / 2.0 : nums2[(length1 + length2) / 2];
            return middle;
        }
        //最后一种情况
        data = insert(nums1, nums2, length1, length2);
        middle = (length1 + length2) % 2 == 0 ? (data[(length1 + length2) / 2 - 1] + data[(length1 + length2) / 2]) / 2.0 : data[(length1 + length2) / 2];
        
        return middle;
    }

    //直接插入排序
    vector<int> insert(vector<int> &num1, vector<int> &num2,int len1,int len2){
        vector<int> value(len1 + len2);
    
        
        int k = 0;
        for (k = 0; k < len1; k++){
            value[k] = num1[k];
        }
        
        
        for (k = 0; k < len2; k++){
            if (num2[k] < value[len1 - 1]){
                int temp = num2[k];
                int index = len1-1;
                while (temp < value[index])
                {
                    value[index+1] = value[index]; //元素后移
                    index--;
                }
                value[index + 1] = temp;
                len1++;
            }
            else{
                value[len1] = num2[k];
                len1++;
            }
        
        }
        return value;
    
    }
};

int main(){
    int array1[] = { 2,3,4,5};
    int array2[] = { 1};

    vector<int> arr1(array1, array1 + 4);
    vector<int> arr2(array2, array2 + 1);

    Solution solution;
    double mid = solution.findMedianSortedArrays(arr1, arr2);
    cout << mid;

}

```

* 简单说做这道题目分了6种情况，其中有两种思想是一样的

1. 就是两个都为空数组的时候，返回的是0
2. 当一个为空数组的时候，另一个不为空的时候，直接在不为空的数组找中位数
3. 当数组的尾比另一个数组的头，还要小的时候，两个数组直接连起来找中位数
4. 以上情况都不符合的时候，就用了直接插入排序，用排序后的数组找中位数

> 但是后来想前三个的情况也可以用第四种方法解决


----

> 这样的做法毫无意义

找到了两个[解释1](http://www.geeksforgeeks.org/median-of-two-sorted-arrays-of-different-sizes/),[解释2](https://discuss.leetcode.com/topic/16797/very-concise-o-log-min-m-n-iterative-solution-with-detailed-explanation) 不太好理解