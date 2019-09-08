# 栈 Stack
    - 应用

- Implement Queue by Two Stacks
    - if(s2.isEmpty()){
             moveS1toS2();
        }

- Implement Stack by Two Queues
    - 3 2 1 
    - 2 1 move to a Q
    - pop 3
    - move 1 to a q
    - pop 2

- Min Stack
    - two Stack 
        - one normal 
        - minVal, Math.min(number, minStack.peek()


- Iterator   
    - Flatten Nested List Iterator
    - Use two stack, one main stack, another one is temp stack, 
    - 主要考点是迭代，而不是一股脑的全部flatten to list
    - [1,[4,[6]]]
        - Main Stack
            - 1,[4,[6]]
        - pop 1 from main stack
        - pop [4,[6]] to temp stack
        - push 4[6] to main stack
        - pop 3 from main stack

- 哈希表 Hash
    - HashTable thead saft
    - hash map not thead saft
    - 原理
    - 应用
    - Subarray Sum
    - Copy List with Random Pointer
        - HashMap<RandomListNode, RandomListNode> map = new HashMap<RandomListNode, RandomListNode>();
        - avoid to init same node using hashMap
    - LRU Cache
        - Map,Node,tail,head
        - get()
            - Map.contains()
                - move the node to tail
        - set()
            - Map.contains()
                - move the node to tail
            - !Map.contains()
                - Map.size() < capacity
                    - add to Map
                    - add to node to tail
                - Map.size() == capacity
                    - remove tail item
                    - add to Map
                    - add to node to tail

- 堆 Heap
    - 原理：小视频
    - 应用：优先队列 Priority Queue
    - 替代品：TreeMap

    - Top k Largest Numbers
    - high five
    - k closest points

- TreeMap  (TODO)
    - Top K Frequent Words



