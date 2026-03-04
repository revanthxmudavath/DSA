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

# 7. 761. Special Binary String - Hard

Special binary strings are binary strings with the following two properties:

The number of 0's is equal to the number of 1's.
Every prefix of the binary string has at least as many 1's as 0's.
You are given a special binary string s.

A move consists of choosing two consecutive, non-empty, special substrings of s, and swapping them. Two strings are consecutive if the last character of the first string is exactly one index before the first character of the second string.

Return the lexicographically largest resulting string possible after applying the mentioned operations on the string.

Example 1:

Input: s = "11011000"
Output: "11100100"
Explanation: The strings "10" [occuring at s[1]] and "1100" [at s[3]] are swapped.
This is the lexicographically largest string possible after some number of swaps. 

Approach: Keep track of 1's and 0's until they balance out. If balanced, check the substrings from j+1 till i to find the balanced substrings recursively. Add them in List and sort in reverseorder before returning as a string

```
 public String makeLargestSpecial(String s) {
        if (s.length() == 0) return "";

        List<String> arr = new ArrayList<>();
        int count = 0; // track the balance between 1 and 0

        int i = 0;
        int j = 0;
        

        for(i = 0; i<s.length(); i++){

            count += (s.charAt(i) == '1') ? 1 : -1;

            if( count == 0) {
                String inner = makeLargestSpecial(s.substring(j + 1, i));

                String complete = "1" + inner + "0";

                arr.add(complete);
                
                j = i + 1;
            }
        }

        Collections.sort(arr, Collections.reverseOrder()); 
        // arr.sort(Comparator.reverseOrder());

        return String.join("", arr);
```

# 8 868. Binary Gap - Easy

Given a positive integer n, find and return the longest distance between any two adjacent 1's in the binary representation of n. If there are no two adjacent 1's, return 0.

Two 1's are adjacent if there are only 0's separating them (possibly no 0's). The distance between two 1's is the absolute difference between their bit positions. For example, the two 1's in "1001" have a distance of 3.


Example 1:

Input: n = 22
Output: 2

Explanation: 22 in binary is "10110".
The first adjacent pair of 1's is "10110" with a distance of 2.
The second adjacent pair of 1's is "10110" with a distance of 1.
The answer is the largest of these two distances, which is 2.
Note that "10110" is not a valid pair since there is a 1 separating the two 1's underlined.

```
public int binaryGap(int n) {
        int len = 0;

        String x = Integer.toBinaryString(n);
        

        int j = 0;
        for(int i = 0; i<x.length(); i++) {

            if( x.charAt(i) == '1') {
                len = Math.max(len, i - j );
                j = i;
            }

        }
        return len;

    }
```

# 9. 1022. Sum of Root To Leaf Binary Numbers - Easy 

You are given the root of a binary tree where each node has a value 0 or 1. Each root-to-leaf path represents a binary number starting with the most significant bit.
For example, if the path is 0 -> 1 -> 1 -> 0 -> 1, then this could represent 01101 in binary, which is 13.
For all leaves in the tree, consider the numbers represented by the path from the root to that leaf. Return the sum of these numbers.
The test cases are generated so that the answer fits in a 32-bits integer.

Example 1:

Input: root = [1,0,1,0,1,0,1]
Output: 22
Explanation: (100) + (101) + (110) + (111) = 4 + 5 + 6 + 7 = 22

Approach: Dfs algorithm + binary to int calculation

```
public int sumRootToLeaf(TreeNode root) {
        return dfs(root, 0);
    }

    private int dfs(TreeNode node, int sum) {
        if ( node == null) return 0;

        sum = (sum << 1) + node.val;

        if(node.left == null && node.right == null) return sum;

        return dfs(node.left, sum ) + dfs(node.right, sum);
    }

```

# 10. 1356. Sort Integers by The Number of 1 Bits - Easy

You are given an integer array arr. Sort the integers in the array in ascending order by the number of 1's in their binary representation and in case of two or more integers have the same number of 1's you have to sort them in ascending order.

Return the array after sorting it.
Example 1:

Input: arr = [0,1,2,3,4,5,6,7,8]
Output: [0,1,2,4,8,3,5,6,7]
Explantion: [0] is the only integer with 0 bits.
[1,2,4,8] all have 1 bit.
[3,5,6] have 2 bits.
[7] has 3 bits.
The sorted array by bits is [0,1,2,4,8,3,5,6,7]

Approach: TreeMap < integer, priorityqueue>, store the bit counts and its related numbers (they are automatically sorted). Then retrieve and store in an array with a moving index.

```
public int[] sortByBits(int[] arr) {

        TreeMap<Integer, PriorityQueue<Integer>> map = new TreeMap<>();

        for(int i : arr) {
            int bits = Integer.bitCount(i);
            map.putIfAbsent(bits, new PriorityQueue<>());
            map.get(bits).add(i);
        } 

        int [] nums = new int[arr.length];
        int idx = 0;

        for(int i : map.keySet()){
            PriorityQueue<Integer> pq = map.get(i);
            while(!pq.isEmpty()) nums[idx++] = pq.poll();
        }

        return nums;
        
    }
```

# 11. 1404. Number of Steps to Reduce a Number in Binary Representation to One - Medium

Given the binary representation of an integer as a string s, return the number of steps to reduce it to 1 under the following rules:

If the current number is even, you have to divide it by 2.
If the current number is odd, you have to add 1 to it.
It is guaranteed that you can always reach one for all test cases.

Example 1:

Input: s = "1101"
Output: 6
Explanation: "1101" corressponds to number 13 in their decimal representation.
Step 1) 13 is odd, add 1 and obtain 14. 
Step 2) 14 is even, divide by 2 and obtain 7.
Step 3) 7 is odd, add 1 and obtain 8.
Step 4) 8 is even, divide by 2 and obtain 4.  
Step 5) 4 is even, divide by 2 and obtain 2. 
Step 6) 2 is even, divide by 2 and obtain 1.  

