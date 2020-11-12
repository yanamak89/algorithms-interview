+ [Valid Anagram](#valid-anagram)
+ [Reverse String](#reverse-string)
+ [Reverse Vowels of a String](#reverse-vowels-of-a-string)
+ [Reverse Words in a String III](#reverse-words-in-a-string-iii)
+ [To Lower Case](#to-lower-case)

## Valid Anagram

https://leetcode.com/problems/valid-anagram/

Given two strings s and t , write a function to determine if t is an anagram of s.

```java
class Solution {
    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) {
            return false;
        }
        char[] str1 = s.toCharArray();
        char[] str2 = t.toCharArray();
        Arrays.sort(str1);
        Arrays.sort(str2);
        return Arrays.equals(str1, str2);
    }
}
```

## Reverse String

https://leetcode.com/problems/reverse-vowels-of-a-string/

Write a function that takes a string as input and reverse only the vowels of a string.

```java
class Solution {
    public String reverseVowels(String s) {
        if(s == null || s.length() == 0){
            return "";
        }
        Set<Character> vowels = new HashSet<>(Arrays.asList('a', 'A', 'e', 'E', 'i',
                                                           'I', 'o', 'O', 'u','U'));
        char arr[] = s.toCharArray();
        int start = 0, end = s.length() - 1;
        while(start < end){
            while(start < end && !vowels.contains(arr[start])){
                start++;
            }
            while(start < end && !vowels.contains(arr[end])){
                end--;
            }
            if(start < end){
                char c = arr[start];
                arr[start] = arr[end];
                arr[end] = c;
            }
            start++;
            end--;
        }
        return new String(arr);
    }
}
```


https://leetcode.com/problems/reverse-string/

Write a function that reverses a string. The input string is given as an array of characters char[].
Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.
You may assume all the characters consist of printable ascii characters.

```java
class Solution {
    public void helper(char[] s, int left, int right) {
        if(left >= right){
            return;
        }
        char tmp= s[left];
        s[left++] = s[right];
        s[right--] = tmp;
        helper(s, left, right);
    }
    
    public void reverseString(char[] s){
        helper(s, 0, s.length - 1);
    }
}
```

## Reverse Words in a String III

https://leetcode.com/problems/reverse-words-in-a-string-iii/

Given a string, you need to reverse the order of characters in each word within a sentence while still preserving whitespace and initial word order.

```java
class Solution {
    public String reverseWords(String s) {
        String words [] = s.split(" ");
        StringBuilder sb = new StringBuilder();
        for(String word: words){
            sb.append(new StringBuffer(word).reverse().toString() + " ");
        }
        return sb.toString().trim();
    }
}
```

## To Lower Case

https://leetcode.com/problems/to-lower-case/

Implement function ToLowerCase() that has a string parameter str, and returns the same string in lowercase.

```java 
class Solution {
    public String toLowerCase(String str) {
        return str.toLowerCase();
    }
}
```




