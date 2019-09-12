# Linked List
## Dummy Node
## High Frequency

- Reverse linked list
- Reverse Nodes in k-Group (1 more) (1 more) P0
- Partition List
- http://www.lintcode.com/en/problem/merge-two-sorted-lists/
- http://www.lintcode.com/en/problem/reverse-linked-list-ii/
- http://www.lintcode.com/en/problem/swap-two-nodes-in-linked-list/
- http://www.lintcode.com/en/problem/reorder-list/
- http://www.lintcode.com/en/problem/rotate-list/
- Copy List with Random Pointer (1 more) P0
- Listed List cycle
- http://www.lintcode.com/problem/convert-sorted-list-to-balanced-bst/


# Array
## Subarray
Sum(i~j) = PrefixSum[j + 1] - PrefixSum[i]
- Maximum Subarray (1 more)  P0
    -           -2 -2 -3  4 -1  2 1
    - sum:      -2 -4 -7 -3 -4 -1 2 1
    - max:      -2 -2 -2  4  4  5 6
    - minPrfix: -2 -2 -7 -7 -7 -7 -7
    - Sum(i~j) = PrefixSum[j + 1] - PrefixSum[i]


- Subarray Sum (1 more)  P0
    - prefixSum is same

- Subarray Sum Closest
    - Pair(prefixSum, index)
    - sort By prefixSum
    - find small difference to get index

## Soted array
- Merge Two Sorted Arrays
- Merge Sorted Array
    - 反过来 merge
- inetersection of two arrays

- 数组内积（点乘）
    - Example [1,3] · [2,4] = 1*2 + 3*4 = 14
    - Follow up: 两个数组都非常大，但是其中都包含很多0
    - Example [1,0,0,0,0 …, 0, 2, 0,…, 0, 3] · [0,…, 0, 4, 0,…, 0, 5]
    - Pair(value + index) 

    
- Median of two Sorted Arrays

- Median
    ```java
    public int median(int[] nums) {
        // write your code here
        
        // Please note: the `k` must be (nums.length + 1) / 2 - 1 in order to satisfy the requirement
        return partition(nums, 0, nums.length - 1, (nums.length + 1) / 2 - 1);
    }
    
    // Same to find kth smallest element in an array
    // Modified for the partition function of quicksort
    private int partition(int[] nums, int left, int right, int k) {
        if (left == right) {
            return nums[k];
        }
        
        int start = left;
        int end = right;
        int pivot = nums[(end - start) / 2 + start];
        while (start <= end) {
            while (nums[start] < pivot && start <= end) {
                start++;
            }
            while (nums[end] > pivot && start <= end) {
                end--;
            }
            if (start <= end) {
                int temp = nums[start];
                nums[start] = nums[end];
                nums[end] = temp;
                start++;
                end--;
            }
        }
                
        if (k <= end) {
            return partition(nums, left, end, k);
        } else if (k >= start) {
            return partition(nums, start, right, k);
        }
        
        return nums[k];
    }
    ```