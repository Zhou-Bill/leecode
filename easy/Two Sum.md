# Two Sum

```
#include <iostream>
#include <vector>
#include<algorithm>
using namespace std;

class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        vector<int> result;
        int flag,i,j,length = nums.size();
        for (i = 0; i < length; i++){
            for (j = i+1; j < length; j++){
                if (nums[i] + nums[j] == target){
                    result.push_back(i);
                    result.push_back(j);
                    return result;
                }
            }
        }
        
        return result;

    }
};

int main()
{
    Solution solution;
    int data[] = { 3, 2, 4 };
    vector<int> mydata(data, data + 3);
    vector<int> res = solution.twoSum(mydata,6);
    for (int i = 0; i < res.size(); i++){
        cout << res[i] << " ";
    }
}
```

> 题目简单，毫无解题技巧，就是一个一个去相加，以3，2,4 为例子

* 就是3 + 2 ，3+4 ，2+4 等不等于 target ，等于就把索引添加到数组中

> 我的另一个想法就是

* 先把数组排序
* 然后遍历数组，将target-数组值 ，在数组中找，如果他们的差在排序后的数组中小于的话就不需要继续往下找了
* 就比如 一开始数组 为 [2,11,7,3,15,6] ,target = 10, 那么排序后的数组为[2,3,6,7,11,15] ,从2开始，10-2=8，当8<11,遍历就停止了，
不需要再往下找
* 有个问题就是当排序之后，索引就发生了变化，返回索引就会出错，
* 所以有用到map