Approach: Bit counting

```
public int numSteps(String s) {
        if(s.length() == 1 && s.charAt(0) == '1') return 0;
        int steps = 0;
        int carry = 0;

        for(int i = s.length() - 1; i> 0; i--) {
            int bit = s.charAt(i) - '0';

            if ( bit + carry == 1){
                steps += 2;
                carry = 1;
            }

            else {
                steps += 1;
            }
        }

        return steps + carry;

        }
```

# 12. 1689. Partitioning Into Minimum Number Of Deci-Binary Numbers - Easy

A decimal number is called deci-binary if each of its digits is either 0 or 1 without any leading zeros. For example, 101 and 1100 are deci-binary, while 112 and 3001 are not.

Given a string n that represents a positive decimal integer, return the minimum number of positive deci-binary numbers needed so that they sum up to n.

Example 1:

Input: n = "32"
Output: 3
Explanation: 10 + 11 + 11 = 32

Approach - Find the largest number

```
class Solution {
    public int minPartitions(String n) {
        int x = 0;
        for(char i : n.toCharArray()){
            int o = i - '0';
            x = Math.max(x, o);
        }
        return x;
    }
}
```


# 13. 1536. Minimum Swaps to Arrange a Binary Grid - Medium

Given an n x n binary grid, in one step you can choose two adjacent rows of the grid and swap them.

A grid is said to be valid if all the cells above the main diagonal are zeros.

Return the minimum number of steps needed to make the grid valid, or -1 if the grid cannot be valid.

The main diagonal of a grid is the diagonal that starts at cell (1, 1) and ends at cell (n, n).

Approach: Store the last ending zeroes in an array, for each row you need n - row - 1 -> 0's to satisfy the condition. We store them in an array. In another loop, check for each row, if you found the n - row - 1th row, calculate the steps required to swap and swap the rows. o(n^2)


```

public int minSwaps(int[][] grid) {
        
        int arr [] = new int[ grid.length];

        int n = grid.length;

        for(int i = 0; i<n;i++){
            int count = 0;
            int j = n - 1;

            while( j >= 0 && grid[i][j]==0){
                count++;
                j--;
            }

            arr[i] = count;
        }


        int steps = 0;

        for(int i = 0; i<n;i++){
            int need = n - i - 1;

            int j = i;

            while( j < n && arr[j] < need){
                j++;
            }

            if (j == n) return -1;

            steps += j - i;

            while ( j > i){
                swap(arr, j, j-1);
                j--;
            }
            
            
            }
            
            return steps;
               }

    private void swap(int [] arr, int x, int y){
        int temp = arr[x];
        arr[x] = arr[y];
        arr[y] = temp;

    }

```

# 14 1582. Special Positions in a Binary Matrix - Easy

Given an m x n binary matrix mat, return the number of special positions in mat.
A position (i, j) is called special if mat[i][j] == 1 and all other elements in row i and column j are 0 (rows and columns are 0-indexed).

```
public int numSpecial(int[][] matrix) {
        int n = matrix.length;
        int m = matrix[0].length;

        int count=0;
        int[] rowsum = new int[n];
        int[] colsum = new int[m];

        for(int i = 0; i < n; i++){
            for(int j = 0; j < m; j++){
                rowsum[i] += matrix[i][j];
                colsum[j] += matrix[i][j];
            }
        }

        for(int i = 0; i < n; i++){
            for(int j = 0; j < m; j++){
                if(matrix[i][j] == 1 && rowsum[i] == 1 && colsum[j] == 1){
                    count++;
                }
            }
        }

        return count;
    
    }
```
