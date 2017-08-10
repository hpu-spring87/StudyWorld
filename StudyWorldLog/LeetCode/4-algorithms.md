#  4. Median of Two Sorted Arrays

## 问题描述

> There are two sorted arrays nums1 and nums2 of size m and n respectively.
  Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).

**Example:**

```
nums1 = [1, 3]
nums2 = [2]

The median is 2.0

nums1 = [1, 2]
nums2 = [3, 4]

The median is (2 + 3)/2 = 2.5

```
## 代码实现

**常规暴力实现方式**

```
package me.chunsheng.leetcode;

/**
 * Created by wei_spring on 2017/8/8.
 * <p>
 * nums1 = [1, 3]
 * nums2 = [2]
 * <p>
 * The median is 2.0
 * <p>
 * nums1 = [1, 2]
 * nums2 = [3, 4]
 * <p>
 * The median is (2 + 3)/2 = 2.5
 */
public class Problems4 {

    public static void main(String[] args) {

        findMedianSortedArrays(new int[]{1,2},new int[]{3,4});

    }

    public static double findMedianSortedArrays(int[] nums1, int[] nums2) {

        int lenght1 = nums1.length,length2 = nums2.length,lengthAll = nums1.length + nums2.length;
        int index1 = 0,index2 = 0,index3 = 0;
        int[] num3 = new int[lengthAll];
        while(index1 < lenght1 && index2 < length2){

            if(nums1[index1] < nums2[index2]){
                num3[index3++] = nums1[index1++];
            }else{
                num3[index3++] = nums2[index2++];
            }
        }
        while(index1 < lenght1){
            num3[index3++] = nums1[index1++];
        }
        while(index2 < length2){
            num3[index3++] = nums2[index2++];
        }
        int med1 = (num3.length-1)/2, med2 = num3.length /2;
        if(num3.length % 2 == 0){
            double media = (num3[med1] + num3[med2]) / 2.0;
            System.out.println("media1 = [" + media+ "]");
            return media;
        }else{
            double media = num3[med2];
            System.out.println("media2 = [" + media + "]");
            return media;
        }
    }
}

```




