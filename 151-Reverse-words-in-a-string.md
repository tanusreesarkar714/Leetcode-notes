# Problem Explanation
Given an input string s, reverse the order of the words.
Example :
```
Input: s = "the sky is blue"
Output: "blue is sky the"

Input: s = "  hello world  "
Output: "world hello"
Explanation: Your reversed string should not contain leading or trailing spaces.

Input: s = "a good   example"
Output: "example good a"
Explanation: You need to reduce multiple spaces between two words to a single space in the reversed string.
```
## Algorithm
### Brute force
* Reverse the whole string.
* Then reverse the individual words.
### Code
```
string reverseWords(string s) {
        int n = s.size();
        string ans = "";
        reverse(s.begin(),s.end());
        for(int i=0; i<s.size(); i++){
            string word = "";
            while(i < n && s[i]!=' '){
                word += s[i];
                i++;
            }
            reverse(word.begin(),word.end());
            if(word.length() > 0){
                ans += " " + word;
            }
        }
        return ans.substr(1);
    }
```
if(word.length() > 0) ei condition ta deowa hoyeche because the extra spaces will skip the while loop but w/o this condition it will add extra spaces bcz ans += " " + word;

**Time Complexity** - O(n)
**Space complexity** - O(1)

### Optimized approach
* Take two variables, end and i.
* After skipping extra spaces point one to the first letter of the string and one to the last.
* And then reverse.
### Code
```
string reverseWords(string s) {
        string ans = "";
        int i = s.size() - 1;
        while(i >= 0){
            while(i >= 0 && s[i] == ' '){//skipping spaces
                i--;
            }
            if(i < 0) break;
            int end = i;
            while(i >= 0 && s[i] != ' '){
                i--;
            }
            string word = s.substr(i+1,end-i);
            if(! ans.empty()){
                ans += " ";
            }
            ans += word;
        }
        return ans;
    }
```
**Time Complexity** - O(n)
**Space Complexity** - O(1)
