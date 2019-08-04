# Binary Tree & Divide Conquer

## Time Complexity
In O(n) time, make n to be two n/2. What is time complexity? \
    T(n) = O(n) + 2 T(n/2)\
         = O(n) + 2 ( O(n/2) + 2 T(n/4))\ = 2 O(n) + 4 T(n/4)) = 3 O(n) + 8 T(n/ 8))\
         = ...\
         = 4 O(n) + 16 T(n/ 16))\
         = O(n log n) +  n O(1) \
         = O(n log n)

In O(1) time, make n to be n/2. What is time complexity? \
 T(n) = O(1) + 2 T(n/2)\
         = O(1) + 2 ( O(n/2) + 2 T(n/4)) = 2 O(1) + 4 T(n/4)) = 3 O(1) + 8 T(n/ 8))\
         = ...\
         = O(log n) +  n O(1) \
         = O(n)

## Traverse in Binary Tree
![Traverse in Binary Tree](./assets/traverseBinalyTree.png)

### Preorder  Root L R 
https://www.lintcode.com/problem/binary-tree-preorder-traversal/

```java
Version 0: Non-Recursion (Recommend)
/**
 * Definition for binary tree
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
public class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        Stack<TreeNode> stack = new Stack<TreeNode>();
        List<Integer> preorder = new ArrayList<Integer>();
        
        if (root == null) {
            return preorder;
        }
        
        stack.push(root);
        while (!stack.empty()) {
            TreeNode node = stack.pop();
            preorder.add(node.val);
            if (node.right != null) {
                stack.push(node.right);
            }
            if (node.left != null) {
                stack.push(node.left);
            }
        }
        
        return preorder;
    }
}

//Version 1: Traverse
public class Solution {
    public ArrayList<Integer> preorderTraversal(TreeNode root) {
        ArrayList<Integer> result = new ArrayList<Integer>();
        traverse(root, result);
        return result;
    }
    // 把root为跟的preorder加入result里面
    private void traverse(TreeNode root, ArrayList<Integer> result) {
        if (root == null) {
            return;
        }

        result.add(root.val);
        traverse(root.left, result);
        traverse(root.right, result);
    }
}

//Version 2: Divide & Conquer
public class Solution {
    public ArrayList<Integer> preorderTraversal(TreeNode root) {
        ArrayList<Integer> result = new ArrayList<Integer>();
        // null or leaf
        if (root == null) {
            return result;
        }

        // Divide
        ArrayList<Integer> left = preorderTraversal(root.left);
        ArrayList<Integer> right = preorderTraversal(root.right);

        // Conquer
        result.add(root.val);
        result.addAll(left);
        result.addAll(right);
        return result;
    }
}
```
### Inorder  L Root R
https://www.lintcode.com/en/problem/binary-tree-inorder-traversal/

