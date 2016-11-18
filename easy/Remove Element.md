###Remove Element


```
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        int length = nums.size(),i=0,total=0;
        length = length - 1;
        for (int i = 0; i <=length; i++){
            if (nums[i] != val){
                nums[total++] = nums[i];
            }
            else
            {
                // 如果最后一个值还是等于val ，那么length继续减减
                while (nums[length] == val && length>=0)
                {
                    length--;
                    // 这里是防止length等于-1的时候 ,nums[length] 出错
                    if (length < 0)
                        break;
                } 
                // 接着上面那个，如果[3,3],我要删除3，那么length 已经是-1了, 就不继续下去了，至于length<i 也停止[4,5]，删除5 ，我现在剩余的数组小于你当前的index值，就直接删除
                if (length < 0 || length < i)
                    break;
                nums[total++] = nums[length--];
            }
        }
        return total;

    }
};
```


> 官方解答

```
public int removeElement(int[] nums, int val) {
    int i = 0;
    int n = nums.length;
    while (i < n) {
        if (nums[i] == val) {
            nums[i] = nums[n - 1];
            // reduce array size by one
            n--;
        } else {
            i++;
        }
    }
    return n;
}
```

* 相同的时候直接把最后一个放进去，然后数组不加，以[3,2,2,3] ，因为最后一个有可能与删除的元素一样，所以新数组长度不添加
* 不同的时候,就直接添加数组长度，i++