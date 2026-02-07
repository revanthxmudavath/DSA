# 1. 3637. Trionic Array I
  
You are given an integer array nums of length n.

An array is trionic if there exist indices 0 < p < q < n − 1 such that:

nums[0...p] is strictly increasing,
nums[p...q] is strictly decreasing,
nums[q...n − 1] is strictly increasing.
Return true if nums is trionic, otherwise return false.

Example 1:

Input: nums = [1,3,5,4,2,6]

Output: true
```
public boolean isTrionic(int[] nums) {
        if(nums.length <= 3) return false;
        int i = 0;
        while( i < nums.length - 1 && nums[i] < nums[i+1]) i++;
        if(i == 0 || i == nums.length - 1) return false;
        int n = nums.length;
        int peak = i;
        while( i < n - 1 && nums[i] > nums[i+1])i++;
        if(i == peak || i == n - 1) return false;
        while(i < n - 1){
        if (nums[i] >= nums[i+1]) return false;
            i++;
        }
        return true;
    }
```

# 2. 1653. Minimum Deletions to Make String Balanced - Medium
         
You are given a string s consisting only of characters 'a' and 'b'​​​​.

You can delete any number of characters in s to make s balanced. s is balanced if there is no pair of indices (i,j) such that i < j and s[i] = 'b' and s[j]= 'a'.

Return the minimum number of deletions needed to make s balanced.



Example 1:

Input: s = "aababbab"
Output: 2
Explanation: You can either:
Delete the characters at 0-indexed positions 2 and 6 ("aababbab" -> "aaabbb"), or
Delete the characters at 0-indexed positions 3 and 6 ("aababbab" -> "aabbbb").


Approach - Greedy : count the number of b's once we see an 'a', delete the b's we see after it and increase counter to store the deletions required to keep the string balanced.

```
class Solution:
    def minimumDeletions(self, s: str) -> int:
        res = 0
        b = 0
        for i in s:
            if i == 'b':
                b += 1
            elif b>0:
                res += 1
                b -= 1
        return res
```
