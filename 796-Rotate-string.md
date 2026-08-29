# Problem Explanation
Given two strings s and goal, return true if and only if s can become goal after some number of shifts on s.

A shift on s consists of moving the leftmost character of s to the rightmost position.

For example, if s = "abcde", then it will be "bcdea" after one shift.

Example 1 :
```
Input: s = "abcde", goal = "cdeab"
Output: true
```
Example 2 :
```
Input: s = "abcde", goal = "abced"
Output: false
```
## Brute force
### Algorithm
* Check my notebook for algorithm
### Code
```
bool rotateString(string s, string goal) {
        string left = "";
        if(s.length() != goal.length()) return false;
        for(int i=0; i<s.length(); i++){
            string right = s.substr(i);
            if(goal == right + left) return true;
            left += s[i];
        }
        return false;
    }
```
* **Time Complexity** - O(n^2)
Each of the n iterations does substr (O(n)), builds right + left (O(n)), and compares to goal (O(n)). That's O(n) work × n iterations = O(n²).
* **Space Complexity** - O(n) * 2 which is almost equal to O(n).
## Optimized approach
### Algorithm
* Take a new variable, doubledS = s + s
* Find for goal in doubledS, if the find function doesnot return npos i.e. goal is been found in doubledS then return true.
* Else return false.
### Code
```
bool rotateString(string s, string goal) {
        if(s.length() != goal.length()) return false;
        string doubledS = s + s;
        if(doubledS.find(goal) != string::npos) return true;
        else return false;
    }
```
* **Time complexity** - O(n²) worst case , effectively O(n) on average/typical cases.
* **Space complexity** - O(n) for doubledS.
