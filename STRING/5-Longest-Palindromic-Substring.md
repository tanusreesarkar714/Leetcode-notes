# Problem Explanation
Given a string s, return the longest palindromic substring in s.
Example 1:
```
Input: s = "babad"
Output: "bab"
Explanation: "aba" is also a valid answer.
```
Example 2:
```
Input: s = "cbbd"
Output: "bb"
```
## Naive approach
### Algorithm
* First generate all the substrings.
* Then check if they are palindrome.
### Code
```
//do it with Dynamic Programming later, that has a better TC & SC
    bool ispalindrome(int i, int j, string &s){
        while(i <= j){
            if(s[i] == s[j]){
                i++;
                j--;
            }
            else return false;
        }
        return true;
    }

    string longestPalindrome(string s) {
        int maxlen = 0;
        int sp = -1;//starting point
        for(int i=0; i<s.size(); i++){
            for(int j=i; j<s.size(); j++){
                if(ispalindrome(i, j, s) == true){
                    if(j - i + 1 > maxlen){
                        maxlen = j - i + 1;
                        sp = i;
                    }
                }
            }
        }

        return s.substr(sp,maxlen);

    }
```
* **Time Complexity** - O(n³)
* **Space Complexity** - O(1)
