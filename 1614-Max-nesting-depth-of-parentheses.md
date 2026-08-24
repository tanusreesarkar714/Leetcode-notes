# Problem Explanation
Given a **valid parentheses string** s, return the nesting depth of s.
Example : 
i/p : s = "(1 + (2 * 3) + ((8) / 4))"
o/p : 3 {for 8}

## Approach 1
*Parentheses -> Always think about STACK*

#### Intuition
* If ( then push into the stack, if ) the pop from the stack.
* And after each iteration update res, res = max(res,st.size())
* And then return the res.

#### Code
```
stack<char> st;
int result = 0;

for(char ch : s){
     if(ch == '('){
           st.push(ch);
     }
     else if(ch == ')'){
           st.pop();
     }

     result = max(result,(int)st.size());
}

return result;
```

**Time complexity**
O(n), because looping the string of n length

**Space complexity**
O(n), i.e. the space of the stack

## Approach 2
Now we obviously can't reduce the Time complexity, because we'll have to iterate the whole string. But what we can is, reduce the space complexity and use a variable, instead of a stack.

#### Intuition
* Take two variables, openBracket = 0, res = 0
* For ( openBrackets++, and for ) openBrackets--
* Update the res after each iteration, res = max(res,openBracket)

#### Code
```
        int openBrackets = 0;
        int res = 0;

        for(char ch : s){
            if(ch == '(') openBrackets++;
            else if(ch == ')') openBrackets--;

            res = max(res,openBrackets);
        }

        return res;
```

**Time complexity**
O(n)

**Space complexity**
O(1)
