## 合并两个有序数组
给你两个有序整数数组 nums1 和 nums2，请你将 nums2 合并到 nums1 中，使 nums1 成为一个有序数组。  
说明：  
初始化 nums1 和 nums2 的元素数量分别为 m 和 n 。
你可以假设 nums1 有足够的空间（空间大小大于或等于 m + n）来保存 nums2 中的元素。  
示例：  
```javascript
输入:
nums1 = [1,2,3,0,0,0], m = 3
nums2 = [2,5,6],       n = 3

输出: [1,2,2,3,5,6]
```

### 解题思路
概括来讲就是，从<font style="color: rgb(227,79,140);">nums1的后面开始插入合并后的数值</font>，即从nums1下标为m+n-1处开始填充。  
+ nums1、nums2有序，若把nums2全部插入到nums1中，则合并后的nums1长度为m+n，最后一个值的下标为m+n-1。   
+ 比较当前```nums1[len1-1]```和```nums2[len2-1]```的值，将大的那一个放到```nums1[len-1]```位置处。之后将大的那个值的数组长度变量和len各自减一，以便下一次取值比较。
+ 边界条件：
  - ```len1 < 0 && len2 >= 0```，此时nums1已经全部重新写入，仅剩还未合并完的nums2，将剩下的nums2挨个写入nums1即可。
  - ```len2 < 0```,nums2已经全部写入nums1，合并完成。
+ 时间复杂度： O(m+n)

### 代码实现
#### 解法一
```javascript
/**
 * @param {number[]} nums1
 * @param {number} m
 * @param {number[]} nums2
 * @param {number} n
 * @return {void} Do not return anything, modify nums1 in-place instead.
 */
var merge = function(nums1, m, nums2, n) {
    let len1 = m - 1,len2 = n - 1,len = m + n - 1
    while(len2 >= 0) {
        if(len1 < 0) {
            nums1[len--] = nums2[len2--]
            continue
        }
        nums1[len--] = nums1[len1] >= nums2[len2] ? nums1[len1--] : nums2[len2--]
    }
};
```

#### 解法二
```JavaScript
var merge = function(nums1, m, nums2, n) {
    let len = m + n
    m--
    n--
    while(len--) {
      // 完整流程写法
      if(n < 0 || nums1[m] > nums2[n]) {
          nums1[len] = nums1[m--]
      } else {
          nums1[len] = nums2[n--]
      }
      // 三目运算符简写
      // nums1[len] = (n < 0 || nums1[m] > nums2[n]) ? nums1[m--] : nums2[n--]
    }
};
```