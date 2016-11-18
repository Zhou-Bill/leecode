##Find All Numbers Disappeared in an Array

>Given an array of integers where 1 ≤ a[i] ≤ n (n = size of array), some elements appear twice and others appear once.

>Find all the elements of [1, n] inclusive that do not appear in this array.

>Could you do it without extra space and in O(n) runtime? You may assume the returned list does not count as extra space.

Example:

Input:
[4,3,2,7,8,2,3,1]

Output:
[5,6]

```
class Solution {
public:
    vector<int> findDisappearedNumbers(vector<int>& nums) {
        int length = nums.size();
        if(length<1) {
            return nums;
        }
        //首先我先用插入排序排序好并去除重复值
        int i, index, currentValue,n=length;
        for (i = 1; i < length; i++){
            if (nums[i] < nums[i - 1]){
                currentValue = nums[i];
                index = i - 1;
                //如果当前元素小于上一个元素，那么元素后移
                while (index>=0 &&currentValue < nums[index])
                {
                    nums[index + 1] = nums[index];
                    index--;

                }
                nums[index + 1] = currentValue;
            }
        }
        vector<int> b,a;
        b.push_back(nums[0]);
        //去重
        for (i = 1; i < length; i++){
            if (nums[i] != nums[i-1]){
                b.push_back(nums[i]);
            }
        }
        n = 0;
        for (i = 1; i <= length; i++){
            if (i != b[n]){
                a.push_back(i);
                
            }
            else{
                n++;
            }
        }

    
        return a;
    }
};
```

* 个人做法是先排序后去重，剩下的数组是[1,2,3,4,7,8]
* 然后跟i比，i的长度为原来数组的长度，如果i不在剩下的数组，则把他加到新的数组，然后数组下标不变，i++;