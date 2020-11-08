# Arrays

+ [Max Consecutive Ones](#max-consecutive-ones)
+ [Reshape the Matrix](#reshape-the-matrix)
+ [Image Smoother](#image-smoother)
+ [Flipping an Image](#flipping-an-image)
+ [867. Transpose Matrix](#transpose-matrix)
+ [283. Move Zeroes](#move-zeroes)
+ [977. Squares of a Sorted Array](#squares-of-a-sorted-array)


## Max Consecutive Ones

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

## Reshape the Matrix

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

https://leetcode.com/problems/image-smoother/

Given a 2D integer matrix M representing the gray scale of an image, you need to design a smoother to make the gray 
scale of each cell becomes the average gray scale (rounding down) of all the 8 surrounding cells and itself. If a 
cell has less than 8 surrounding cells, then use as many as you can.

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

## 832. Flipping an Image

https://leetcode.com/problems/flipping-an-image/

Given a binary matrix A, we want to flip the image horizontally, then invert it, and return the resulting image.
To flip an image horizontally means that each row of the image is reversed.  For example, flipping [1, 1, 0] 
horizontally results in [0, 1, 1].
To invert an image means that each 0 is replaced by 1, and each 1 is replaced by 0. For example, inverting [0, 1, 1] results in [1, 0, 0]

Example 1:
```
Input: [[1,1,0],[1,0,1],[0,0,0]]
Output: [[1,0,0],[0,1,0],[1,1,1]]
Explanation: First reverse each row: [[0,1,1],[1,0,1],[0,0,0]].
Then, invert the image: [[1,0,0],[0,1,0],[1,1,1]]
```

```java
class Solution {
    public int[][] flipAndInvertImage(int[][] A) {
        int c = A[0].length;
        for (int[] row: A){
            for(int i = 0; i < (c + 1) / 2; ++i){
                int temp = row[i] ^ 1;
                row[i] = row[c - 1 - i] ^ 1;
                row[c - 1 - i] = temp;
            }
        }
        return A;
    }
}
```

## 867. Transpose Matrix
https://leetcode.com/problems/transpose-matrix/

Given a matrix A, return the transpose of A.
The transpose of a matrix is the matrix flipped over it's main diagonal, switching the row and column indices of the matrix.

Example 1:
```
Input: [[1,2,3],[4,5,6],[7,8,9]]
Output: [[1,4,7],[2,5,8],[3,6,9]]
```
Example 2:
```
Input: [[1,2,3],[4,5,6]]
Output: [[1,4],[2,5],[3,6]]
```
```
class Solution {
    public int[][] transpose(int[][] A) {
        int R = A.length, C = A[0].length;
        int[][] ans = new int[C][R];
        for (int r = 0; r< R; ++r){
            for(int c = 0; c < C; ++c){
                ans[c][r] = A[r][c];
            }
        }
        return ans;
    }
}
```
## 283. Move Zeroes
https://leetcode.com/problems/move-zeroes/

Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.
Example:
```
Input: [0,1,0,3,12]
Output: [1,3,12,0,0]
```
Note:
You must do this in-place without making a copy of the array.
Minimize the total number of operations.

```java
class Solution {
    public void moveZeroes(int[] nums) {
        int numberOfZeroes = 0;
        int currentPointer = 0;
        for(int i=0;i<=nums.length-1;i++){
            if(nums[i] == 0){
                numberOfZeroes++;
            }
        }
    
        for(int i=0;i<=nums.length-1;i++){
            if(nums[i] != 0){
                nums[currentPointer] = nums[i];
                currentPointer++;
            }
        }
    
        for(int i=currentPointer;i<=nums.length-1;i++){
            nums[i] = 0;
        }
    }
} 
```

## 977. Squares of a Sorted Array
Given an array of integers A sorted in non-decreasing order, return an array of the squares of each number, also in sorted non-decreasing order.

Example 1:
```
Input: [-4,-1,0,3,10]
Output: [0,1,9,16,100]
```
Example 2:
```
Input: [-7,-3,2,3,11]
Output: [4,9,9,49,121]
``` 
Note:

1 <= A.length <= 10000
-10000 <= A[i] <= 10000
A is sorted in non-decreasing order.

```java
class Solution {
    public int[] sortedSquares(int[] A) {
        int N = A.length;
        int[] ans = new int[N];
        for(int i = 0; i < N; ++i){
            ans[i]=A[i] * A[i];
        }
        Arrays.sort(ans);
        return ans;
    }
}
```



