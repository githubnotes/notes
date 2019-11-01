![subset](./assets/kruskal.png)
```java

/*************Valid Word Abbreviation******************************

Input : s = "internationalization", abbr = "i12iz4n"
Output : true
********************Merge Intervals*********************************
Example 1:
Input: [(1,3)]
Output: [(1,3)]
Example 2:
Input:  [(1,3),(2,6),(8,10),(15,18)]
Output: [(1,6),(8,10),(15,18)]

***************Log Sorting**************************************
Input:  
    logs = [
        "zo4 4 7",
        "a100 Act zoo",
        "a1 9 2 3 1",
        "g9 act car"
    ]
Output: 
    [
        "a100 Act zoo",
        "g9 act car",
        "zo4 4 7",
        "a1 9 2 3 1"
    ]
Explanation: "Act zoo" < "act car", so the output is as above.


******************Decode Ways***********************************
Input: "12"
Output: 2
Explanation: It could be decoded as AB (1 2) or L (12).


******************Course Schedule I/II***********************************



******************High Five***********************************
There are two properties in the node student id and scores, to ensure that each student will have at least 5 points, find the average of 5 highest scores for each person.

Example
Example 1:

Input: 
[[1,91],[1,92],[2,93],[2,99],[2,98],[2,97],[1,60],[1,58],[2,100],[1,61]]
Output:
1: 72.40
2: 97.40



******************612. K Closest Points***********************************
Given some points and an origin point in two-dimensional space, find k points which are nearest to the origin.
Return these points sorted by distance, if they are same in distance, sorted by the x-axis, and if they are same in the x-axis, sorted by y-axis.

Example
Example 1:

Input: points = [[4,6],[4,7],[4,4],[2,5],[1,1]], origin = [0, 0], k = 3 
Output: [[1,1],[2,5],[4,4]]

******************Copy List with Random Pointer***********************************
1: Map
2: 1 -> 1` -> 2 -> 2`

******************cloneTree***********************************

******************Minimum Spanning Tree***********************************

*/



public class Solution {
    /**
     * @param points a list of points
     * @param origin a point
     * @param k an integer
     * @return the k closest points
     */
    private Point global_origin = null;
    public Point[] kClosest(Point[] points, Point origin, int k) {
        // Write your code here
        global_origin = origin;
        PriorityQueue<Point> pq = new PriorityQueue<Point> (k, new Comparator<Point> () {
            @Override
            public int compare(Point a, Point b) {
                int diff = getDistance(b, global_origin) - getDistance(a, global_origin);
                if (diff == 0)
                    diff = b.x - a.x;
                if (diff == 0)
                    diff = b.y - a.y;
                return diff;
            }
        });

        for (int i = 0; i < points.length; i++) {
            pq.offer(points[i]);
            if (pq.size() > k)
                pq.poll();
        }
        
        k = pq.size();
        Point[] ret = new Point[k];  
        while (!pq.isEmpty())
            ret[--k] = pq.poll();
        return ret;
    }
    
    private int getDistance(Point a, Point b) {
        return (a.x - b.x) * (a.x - b.x) + (a.y - b.y) * (a.y - b.y);
    }
}

//Course Schedule

 public Map<Integer, Double> highFive(Record[] results) {
        // Write your code here
     
        Map<Integer, PriorityQueue<Integer>> hash = new HashMap<Integer, PriorityQueue<Integer>>();
        Map<Integer,Double> answer = new HashMap<>();
    
        for(Record record : results){
            if(!hash.containsKey(record.id)){
                 PriorityQueue<Integer> pq = new PriorityQueue<>();
          
                hash.put(record.id,pq);
            }
                
                PriorityQueue<Integer> pq = hash.get(record.id);
                if(pq.size() < 5){
                    pq.add(record.score);
                }else{
                    if(pq.peek() < record.score){
                       pq.poll();
                        pq.add(record.score);
                    }
                }
        }
        
        for (Map.Entry<Integer, PriorityQueue<Integer>> entry : hash.entrySet()) {
            int id = entry.getKey();
            PriorityQueue<Integer> scores = entry.getValue();
            double average = 0;
            for (int i = 0; i < 5; ++i)
                average += scores.poll();
            average /= 5.0;
            answer.put(id, average);
        }
        return answer;
}


public class Solution {
    /*
     * @param numCourses: a total of n courses
     * @param prerequisites: a list of prerequisite pairs
     * @return: true if can finish all courses or false
     */
    public int[] findOrder(int numCourses, int[][] prerequisites) {
        // write your code here
        
        HashMap<Integer, List<Integer>> graph = mapping(numCourses, prerequisites);
        
        Map<Integer, Integer> indegreeMap = inDegree(numCourses,graph);
         
        Queue<Integer> myQ= new LinkedList<>();
        int re[] =  new int[numCourses];    
        int count = numCourses -1;
        
         for(int i = 0; i < numCourses; i++){
             if(!indegreeMap.containsKey(i)){
                 myQ.offer(i);
                 re[count--] = i;
                 }
         }
         
        while(!myQ.isEmpty()){
          
          Integer temp = myQ.poll();
          for(Integer item: graph.get(temp)){
              indegreeMap.put(item, indegreeMap.get(item) -1);
              
              if( indegreeMap.get(item) == 0){
                   myQ.offer(item);
                  re[count--] = item;
              }
          }
          
        }
        
        if(count != -1){
            return new int[0];
        }
      
        return re;
        
    }
    
     private Map<Integer,Integer> inDegree (int numCourses, HashMap<Integer, List<Integer>> courseMap){
    
         HashMap<Integer, Integer> indegreeMap = new HashMap<>();
         
        for (int i = 0; i < numCourses; i++) {
            for (Integer neighbor : courseMap.get(i)) {
                if (indegreeMap.containsKey(neighbor)) {
                    indegreeMap.put(neighbor, indegreeMap.get(neighbor) + 1);
                } else {
                    indegreeMap.put(neighbor, 1);
                }
            }
        }
        
        return indegreeMap;
    } 
    
    
    
    private HashMap<Integer, List<Integer>> mapping(int numCourses, int[][] prerequisites){
        
        HashMap<Integer, List<Integer>> map = new HashMap<>();
        for (int i = 0; i < numCourses; i++) {
            map.put(i, new ArrayList<>());
        }
        for (int i = 0; i < prerequisites.length; i++) {
            int cur = prerequisites[i][0];
            int pre = prerequisites[i][1];
            map.get(cur).add(pre);
        }
        return map;
    } 
}


public class Solution {
    /**
     * @param logs: the logs
     * @return: the log after sorting
     */
     
    class MyCompartor implements Comparator<String> {
        public int compare(String s1, String s2){
            int t1 = s1.indexOf(' ');
            int t2 = s2.indexOf(' ');
            String id1 = s1.substring(0, t1);
            String id2 = s2.substring(0, t2);
            String body1 = s1.substring(t1);
            String body2 = s2.substring(t2);
            
            if(body1.equals(body2)){
                return id1.compareTo(id2);
            }else{
                return body1.compareTo(body2);
            }
        }
    }
    
    public String[] logSort(String[] logs) {
        // Write your code here
        
        int size = logs.length;
        int idx = size -1;
        String[] res = new String[size];
        
        List<String> logsStr = new LinkedList<>();
        
        for(int i = size -1; i >= 0 ; i--){
            
            int index =  logs[i].indexOf(" ");
            String temp = logs[i].substring(index);
             
            if(Character.isDigit(temp.charAt(1))){
             
                res[idx--] = logs[i];
            }else{
                logsStr.add(logs[i]);
            }
        }
        
        Collections.sort(logsStr, new MyCompartor());
        
        int i = 0;
        for(String item : logsStr){
            res[i++] = item;
        }

        return res;  
    }
}


/***
Decode Ways
*/

public class Solution {
    /**
     * @param s: a string,  encoded message
     * @return: an integer, the number of ways decoding
     */
    public int numDecodings(String s) {
        // write your code here
        
        if(s == null || s.length() == 0){
            return 0;
        }
        
        int l = s.length();
        if (l == 0) {
            return 0;   // only for this problem, but the ans should be 1
        }
        int[] f = new int[l + 1];
        f[0] = 1;
        
        char chars[] = s.toCharArray();
    
    
        for(int i = 1; i <= l; i++){
            
            if(chars[i - 1] != '0'){
                f[i] += f[i -1];
            }
            
            if(i >= 2){
                int val =  (chars[i - 2] - '0') * 10 + chars[i - 1] - '0';
                if(val >= 10 && val <= 26){
                    f[i] += f[i -2];
                }
            }
        }
        
        return f[l];
        
        
    }
}


public RandomListNode copyRandomList(RandomListNode head) {
        // write your code here
        
        Map<Integer, RandomListNode> map = new HashMap<>();
        
        
        RandomListNode faker = new RandomListNode(-1);
        RandomListNode cur = faker;
        
        while(head != null){
            
            RandomListNode newNode = null;
            if(!map.containsKey(head.label)){
                newNode = new RandomListNode(head.label);
                map.put(head.label, newNode);
            }
            
            newNode = map.get(head.label);
            cur.next = newNode;
            
            RandomListNode newRandomNode = null;
            if(head.random != null){
                if(!map.containsKey(head.random.label)){
                    newRandomNode = new RandomListNode(head.random.label);
                     map.put(head.random.label, newRandomNode);
                }
               newRandomNode = map.get(head.random.label);
            }
            
            cur.next.random =  newRandomNode;
           
           
           head = head.next;
           cur =  cur.next ;
        }
        
        return faker.next;
    }

     public TreeNode cloneTree(TreeNode root) {
        // write your code here
        if(root == null){
            return null;
        }
        TreeNode clone_root = new TreeNode(root.val);
    
        clone_root.left = cloneTree(root.left);
        clone_root.right = cloneTree(root.right);
        
        return clone_root;
        
    }

/**
 * Definition for undirected graph.
 * class UndirectedGraphNode {
 *     int label;
 *     ArrayList<UndirectedGraphNode> neighbors;
 *     UndirectedGraphNode(int x) { label = x; neighbors = new ArrayList<UndirectedGraphNode>(); }
 * };
 */
    public class Solution {
    /*
     * @param node: A undirected graph node
     * @return: A undirected graph node
     */
    public UndirectedGraphNode cloneGraph(UndirectedGraphNode node) {
        // write your code here
         if (node == null) {
            return node;
        }
        ArrayList<UndirectedGraphNode> mySet = getNodes(node);
        
        Map<UndirectedGraphNode, UndirectedGraphNode> graph = new HashMap<>();
        
        for(UndirectedGraphNode item: mySet){
            graph.put(item,new UndirectedGraphNode (item.label));
        }
        
        for(UndirectedGraphNode item: mySet){
            UndirectedGraphNode newNode = graph.get(item);
            
            for(UndirectedGraphNode nei: item.neighbors){
                newNode.neighbors.add(graph.get(nei));
            }
        }
        
       
        return graph.get(node);
       
    }
    
    private ArrayList<UndirectedGraphNode> getNodes(UndirectedGraphNode node) {
        Queue<UndirectedGraphNode> queue = new LinkedList<UndirectedGraphNode>();
        HashSet<UndirectedGraphNode> set = new HashSet<>();

        queue.offer(node);
        set.add(node);
        while (!queue.isEmpty()) {
            UndirectedGraphNode head = queue.poll();
            for (UndirectedGraphNode neighbor : head.neighbors) {
                if (!set.contains(neighbor)) {
                    set.add(neighbor);
                    queue.offer(neighbor);
                }
            }
        }

        return new ArrayList<UndirectedGraphNode>(set);
    }
}


/**
 * Definition for a Connection.
 * public class Connection {
 *   public String city1, city2;
 *   public int cost;
 *   public Connection(String city1, String city2, int cost) {
 *       this.city1 = city1;
 *       this.city2 = city2;
 *       this.cost = cost;
 *   }
 * }
 */
public class Solution {
    /**
     * @param connections given a list of connections include two cities and cost
     * @return a list of connections from results
     */
   
    public List<Connection> lowestCost(List<Connection> connections) {
        // Write your code here
        List<Connection> res = new ArrayList<Connection>();
        
        Collections.sort(connections, new Comparator<Connection>() {
            public int compare(Connection a, Connection b) {
                if (a.cost != b.cost) {
                    return a.cost - b.cost;
                }
                if (!a.city1.equals(b.city1)) {
                    return a.city1.compareTo(b.city1);
                }
                return a.city2.compareTo(b.city2);
            }
        });
        
        Map<String, String> father = new HashMap<>();
        for (Connection con : connections) {
            String root1 = find(con.city1, father), root2 = find(con.city2, father);
            System.out.println(root1 + "   " + root2);
            if (!root1.equals(root2)) {
                father.put(root1, root2);
                res.add(con);
            }
        }
        
        if (res.size() != father.size() - 1) {
            return new ArrayList<Connection>();
        }
        
        return res;
    }
    
    private String find(String str, Map<String, String> father) {
        if (!father.containsKey(str)) {
            father.put(str, str);
        } else if (!father.get(str).equals(str)) {
            father.put(str, find(father.get(str), father));
            System.out.println(str +  " + " + find(father.get(str), father));
        }
        
        return father.get(str);
    } 
    
}

Input
Show Difference
["Acity","Bcity",1]
["Acity","Ccity",2]
["Bcity","Ccity",3]
Your stdout
    Acity   Bcity
        Acity + Bcity
    Bcity   Ccity
        Bcity + Ccity
    Ccity   Ccity
Output
["Acity","Bcity",1]
["Acity","Ccity",2]
Expected
["Acity","Bcity",1]
["Acity","Ccity",2]



public class Solution {
    /**
     * @param word: a non-empty string
     * @param abbr: an abbreviation
     * @return: true if string matches with the given abbr or false
     */
    public boolean validWordAbbreviation(String word, String abbr) {
        
        if(word == null || abbr == null){
            return false;
        }
        // write your code here
        
        int i = 0;
        int j = 0;
        
        while(i < word.length && j < abbr.length){
            int moveIndex = 0;
            while(j < abbr.length && abbr.charAt(j).isDigit()){
                moveIndex = moveIndex * 10 + abbr.charAt(j) - '0';
                j++;
            }
            
            i += j;
            
            if(word.charAt(i) != word.charAt[j]){
                return false;
            }
            
            i++;
            j++;
        }
        
        
        return i == word.length && j == abbr.length;
        
    }
}

  while(i < word.length() && j < abbr.length()){
            if(abbr.charAt(j) == '0'){
                return false;
            }
        
            if(Character.isDigit(abbr.charAt(j))){
                
                int index = 0;
                while(j < abbr.length() && Character.isDigit(abbr.charAt(j))){
                    index = index * 10 + abbr.charAt(j) - '0';
                    j++;
                }   
                
                i += index;
            }else{
                if(word.charAt(i) != abbr.charAt(j)){
                    return false;
                }
          
                i++;
                j++;
            }
        }
        
        return i == word.length() && j == abbr.length();


          List<Interval> res = new LinkedList<>();
        
        if(intervals == null || intervals.size() == 0){
            return res;
        }
        
        intervals.sort(Comparator.comparing(i -> i.start));
        
        Interval last = null;
        
        
        for(Interval item : intervals){
           if(last  == null || last.end < item.start){
               res.add(item);
               last = item;
           }else{
               last.end = Math.max(item.end,last.end);
           }
            
        }
        
        return res;



public class Solution {
    /**
     * @param points a list of points
     * @param origin a point
     * @param k an integer
     * @return the k closest points
     */
    private Point global_origin = null;
    public Point[] kClosest(Point[] points, Point origin, int k) {
        // Write your code here
        global_origin = origin;
        PriorityQueue<Point> pq = new PriorityQueue<Point> (k, new Comparator<Point> () {
            @Override
            public int compare(Point a, Point b) {
                int diff = getDistance(b, global_origin) - getDistance(a, global_origin);
                if (diff == 0)
                    diff = b.x - a.x;
                if (diff == 0)
                    diff = b.y - a.y;
                return diff;
            }
        });

        for (int i = 0; i < points.length; i++) {
            pq.offer(points[i]);
            if (pq.size() > k)
                pq.poll();
        }
        
        k = pq.size();
        Point[] ret = new Point[k];  
        while (!pq.isEmpty())
            ret[--k] = pq.poll();
        return ret;
    }
    
    private int getDistance(Point a, Point b) {
        return (a.x - b.x) * (a.x - b.x) + (a.y - b.y) * (a.y - b.y);
    }
}

//Course Schedule


private Point global_origin = null;
    public Point[] kClosest(Point[] points, Point origin, int k) {
        // Write your code here
        global_origin = origin;
        PriorityQueue<Point> pq = new PriorityQueue<Point> (k, new Comparator<Point> () {
            @Override
            public int compare(Point a, Point b) {
                int diff = getDistance(b, global_origin) - getDistance(a, global_origin);
                if (diff == 0)
                    diff = b.x - a.x;
                if (diff == 0)
                    diff = b.y - a.y;
                return diff;
            }
        });


        PriorityQueue<Point> pq = new PriorityQueue<>(k, new Comparator<point> (){
            @Override
            public int compare(Point a, Point b){
                int diff = getDistance(b, global_origin) - getDistance(a, global_origin);

                if()
            }

        });

        for (int i = 0; i < points.length; i++) {
            pq.offer(points[i]);
            if (pq.size() > k)
                pq.poll();
        }
        
        k = pq.size();
        Point[] ret = new Point[k];  
        while (!pq.isEmpty())
            ret[--k] = pq.poll();
        return ret;
    }
    
    private int getDistance(Point a, Point b) {
        return (a.x - b.x) * (a.x - b.x) + (a.y - b.y) * (a.y - b.y);
    }



    public int[] findOrder(int numCourses, int[][] prerequisites) {
        // write your code here
        
        HashMap<Integer, List<Integer>> graph= mapping(numCourses, prerequisites);
        
         Map<Integer, Integer> indegreeMap = inDegree(numCourses,graph);
         
         Queue<Integer> myQ= new LinkedList<>();
        int re[] =  new int[numCourses];    
        int count = numCourses -1;
        
         for(int i = 0; i < numCourses; i++){
             if(!indegreeMap.containsKey(i)){
                 myQ.offer(i);
                 re[count--] = i;
                 }
         }
         
        while(!myQ.isEmpty()){
          
           Integer temp = myQ.poll();
          for(Integer item: graph.get(temp)){
              indegreeMap.put(item, indegreeMap.get(item) -1);
              
              if( indegreeMap.get(item) ==0 ){
                   myQ.offer(item);
                  re[count--] = item;
              }
          }
          
        }
        
        if(count != -1){
            return new int[0];
        }
      
        return re;
        
    }

    private HashMap<Integer, List<Integer>> mapping(int numCourses, int[][] prerequisites){
        
        HashMap<Integer, List<Integer>> map = new HashMap<>();
        for (int i = 0; i < numCourses; i++) {
            map.put(i, new ArrayList<>());
        }
        for (int i = 0; i < prerequisites.length; i++) {
            int cur = prerequisites[i][0];
            int pre = prerequisites[i][1];
            map.get(cur).add(pre);
        }
        return map;
    } 
```