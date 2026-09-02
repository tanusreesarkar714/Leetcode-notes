# Problem Explanation
Implement the myAtoi(string s) function, which converts a string to a 32-bit signed integer.
Example 1 :
```
Input: s = "1337c0d3"
Output: 1337
```
Example 2 :
```
Input: s = "0-1"
Output: 0
```
Example 3 :
```
Input: s = " -042"
Output: -42
```
## Algorithm
1. Remove leading white spaces
2. Check for sign in the string, before the no. starts, i.e. right after the spaces
3. Traverse until you find a non-digit character, and that is when you break out from the loop.
## Code
```
int myAtoi(string s) {
        if(s.size() == 0) return 0;
        int i = 0;
        // remove leading whitespaces
        while(i < s.size() && s[i] == ' '){
            i++;
        }
        s = s.substr(i);
        // handle sign
        int sign = 1;
        if(s[0] == '-') sign = -1;
        if(s[0] == '+'||s[0] == '-') i = 1;
        else i = 0;

        long long ans = 0;
        int MAX = INT_MAX, MIN = INT_MIN;

        while(i < s.size()){
            // if space or non-digit char, then break
            if(s[i] == ' '|| !isdigit(s[i])) break;

            ans = ans*10 + (s[i]-'0');
            if(sign == -1 && -1*ans < MIN) return MIN;
            if(sign == 1 && 1*ans > MAX) return MAX;
            i++;
        }
        return (int)(sign*ans);
    }
```
* **Time complexity** - O(n)
* **Space complexity** - O(1)
