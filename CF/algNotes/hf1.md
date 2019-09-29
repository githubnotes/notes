
```java

/***
Valid Word Abbreviation
Input : s = "internationalization", abbr = "i12iz4n"
Output : true
*****************************************************

Merge Intervals
Example 1:
Input: [(1,3)]
Output: [(1,3)]
Example 2:
Input:  [(1,3),(2,6),(8,10),(15,18)]
Output: [(1,6),(8,10),(15,18)]

*****************************************************
Log Sorting
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



*****************************************************
Decode Ways
Input: "12"
Output: 2
Explanation: It could be decoded as AB (1 2) or L (12).
*/



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
```