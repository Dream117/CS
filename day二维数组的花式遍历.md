#### [48. 旋转图像](https://leetcode-cn.com/problems/rotate-image/)

**解题思路**

把二维矩阵延左上角至右下角这条对角线，把左下部分和右上部分元素进行互换，然后把每一行的元素进行互换，就能达到整个二维矩阵顺时针旋转90°，如果是逆时针的话，就沿着右上角至左下角这条对角线进行元素互换，剩下的和顺时针一样。

**代码**

```java
class Solution {
    public void rotate(int[][] matrix) {
        int n=matrix.length;
// 先沿对角线反转二维矩阵
        for(int i=0;i<n;i++){
            for(int j=i;j<n;j++){
                int tmp=matrix[i][j];
                matrix[i][j]=matrix[j][i];
                matrix[j][i]=tmp;
            }
        }// 然后反转二维矩阵的每一行
        for(int[] row :matrix)reverse(row);
    } 
    // 反转一维数组
    public void reverse(int[] arr){
        int i=0,j=arr.length-1;
        while(j>i){
            int tmp=arr[i];
            arr[i]=arr[j];
            arr[j]=tmp;

            i++;
            j--;
        }
    }
}
```

