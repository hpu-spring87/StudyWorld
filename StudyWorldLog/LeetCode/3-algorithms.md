# 3. Longest Substring Without Repeating Characters

## 问题描述

> Given a string, find the length of the longest substring without repeating characters.

**Example:**

```
Given "abcabcbb", the answer is "abc", which the length is 3.

Given "bbbbb", the answer is "b", with the length of 1.

Given "pwwkew", the answer is "wke", with the length of 3. Note that the answer must be a substring, "pwke" is a subsequence and not a substring.

```
## 代码实现

**常规暴力实现方式**

```
package me.chunsheng.leetcode;

/**
 * Created by wei_spring on 2017/8/4.
 * <p>
 * Given "abcabcbb", the answer is "abc", which the length is 3.
 * <p>
 * Given "bbbbb", the answer is "b", with the length of 1.
 * <p>
 * Given "pwwkew", the answer is "wke", with the length of 3. Note that the answer must be a substring, "pwke" is a subsequence and not a substring.
 */

public class Problems3 {

    public static void main(String[] args) {
        System.out.println("Test Result = [" + lengthOfString("pwwkew") + "]");
    }

    public static int lengthOfString(String s) {
        int[] map = new int[256];
        int i = 0, j = 0, count = 0;
        for (i = 0; i < s.length(); i++) {
            while (j < s.length() && map[s.charAt(j)] == 0) {
                map[s.charAt(j)] = 1;
                count = Math.max(count, j - i + 1);
                j++;
            }
            //遍历过的要清零,不然后面遇到跟这个一样字母就直接跳出了,
            //abssadfg,比如第二个a机会跳出循环
            map[s.charAt(i)] = 0;
        }
        return count;
    }

}


时间复杂度： O(n2)
空间复杂度： O(1)
```




