## 题目描述

假设你有一个数组，其中第 i  个元素是股票在第  i  天的价格。
你有一次买入和卖出的机会。（只有买入了股票以后才能卖出）。请你设计一个算法来计算可以获得的最大收益。

### 示例1

输入

```
[1,4,2]
```

输出

```
3
```

### 示例2

输入

```
[2,4,1]
```

输出

```
2
```





## 二、解答

```java
/**
 * @Author GJXAIOU
 * @Date 2020/9/10 10:35
 */
public class NC7 {

    public int maxProfit(int[] prices) {
        if (prices == null || prices.length == 0) {
            return 0;
        }

        int min = prices[0];
        int res = 0;
        for (int i = 1; i < prices.length; i++) {
            min = Math.min(prices[i], min);
            res = Math.max(prices[i] - min, res);
        }
        return res;
    }
}
```

