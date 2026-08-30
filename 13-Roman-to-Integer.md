# Problem Explanation
Given a roman numeral, convert it to an integer.
Roman numerals are represented by seven different symbols: I, V, X, L, C, D and M.
```
Symbol       Value
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
```
Example 1 :
```
Input: s = "III"
Output: 3
Explanation: III = 3.
```
Example 2 :
```
Input: s = "MCMXCIV"
Output: 1994
Explanation: M = 1000, CM = 900, XC = 90 and IV = 4.
```
## Algorithm
* Start from the end.
* If a >= b, then add.
* If a < b, then subtract.
## Code
```
int romanToInt(string s) {
        // Map of roman numerals to their integer values
        unordered_map<char,int> roman = {
            {'I',1}, {'V',5}, {'X',10}, {'L',50}, {'C',100}, {'D',500}, {'M',1000} 
        };
        // res = the last digit,bcz that's the digit which we don't have to compare with
        int n = s.size();
        int res = roman[s[n-1]];
        // Iterate through the string
        for(int i = n-2; i>=0; i--){
            // subtract if current numeral is less than the next one
            if(roman[s[i]] < roman[s[i+1]]){
                res = res - roman[s[i]];
            }
            else{
                res = res + roman[s[i]];
            }
        }
        return res;
    }
```
* **Time complexity** - O(n) - single pass from right to left over the string
* **Space complexity** - O(1) - the roman map has a fixed 7 entries regardless of input size, so it doesn't grow with n. No other extra space used.
