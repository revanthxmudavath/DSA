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

# 3. 334. Increasing Triplet Subsequence - Medium

Given an integer array nums, return true if there exists a triple of indices (i, j, k) such that i < j < k and nums[i] < nums[j] < nums[k]. If no such indices exists, return false.

Example 1:

Input: nums = [1,2,3,4,5]
Output: true
Explanation: Any triplet where i < j < k is valid.

Approach - Greedy + Prefix Min tracking: Check if i is less than first if not check with second if not return true

```
class Solution:
    def increasingTriplet(self, nums: List[int]) -> bool:
        if len(nums) <= 2: return False

        first = float(inf)
        second = float(inf)

        for i in nums:

            if i <= first:
                first = i
            elif i <= second:
                second = i
            else:
                return True
        return False
```

# 4. 443. String Compression - medium

Given an array of characters chars, compress it using the following algorithm:

Begin with an empty string s. For each group of consecutive repeating characters in chars:

If the group's length is 1, append the character to s.
Otherwise, append the character followed by the group's length.
The compressed string s should not be returned separately, but instead, be stored in the input character array chars. Note that group lengths that are 10 or longer will be split into multiple characters in chars.

After you are done modifying the input array, return the new length of the array.

You must write an algorithm that uses only constant extra space.

Note: The characters in the array beyond the returned length do not matter and should be ignored.

Example 1:

Input: chars = ["a","a","b","b","c","c","c"]
Output: Return 6, and the first 6 characters of the input array should be: ["a","2","b","2","c","3"]
Explanation: The groups are "aa", "bb", and "ccc". This compresses to "a2b2c3".

Approach: Two pointers: Find the count of a char, take write pointer and append the char with their count. If their count if greater than 9, then divide it into two digits and append them.

```
def compress(self, chars: List[str]) -> int:
        if len(chars) == 1: return 1

        read = 0
        write = 0
        s = []

        while read < len(chars):
            c = chars[read]
            count = 0

            while read < len(chars) and c == chars[read]:
                count += 1
                read +=1 
            
            chars[write] = c
            write += 1
          

            if count > 1:
                for i in str(count):
                   chars[write] = i
                   write += 1
    
        return write
```

# 5. 283. Move Zeroes - Easy

Given an integer array nums, move all 0's to the end of it while maintaining the relative order of the non-zero elements.

Note that you must do this in-place without making a copy of the array.


Example 1:

Input: nums = [0,1,0,3,12]
Output: [1,3,12,0,0]

Approach: Two pointers, one to find none zero digit, if yes, swap with l and increment l

```
 l = 0

        for i in range(len(nums)):
            if nums[i] != 0:
                temp = nums[i]
                nums[i] = nums[l]
                nums[l] = temp
                l += 1
        
```

# 6. Longest Balanced Substring - I : medium

You are given a string s consisting of lowercase English letters.

A substring of s is called balanced if all distinct characters in the substring appear the same number of times.

Return the length of the longest balanced substring of s.

Example 1:

Input: s = "abbac"

Output: 4

Explanation:

The longest balanced substring is "abba" because both distinct characters 'a' and 'b' each appear exactly 2 times.

Approach: Hashmap: Iterate twice, i & j from 0 to n - 1, add the frequencies in the map, and check if the map is unique with balanced characters or not. If yes, attach the max length (j - i + 1) lest skip


```
public int longestBalanced(String s) {

        int maxL = 0;
        
        for(int i = 0; i<s.length();i++){
            int freq[] = new int[26];

            for(int j = i; j<s.length(); j++){

                int c = s.charAt(j) - 'a';

                freq[c]++;

                if(checkB(freq)) {
                    maxL = Math.max(maxL, j - i + 1);
                }
            }
        }

        return maxL;

    }

    private boolean checkB(int [] ans) {
        int common = 0;

        for(int i = 0; i<ans.length; i++){


            if( ans[i] == 0 ) continue;

            if ( common == 0) common = ans[i];


            else if ( ans[i] != common) return false;
        }

        return true;
    }

```

