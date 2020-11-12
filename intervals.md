+ [Non-overlapping Intervals](#non-overlapping-intervals)


## Non-overlapping Intervals

https://leetcode.com/problems/non-overlapping-intervals/

Given a collection of intervals, find the minimum number of intervals you need to remove to make the rest of the intervals non-overlapping.

```java
class Solution {
    class myComparator implements Comparator<int[]>{
        public int compare(int[] a, int[] b){
            return a[1] - b[1];
        }
    }
    
    public int eraseOverlapIntervals(int[][] intervals) {
        Arrays.sort(intervals, new myComparator());
        return erase_Overlap_Intervals(-1, 0, intervals);
    }
    
    public int erase_Overlap_Intervals(int prev, int curr, int[][] intervals){
        if(curr == intervals.length){
            return 0;
        }
        int taken = Integer.MAX_VALUE, nottaken;
        if(prev == -1 || intervals[prev][1] <= intervals[curr][0]){
            taken = erase_Overlap_Intervals(curr, curr + 1, intervals);
        }
        nottaken = erase_Overlap_Intervals(prev, curr + 1, intervals) + 1;
        return Math.min(taken, nottaken);
    }
}
```

