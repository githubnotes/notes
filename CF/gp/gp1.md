# 序列型动态规划/楼梯问题
    - 512. Decode Ways

# merge
## merge lists
    - 156. Merge Intervals

# Subarray
Sum(i~j) = PrefixSum[j + 1] - PrefixSum[i]
## Winodw sum
    - 604. Window Sum
    - 642. Moving Average from Data Stream
## subarray
    - 41. Maximum Subarray
    - 138. Subarray Sum
    - 139. Subarray Sum Closest
# DFS
## subtree
    - 628. Maximum Subtree


# String
## Hash 字符/字符串统计类问题
    - 646. First Position Unique Character
    - Valid Anagram
    - 772. Group Anagrams
    - Find All Anagrams in a String
    - 384. Longest Substring Without Repeating Characters
    - 124. Longest Consecutive Sequence
    - 774. Repeated DNA
### Hash + Arr
    - 526. Load Balancer
## Palindrome
    - 627. Longest Palindrome
    - 415. Valid Palindrome
## two pointer String
    - 637. valid Word Abbreviation
    - 415. Valid Palindrome


# BFS类问题
- 二叉树上的宽搜 BFS in Binary Tree
- 图上的宽搜 BFS in Graph
   - 拓扑排序 Topological Sorting
- 棋盘上的宽搜 BFS

- When should use BFS?
- 图的遍历 Traversal in Graph
  - 层级遍历 Level Order Traversal
  - 由点及面 Connected Component
  - 拓扑排序 Topological Sorting
- 最短路径 Shortest Path in Simple Graph
  - 仅限简单图求最短路径 
    - (图中每条边，没有方向，没有权重)
## BFS in Binary Tree
    - Binary Tree Level Order Traversal
    - Serialize and Deserialize Binary Tree (1 more)
         - https://www.lintcode.com/help/binary-tree-representation/
    - Binary Tree Level Order Traversal II
    - Binary Tree Zigzag Order Traversal
    - Convert Binary Tree to Linked Lists by Depth
## BFS in graph (Undirected)
    - 433. Number of Islands
    - Knight Shortest Path (to-do)
    - Build Post Office II (to-do)
    - Clone graph
        - find all nodes
        - mapping old node to new node
        - conncet all edges (copy neighbors)
    - Graph Valid Tree
## Topological Sorting (Directed)
    - Topological Sorting
        - collect in-degree 找到所有的 indegree
        - put all nodes that indgree == 0 into queue
        - bfs
    - Course Schedule I && II (to-do)
    - Sequence Reconstruction (to-do)
## Minimum Spanning Tree (kruskal & Union Find Sets)
    - 589. Connecting Graph



# others
## Window Sum
    - 604. window sum
## list
    - copy copyRandomList
## sorting
    - High Five
    - Log Sorting
## others
    - K Closest
