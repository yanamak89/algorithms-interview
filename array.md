# Arrays

+ [485. Max Consecutive Ones](#485-max-consecutive-ones)
+ [566. Reshape the Matrix](#566-reshape-the-matrix)
+ [661. Image Smoother](#661-image-smoother)


## 485. Max Consecutive Ones

https://leetcode.com/problems/max-consecutive-ones/

```java 
class Solution {
    public int findMaxConsecutiveOnes(int[] nums) {
        int count = 0;
        int maxCount = 0;
        for(int i = 0;i < nums.length; i++){
            if(nums[i] == 1){
                count+= 1;
            }else{
                maxCount = Math.max(maxCount, count);
                count = 0;
            }
        }
        return Math.max(maxCount, count);
    }
}

```

## 566. Reshape the Matrix

https://leetcode.com/problems/reshape-the-matrix/

```java
class Solution {
    public int[][] matrixReshape(int[][] nums, int r, int c) {
        int [][] newArray = new int[r][c];
        if(nums.length == 0 || r * c != nums.length * nums[0].length){
            return nums;
        }
        Queue<Integer> queue = new LinkedList();
        for(int i = 0; i < nums.length; i++){
            for(int j = 0; j < nums[0].length; j++){
                queue.add(nums[i][j]);
            }
        }
        for(int i = 0; i < r; i++){
            for(int j = 0; j < c; j++){
                newArray[i][j] = queue.remove();
            }
        }
        return newArray;
    }
}

```

## 661. Image Smoother

Given a 2D integer matrix M representing the gray scale of an image, you need to design a smoother to make the gray 
scale of each cell becomes the average gray scale (rounding down) of all the 8 surrounding cells and itself. If a 
cell has less than 8 surrounding cells, then use as many as you can.

https://leetcode.com/problems/image-smoother/

```java
class Solution {
    public int[][] imageSmoother(int[][] m) {
        int r = m.length;
        int c = m[0].length;
        
        for (int i = 0; i < r; ++i){
            for (int k = 0; k < c; ++k){
                int sum = 0;
                int count = 0;
                
                for (int ni = i -1; ni <= i + 1; ++ni){
                    for(int nk = k - 1; nk <= k + 1; ++nk){
                        if (0 <= ni && ni < r && 0 <= nk && nk < c) {
                            sum += m[ni][nk] & 255;
                            ++count;
                        }
                    }
                }
                m[i][k] += (sum / count) << 8;
            }
        }
        for(int i = 0; i < r; i++){
            for(int k = 0; k < c; ++k){
                m[i][k] >>= 8;
            }
        }
        return m;
    }
}
```