```java
public class Solution {
    /**
     * @param root: The root of binary tree.
     * @return: Inorder in ArrayList which contains node values.
     */
    public ArrayList<Integer> inorderTraversal(TreeNode root) {
        Stack<TreeNode> stack = new Stack<>();
        ArrayList<Integer> result = new ArrayList<>();
        
        while (root != null) {
            stack.push(root);
            root = root.left;
        }
    
        while (!stack.isEmpty()) {
            TreeNode node = stack.peek();
            result.add(node.val);
            
            if (node.right == null) {
                node = stack.pop();
                while (!stack.isEmpty() && stack.peek().right == node) {
                    node = stack.pop();
                }
            } else {
                node = node.right;
                while (node != null) {
                    stack.push(node);
                    node = node.left;
                }
            }
        }
        return result;
    }
}
```
### Postorder  L R ROOT
https://www.lintcode.com/problem/binary-tree-postorder-traversal/
```java
//Recursive
public ArrayList<Integer> postorderTraversal(TreeNode root) {
    ArrayList<Integer> result = new ArrayList<Integer>();

    if (root == null) {
        return result;
    }

    result.addAll(postorderTraversal(root.left));
    result.addAll(postorderTraversal(root.right));
    result.add(root.val);

    return result;   
}

/*
                    1 
                /       \ 
               2          3 
             /   \       /  \ 
            4    5      6    7 
 
crur    pre    stack           result
1       null    12                   
2       1       124                  
4       2       124                  
4       4       12             4                  
2       4       125                              
5       2       125                              
5       5       12             45                  
2       5       12                               
2       2       1             452                 
1       2       13                              
3       1       136                              
6       3       136                              
6       6       13           4526                   
3       6       137                             
7       3       137                             
7       7       13           45267               
3       7       13                          
3       3       1            452673              
1       3                    4526731              
 */
public ArrayList<Integer> postorderTraversal(TreeNode root) {
    ArrayList<Integer> result = new ArrayList<Integer>();
    Stack<TreeNode> stack = new Stack<TreeNode>();
    TreeNode prev = null; // previously traversed node
    TreeNode curr = root;

    if (root == null) {
        return result;
    }

    stack.push(root);
    while (!stack.empty()) {
        curr = stack.peek();
        if (prev == null || prev.left == curr || prev.right == curr) { // traverse down the tree
            if (curr.left != null) {
                stack.push(curr.left);
            } else if (curr.right != null) {
                stack.push(curr.right);
            }
        } else if (curr.left == prev) { // traverse up the tree from the left
            if (curr.right != null) {
                stack.push(curr.right);
            }
        } else { // traverse up the tree from the right
            result.add(curr.val);
            stack.pop();
        }
        prev = curr;
    }

    return result;
}



/*
                    1 
                /       \ 
               2          3 
             /   \       /  \ 
            4    5      6    7 
 
pop     stackAfterPop     statckAftePush        result
1        null               3 2                    1
2        3                  3 5 4                1 2 
4        3 5                3 5                  1 2 4
5        3                  3                    1 2 4 5
3        null               7 6                  1 2 4 5 3
6        7                  7                    1 2 4 5 3 6
7        null               null                 1 2 4 5 3 6 7
 */
public class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        Stack<TreeNode> stack = new Stack<TreeNode>();
        List<Integer> preorder = new ArrayList<Integer>();
        
        if (root == null) { return preorder; }
        
        stack.push(root);
        while (!stack.empty()) {
            TreeNode node = stack.pop();
            preorder.add(node.val);
            if (node.right != null) {
                stack.push(node.right);
            }
            if (node.left != null) {
                stack.push(node.left);
            }
        }
        
        return preorder;
    }
}



public class Solution {
    /**
     * @param root: The root of binary tree.
     * @return: Inorder in ArrayList which contains node values.
     */
    public ArrayList<Integer> inorderTraversal(TreeNode root) {
        Stack<TreeNode> stack = new Stack<>();
        ArrayList<Integer> result = new ArrayList<>();
        
        while (root != null) {
            stack.push(root);
            root = root.left;
        }
    
        while (!stack.isEmpty()) {
            TreeNode node = stack.peek();
            result.add(node.val);
            
            if (node.right == null) {
                node = stack.pop();
                while (!stack.isEmpty() && stack.peek().right == node) {
                    node = stack.pop();
                }
            } else {
                node = node.right;
                while (node != null) {
                    stack.push(node);
                    node = node.left;
                }
            }
        }
        return result;
    }
}

public class Solution {
    /**
     * @param root: A Tree
     * @return: Level order a list of lists of integer
     */
    public List<List<Integer>> levelOrder(TreeNode root) {
        
        List resule = new ArrayList();
        // write your code here
        Queue<TreeNode> q =  new LinkedList<TreeNode>();
       
        if(root == null){
            return resule;
        }
        q.offer(root);
   
        while(!q.isEmpty()){
            ArrayList<Integer> level = new ArrayList<Integer>();
            
            int qSize = q.size();
            for(int i = 0; i <qSize; i++){
                TreeNode node = q.poll();
                level.add(node.val);
                if(node.left != null){
                    q.offer(node.left);
                }
                 if(node.right != null){
                    q.offer(node.right);
                }
            }
            resule.add(level);
        }
        return resule;
    }  
}
```
### Links of Questions
- Maximum Depth of Binary Tree [97]
[97]: https://www.lintcode.com/problem/maximum-depth-of-binary-tree/
- Binary Tree Paths [480]
[480]: https://www.lintcode.com/problem/binary-tree-paths/
- Minimum Subtree [596]
[596]: https://www.lintcode.com/problem/minimum-subtree/description
- binary-tree-level-order-traversal [69]
[69]: https://www.lintcode.com/problem/binary-tree-level-order-traversal/description
- binary-tree-level-order-traversal II [70]
https://www.lintcode.com/problem/binary-tree-level-order-traversal-ii/description

### Practice Questions & Solutions
- Maximum Depth of Binary Tree [97]
- Binary Tree Paths [480]
- Minimum Subtree [596]
- binary-tree-level-order-traversal [69]
- binary-tree-level-order-traversal II [70]

## DFS in Binary Tree
### Preorder /Inorder /Postorder
### Introduce Divide Conquer Alg
### Non-Recusion VS Traverse VS Divide Conquer
### Binary Search Tree
#### Insert/Remove/Find/Validate
