# 1. Two Sum

## 问题描述

> Given an array of integers, return indices of the two numbers such that they add up to a specific target.
  You may assume that each input would have exactly one solution, and you may not use the same element twice.

**Example:**

```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```
## 代码实现

**常规暴力实现方式**

```
public class Problems1 {

    public static void main(String[] args) {
        int [] test = {2, 7, 11, 15};
        System.out.println(Arrays.toString(twoSum(test,9)));
    }

    public static int[] twoSum(int[] nums, int target) {
        for (int i = 0; i < nums.length; i++) {
            int first = nums[i];
            for (int j = i+1; j < nums.length; j++) {
                if(first + nums[j] == target){
                    int [] result = {i,j};
                    return result;
                }
            }
        }
       return null;
    }

}

时间复杂度： O(n2)
空间复杂度： O(1)
```

**散列表折中实现方式**

```
public class Problems1 {

    public static void main(String[] args) {
        int [] test = {2, 7, 11, 15};
        System.out.println(Arrays.toString(twoSum(test,9)));
    }

   public static int[] twoSum(int[] nums, int target) {
        HashMap<Integer,Integer> contain = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            contain.put(nums[i],i);
        }
        for (int i = 0; i < nums.length; i++) {
            int find = target - nums[i];
            if(contain.containsKey(find) && contain.get(find) != i){
                return new int[] {i,contain.get(find)};
            }
        }
        return null;
    }

}

时间复杂度： O(n)
空间复杂度： O(n)
```



