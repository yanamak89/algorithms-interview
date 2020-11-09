+ [Reverse Integer](#reverse-integer)
+ [Palindrome Number](#palindrome-number)
+ [Fizz Buzz](#fizz-buzz)
+ [Base 7](#base-7)
+ [Fibonacci Number](#fibonacci-number)
+ [Largest Perimeter Triangle](#largest-perimeter-triangle)
+ [Sqrt(x)](#sqrtx)


## Reverse Integer

https://leetcode.com/problems/reverse-integer/

Given a 32-bit signed integer, reverse digits of an integer.

Note:
Assume we are dealing with an environment that could only store integers 
within the 32-bit signed integer range: [−231,  231 − 1]. For the purpose 
of this problem, assume that your function returns 0 when the reversed integer 
overflows.

Example 1:
```
Input: x = 123
Output: 321
```
Example 2:
```
Input: x = -123
Output: -321
```
Example 3:
```
Input: x = 120
Output: 21
```
Example 4:
```
Input: x = 0
Output: 0
```
Constraints:
-231 <= x <= 231 - 1

```java
class Solution {
    public int reverse(int x) {
        int rev = 0;
        while (x != 0){
            int pop = x % 10;
            x /= 10;
            if(rev > Integer.MAX_VALUE/10 || (rev == Integer.MAX_VALUE / 10 && pop > 7)) 
                return 0;
            if(rev < Integer.MIN_VALUE/10 || (rev == Integer.MIN_VALUE / 10 && pop < -8)) 
                return 0;
            rev = rev * 10 + pop;
        }
        return rev;
    }
}
```

## Palindrome Number

https://leetcode.com/problems/palindrome-number/

Determine whether an integer is a palindrome. An integer is a palindrome when it reads the same backward as forward.

Follow up: Could you solve it without converting the integer to a string?

 
Example 1:
```
Input: x = 121
Output: true
```
Example 2:
```
Input: x = -121
Output: false
Explanation: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.
```
Example 3:
```
Input: x = 10
Output: false
Explanation: Reads 01 from right to left. Therefore it is not a palindrome.

```
Example 4:
```
Input: x = -101
Output: false
```
Constraints:
```
-231 <= x <= 231 - 1
```

```java
class Solution {
    public boolean isPalindrome(int x) {
        if(x < 0){
            return false;
        }if(x< 10){
            return true;
        }if(x%10 == 0){
            return false;
        }
        int reversed = 0;
        int num = x;
        do{
            reversed = reversed * 10 + num % 10;
            num /= 10;
            if(reversed == num || reversed / 10 == num){
                return true;
            }
        }while(num > reversed);
        return false;
    }
}
```

## Fizz Buzz
Write a program that outputs the string representation of numbers from 1 to n.
But for multiples of three it should output “Fizz” instead of the number and for the multiples of five output “Buzz”. For numbers which are multiples of both three and five output “FizzBuzz”.

Example:
```
n = 15,

Return:
[
    "1",
    "2",
    "Fizz",
    "4",
    "Buzz",
    "Fizz",
    "7",
    "8",
    "Fizz",
    "Buzz",
    "11",
    "Fizz",
    "13",
    "14",
    "FizzBuzz"
]
```
```java
class Solution {
    public List<String> fizzBuzz(int n) {
         List<String> ans = new ArrayList<String>();

    for (int num = 1; num <= n; num++) {

      boolean divisibleBy3 = (num % 3 == 0);
      boolean divisibleBy5 = (num % 5 == 0);

      if (divisibleBy3 && divisibleBy5) {
        ans.add("FizzBuzz");
      } else if (divisibleBy3) {
        ans.add("Fizz");
      } else if (divisibleBy5) {
        ans.add("Buzz");
      } else {
        ans.add(Integer.toString(num));
      }
    }

    return ans;
  }
}
```

## Base 7
Given an integer, return its base 7 string representation.

Example 1:
```
Input: 100
Output: "202"
```
Example 2:
```
Input: -7
Output: "-10"
```
Note: The input will be in range of [-1e7, 1e7].
```java
class Solution {
    public String convertToBase7(int num) {
       return new String(Integer.toString(num,7));
    }
}
```
## Fibonacci Number

https://leetcode.com/problems/fibonacci-number/

The Fibonacci numbers, commonly denoted F(n) form a sequence, called the Fibonacci sequence, such that each number is the sum of the two preceding ones, starting from 0 and 1. That is,
```
F(0) = 0,   F(1) = 1
F(N) = F(N - 1) + F(N - 2), for N > 1.
```
Given N, calculate F(N).

Example 1:
```
Input: 2
Output: 1
Explanation: F(2) = F(1) + F(0) = 1 + 0 = 1.
```
Example 2:
```
Input: 3
Output: 2
Explanation: F(3) = F(2) + F(1) = 1 + 1 = 2.
```
Example 3:
```
Input: 4
Output: 3
Explanation: F(4) = F(3) + F(2) = 2 + 1 = 3.
```
Note:
0 ≤ N ≤ 30.

```java
class Solution {
    public int fib(int N) {
        if(N <= 1){
            return N;
        }
        return fib(N-1) + fib(N-2);
    }
}
```

## Largest Perimeter Triangle

https://leetcode.com/problems/largest-perimeter-triangle/

Given an array A of positive lengths, return the largest perimeter of a triangle with non-zero area, formed from 3 of these lengths.
If it is impossible to form any triangle of non-zero area, return 0.
```java
class Solution {
    public int largestPerimeter(int[] A) {
        Arrays.sort(A);
        for(int i = A.length -3; i >= 0; --i){
            if(A[i] + A[i+1] > A[i+2]){
                return A[i] + A[i+1] + A[i+2];
            }
        }
           return 0;
    }
}
```
## Sqrt(x)
Implement int sqrt(int x).
Compute and return the square root of x, where x is guaranteed to be a non-negative integer.
Since the return type is an integer, the decimal digits are truncated and only the integer part of the result is returned.

```java
class Solution {
    public int mySqrt(int x) {
        if(x<2){
            return x;
        }
        int left = (int)Math.pow(Math.E, 0.5 * Math.log(x));
        int right = left +1;
    return (long)right * right > x ? left : right; 
        
    }
}
```
