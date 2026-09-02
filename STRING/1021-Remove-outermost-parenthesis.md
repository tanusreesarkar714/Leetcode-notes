# Problem Explanation
Remove the outermost parenthesis
Examples :
```
Input : s = "(()())(())" 
Output : "()()()" bcz (()()) and (()) are two different strings here which are concatenated

Input: s = "(()())(())(()(()))"
Output: "()()()()(())"

Input: s = "()()"
Output: ""

```
## Algorithm
### Brute force
**Stack-based approach**
* Initialize a empty stack and empty ans string.
* Traverse the whole string.
* If ch=='(' push it to the stack and if the stack is not empty then add it to the ans string. Bcz if the stack is empty, then it means it is the outermost parenthesis.
* If ch==')' pop from the stack i.e. it will pop one of the '(' from the stack.If the stack is not empty then add it to the ans string.
* Atlast return the ans string.
## Code
```
string removeOuterParentheses(string s) {
        stack<char> st;
        string ans = "";
        for(char ch : s){
            if(ch == '('){
                if(!st.empty()){
                    ans += ch;
                }
                st.push(ch);
            }
            else if(ch == ')'){
                st.pop();
                if(!st.empty()){
                    ans += ch;
                }
            }
        }
        return ans;
    }
```
**Time complexity** - O(n) bcz it is traversing the whole string
**Space complexity** - O(n) bcz we're taking a stack of n size
## Algorithm
### Optimised approach 
**Counter-based approach**
* Initialise a count variable and ans string.
* Traverse the whole string.
* If ch == '(', and if count!=0 then push it to the ans string and count++.
* If ch==')' then count-- and if count!=0 then push it to the ans string.
* Then return the ans variable.
* We check after ) and before ( because amra ( er belaye count++ korchi r ) er belaye count-- korchi.
```
string removeOuterParentheses(string s) {
        int count = 0;
        string ans = "";
        for(char ch : s){
            if(ch == ')') count--;
            if(count != 0) ans.push_back(ch);
            if(ch == '(') count++;
        }
        return ans;
    }
```
**Time complexity** - O(n)
**Space complexity** - O(1)
