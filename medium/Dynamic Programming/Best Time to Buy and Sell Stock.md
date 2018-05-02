##Best Time to Buy and Sell Stock


>Say you have an array for which the ith element is the price of a given stock on day i.

If you were only permitted to complete at most one transaction (ie, buy one and sell one share of the stock), design an algorithm to find the maximum profit.

> Example 1:
Input: [7, 1, 5, 3, 6, 4]
Output: 5

> max. difference = 6-1 = 5 (not 7-1 = 6, as selling price needs to be larger than buying price)
Example 2:
Input: [7, 6, 4, 3, 1]
Output: 0

>In this case, no transaction is done, i.e. max profit = 0.

数组中给定股价得到最大的收益

```
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int length = prices.size();
        int max = 0;
        //索引K 记录当前最小的那个数的下标
        int k = 0;
        for (int i = 1; i < length; i++)
        {
            if (prices[i] < prices[k]){
                max = max ==0?0:max;
                k = i;
            }
            else
            {
                max = prices[i] - prices[k] > max ? prices[i] - prices[k] : max;
            }
        }
        return max;
        
    }
};
```

* 比如 7,1,5,3,6,4
* 第一次k 是0，是7的索引，进入循环，如果i下标的值比k索引的值要小，那么把k下标指向i，并且把max置为0或者max
* 如果i下标的值比k索引的值要大，那么就两个相减，得到的结果保存下来，放入max
* 再判断一下max，如此类推

**注意** k一直是数组中最小单元的索引，比如 7,5,3,1,6, 4，1前面的那些都不需要考虑了,因为1前面那些都是在亏
