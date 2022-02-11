## 1.区域和和检索-数组不可变

https://leetcode-cn.com/problems/range-sum-query-immutable/

**解题思路**

看到这个题目，就联想到前缀合，前缀合就是[left,right]区间内所有元素相加之和，根据前缀合可以总结出两个公式，1.Si=a1+a2+...+ai    2.sum(L,R)=aL+(aL+1)+...+aR=（SR+1）-SL 前缀合数组的下标要从1开始，这点很关键。

![image-20220211210320767](C:\Users\WLW\Desktop\打卡\6.png)

**代码实现**

```java
class NumArray {
    // 定义前缀和数组
    private int[] preSum;
    public NumArray(int[] nums) {
        // preSum[0] = 0，便于计算累加和
        preSum = new int[nums.length + 1];
        // 计算 nums 的累加和 构造前缀和数组
        for (int i = 1; i < preSum.length; i++) {
            preSum[i] = preSum[i - 1] + nums[i - 1];
        }
    }
    /* 计算区间 [left, right] 元素的累加和 */
    public int sumRange(int left, int right) {
        return preSum[right + 1] - preSum[left];
    }
}

```

## 2.区域和和检索-数组不可变

https://leetcode-cn.com/problems/range-sum-query-2d-immutable/

**解题思路**

1.前缀合数组 s[i,j]如何计算？

2.(x1,y1),(x2,y2)这一个子矩阵中所有数的和该如何计算

![image-20220211220957092](C:\Users\WLW\Desktop\打卡\7.png)

根据图我可以得出:

* 1.`s[i,j]=s[i-1,j]-s[i,j-1]+s[i-1,j-1]+a[i,j];`
* 2.`s[x2+1][y2+1]-s[x2+1][y1]-s[x1][y2+1]+s[x1][y1];`

**代码实现**

```java
private int[][] s;

    public NumMatrix(int[][] matrix) {
        int m=matrix.length,n=matrix[0].length;
        if(m==0||n==0)return ;
        // 构造前缀和矩阵
        s=new int[m+1][n+1];
        for(int i=1;i<=m;i++){
            for(int j=1;j<=n;j++){
                //matrix数组下标是从零开始的
                s[i][j]= s[i-1][j]+s[i][j-1]-s[i-1][j-1]+matrix[i-1][j-1];
            }
        }
    }
    
    public int sumRegion(int x1, int y1, int x2, int y2) {
        // 目标矩阵之和由四个相邻矩阵运算获得
        return s[x2+1][y2+1]-s[x2+1][y1]-s[x1][y2+1]+s[x1][y1];
    }
```

​	