1. 3637. Trionic Array I
  
You are given an integer array nums of length n.

An array is trionic if there exist indices 0 < p < q < n − 1 such that:

nums[0...p] is strictly increasing,
nums[p...q] is strictly decreasing,
nums[q...n − 1] is strictly increasing.
Return true if nums is trionic, otherwise return false.

Example 1:

Input: nums = [1,3,5,4,2,6]

Output: true

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
