``` java 
Character.isLetter(c) || Character.isDigit(c);
Character.toLowerCase(s.charAt(front)
Character.isUpperCase(chars[j])
Character.isDigit(abbr.charAt(j))
Integer.valueOf(abbr.substring(start, j));
String subString = s.substring(start, i + 1);
subString.append("#");
char chars[] = s.toCharArray();

Queue<Integer> myQ = new LinkedList<>();
Set<Integer> hash = new HashSet<>();
String[] arr = data.split(",");
Collections.reverse(result);

ListNode faker = new ListNode(0);
ListNode lastNode =  faker;
return faker.next;


Map<Integer, Set<Integer>> graph = initializeGraph(n, edges)
map.containsKey(neighbor)

PriorityQueue<Integer> minheap = new PriorityQueue<Integer>(k, new Comparator<Integer>() {
    public int compare(Integer o1, Integer o2) {
        return o1 - o2;
    }
});

Map<Integer, PriorityQueue<Integer>> hash = new HashMap<Integer, PriorityQueue<Integer>>();
Map.Entry<Integer, PriorityQueue<Integer>> entry : hash.entrySet()
PriorityQueue<Integer> pq = hash.get(r.id);
hash.getKey()
hash.getVlaue()



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

Public myComparer implements Comparator<String>{
    public int compare(String s1, String s2){
        int index1 = s1.indexOf(" ");
        int index2 = s2.indexOf(" ");
        String head1 = s1.substring(0, index1);
        String head2 = s2.substring(0, index2);
        String body1 = s1.substring(index1);
        String body2 = s2.substring(index2);

        if(body1.equal(body2)){
            return head1.compareTo(head2);
        }
        return body1.compareTo(body2);
    }
}
```