# Problem Explanation
Given an integer x, return true if x is a palindrome, and false otherwise.
Example:
```
I/p : 121, O/p : True (Bcz 121 reads the same as left to right and right to left)
I/p : -121, O/p : False
I/p : 10, O/p : False
```
## Algorithm
Just reverse the number and then match, if the reversed and the original numbers are equal then return true, else false.
## Code
```
bool isPalindrome(int x) {
        int num = x;
        int rev = 0;
        while(x > 0){
            int lastDigit = x % 10;
            // Overflow condition
            if(rev > INT_MAX/10 || rev < INT_MIN/10){
                return false;
            }
            rev = (rev * 10) + lastDigit;
            x = x/10;
        }
        return(num == rev);
    }
```
**Whenever 32-bit integer i.e. -231 <= x <= 231 - 1 is given, always use this overflow condition of INT_MIN & INT_MAX **

**Time complexity**
O(log₁₀ x)

**Space complexity**
O(1)
