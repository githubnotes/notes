# Linked List
## Dummy Node
## High Frequency

- Reverse linked list
- Reverse Nodes in k-Group
    - reverse function 
        - Need: preN,startN, endN, endNextN
        - if endN == null return null
        - return startN (next round start.pre)
    - first round:
        - head -> n1 -> n2-> n3 -> n4-> null,  k = 2;
        - preN =  head ,startN = n1, endN = n2, endNextN = n3, reutrn n1
    - second round:
        - head -> n2 -> n1 -> n3 -> n4-> null,  k = 2;
        - preN =  n1 ,startN = n3, endN = n4, endNextN = null.
- Partition List
- http://www.lintcode.com/en/problem/merge-two-sorted-lists/
- http://www.lintcode.com/en/problem/reverse-linked-list-ii/
- http://www.lintcode.com/en/problem/swap-two-nodes-in-linked-list/
- http://www.lintcode.com/en/problem/reorder-list/
- http://www.lintcode.com/en/problem/rotate-list/
- Copy List with Random Pointer
- Listed List cycle
- http://www.lintcode.com/problem/convert-sorted-list-to-balanced-bst/
- http://www.lintcode.com/problem/delete-node-in-the-middle-of-singly-linked-list/
- http://www.lintcode.com/problem/convert-binary-search-tree-to-doubly-linked-list/



# Array
## Subarray
Sum(i~j) = PrefixSum[j + 1] - PrefixSum[i]
- Window Sum
    - [1,2,7,8,5] k = 3
    - 1 + 2 + 7 = 10
    - 1 + 2 + 7 - 1 + 9 = 2 + 7 + 8 = 17
    - 2 + 7+ 8 - 2 + 5 = 7+ 8 + 5 = 20
- Subarray Sum
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