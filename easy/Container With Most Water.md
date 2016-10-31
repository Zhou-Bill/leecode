###Container With Most Water  

>Given n non-negative integers a1, a2, ..., an, where each represents a point at coordinate (i, ai). n vertical lines are drawn such that the two endpoints of line i is at (i, ai) and (i, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.

##### 简单说就是给定一组数组，这些数组包含的是高度，在这些高度中找出面积最大的

比如说 2,3,10,5,7,8,9，面积最大是36，两个点10,9
10和9，9较小，9为高，10跟9之间距离为4，所以9*4=36


```
#include <iostream>
#include <vector>
using namespace std;

class Solution {
public:
    int maxArea(vector<int>& height) {
        int length = height.size(), max = 0, i, j, area;
        if (length < 2)
            return 0;

        //以数组的值作为高度，下标作为宽，寻找最大值
        for (i = 0; i < length; i++){
            for (j = i + 1; j < length; j++){
                if (height[i]>height[j]){
                    area = height[j] * (j - i);
                }
                else{
                    area = height[i] * (j - i);
                }
                if (area>max)
                    max = area;
            }
        }
        return max;
    }
};

int main() {
    int array[] = { 2, 1, 3 };
    //cout << sizeof(array) / sizeof(array[0]) << endl;
    vector<int> value(array, array + sizeof(array) / sizeof(array[0]));

    Solution solution;
    int result = solution.maxArea(value);
    cout << result;
}
```