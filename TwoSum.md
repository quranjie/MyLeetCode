题目：
Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution.

Example:
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].

我的解题思路：
这道题我见过，是给定一个已排序的数组，再给定一个数，查找哪两个数之和与给定的数相等。当时要求的是时间复杂度为O(n).
我的思路是先将第一个数和最后一个数给定起始和终止位置，判断它们的和与给定值的大小关系，两头凑。

我写的算法如下：

```
public int[] twoSum(int[] nums, int target) {
    int start = 0, end = nums.length - 1;

    while (start <= nums.length - 1 && end >= 0) {
        if (nums[start] + nums[end] == target) {
            return new int[]{start, end};
        } else if (nums[start] + nums[end] > target) {
            end--;
        } else {
            start++;
        }
    }

    return new int[]{-1, -1};
}

```

标准答案是这样的：

给定一个整数数组，找到两个数，使得它们的和等于一个特定的目标数。
函数twoSum应返回两个数的索引（index），使它们加起来等于目标，其中索引1必须小于索引2。注意返回的答案（包括索引1和索引2 ）不是从零开始的。
可以假设每个输入有且仅有一个答案。
输入：数字 = {2,7,11,15}，目标 = 9
输出：索引1 = 1，索引2 = 2

分析：首先复制一份array，对其进行排序，找到符合条件的两个数，再在原数组里找到index。

```

public int[] twoSum(int[] numbers, int target) {  
    // Note: The Solution object is instantiated only once and is reused by each test case.  
    int[] num = numbers.clone();  
    Arrays.sort(num);  

    int length = numbers.length;  
    int left = 0;  
    int right = length - 1;  
    int sum = 0;  

    ArrayList<Integer> index = new ArrayList<Integer>();  

    while (left < right) {  
        sum = num[left] + num[right];  

        if (sum == target) {  
            for (int i = 0; i < length; ++i) {  
                if (numbers[i] == num[left]) {  
                    index.add(i + 1);  
                } else if (numbers[i] == num[right]) {  
                    index.add(i + 1);  
                }  
                if (index.size() == 2) {  
                    break;  
                }  
            }  
            break;  
        } else if (sum > target) {  
            --right;  
        } else {  
            ++left;  
        }  
    }  

    int[] result = new int[2];  

    result[0] = index.get(0);  
    result[1] = index.get(1);  

    return result;  
}  

```

我写的程序问题所在：
1、想当然的认为数组是排好序的，以后要注意先clone已知数组，再排序
2、while循环条件其实可以直接写成 start<end ，之前的考虑是左边和右边移动的跨度不一样，后来细分析是我考虑多了
3、标准答案没有考虑到找不到的情况

