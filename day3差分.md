## 1.航班预订统计

https://leetcode-cn.com/problems/corporate-flight-bookings/

**解题思路**

构造一个差分数组`diff`，对`nums`数组一段闭合区间[i,j]+val值后，还原成原数组`nums`，如图线段长度为A,B我们让I,J这个区间同时加上一个val值,可以让I到B同时加上一个val值，J到B同时减去一个val，就能实现I,J这个区间加上一个val值了。

![image-20220212223513159](C:\Users\WLW\Desktop\打卡\8.png)

只要改变差分数组中i的值就能改变整个`nums`数组的值

![image-20220212224555354](C:\Users\WLW\Desktop\打卡\9.png)

**代码**

```java
class Solution {
    public int[] corpFlightBookings(int[][] bookings, int n) {
        // nums 初始化为全 0
        int[] nums = new int[n];
        // 构造差分解法
        Difference df = new Difference(nums);

        for (int[] booking : bookings) {
            // 注意转成数组索引要减一哦
            int i = booking[0] - 1;
            int j = booking[1] - 1;
            int val = booking[2];
            // 对区间 nums[i..j] 增加 val
            df.increment(i, j, val);
        }
        // 返回最终的结果数组
        return df.result();
    }

    class Difference {
        // 差分数组
        private int[] diff;

        public Difference(int[] nums) {
            assert nums.length > 0;
            diff = new int[nums.length];
            // 构造差分数组
            diff[0] = nums[0];
            for (int i = 1; i < nums.length; i++) {
                diff[i] = nums[i] - nums[i - 1];
            }
        }

        /* 给闭区间 [i,j] 增加 val（可以是负数）*/
        public void increment(int i, int j, int val) {
            diff[i] += val;
            if (j + 1 < diff.length) {
                diff[j + 1] -= val;
            }
        }

        public int[] result() {
            int[] res = new int[diff.length];
            // 根据差分数组构造结果数组
            res[0] = diff[0];
            for (int i = 1; i < diff.length; i++) {
                res[i] = res[i - 1] + diff[i];
            }
            return res;
        }
    }

}

```

