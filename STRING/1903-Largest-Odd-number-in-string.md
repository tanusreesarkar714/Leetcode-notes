# Problem Explanation
You are given a string num, representing a large integer. Return the largest-valued odd integer (as a string) that is a non-empty substring of num, or an empty string "" if no odd integer exists.

```
Example 1:
Input: num = "52"
Output: "5"
Explanation: The only non-empty substrings are "5", "2", and "52". "5" is the only odd number.

Example 2:
Input: num = "4206"
Output: ""
Explanation: There are no odd numbers in "4206".

Example 3:
Input: num = "35427"
Output: "35427"
Explanation: "35427" is already an odd number.
```
## Algorithm
* First take a pointer j and iterate it from back to front and stop when you find a odd no. in the string.
* Next take a i pointer and point it to the first non-zero character.
* If the string is empty return "".
* Else return the string.
## Code
```
string largestOddNumber(string num) {
        int n = num.length();
        int j = -1;
        for(int i=n-1; i>=0; i--){
            if((num[i]-'0') % 2 == 1){
                j = i;
                break;
            }
        }
        if(j == -1) return "";
        int i = 0;
        while(i < n){
            if((num[i]-'0')!=0) break;
            i++;
        }
        return num.substr(i,j+1-i);
    }
```
* **Time complexity** - O(n)
* **Space complexity** - O(1)
