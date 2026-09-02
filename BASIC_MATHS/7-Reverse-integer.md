# Problem Explanation
Given a signed 32-bit integer x, return x with its digits reversed. If reversing x causes the value to go outside the signed 32-bit integer range, then return 0.

Assume the environment does not allow you to store 64-bit integers (signed or unsigned).

Example :
```
I/p : x = 123, O/p : 321
I/p : x = 120, O/p : 21
I/p : x = -123, O/p : -321
```
## Algorithm
* Initialize a variable to store the reverse no. as 0
* Loop while the original number is not equal to zero
* Extract the lastdigit by performing modulo 10.
* Before calculating for rev, we have to check the overflow condition, rev can't be more than INT_MAX and lesser than INT_MIN, cz tahole ota outside 32-bit integer range e chole jaabe. Erom hole return 0.
* We're doing this before rev because rev10 is more bigger than rev so has more chances of going out-of-bound, but first loop e rev is zero toh 2nd loop theke check korlei hobe.
* Multiply the reverse no. by 10 and then add the extracted lastdigit
* Remove the last digit from the original number using integer division by 10.
* Continue this process until the original number becomes 0.
* Return the reversed no.
## Code
```
int reverse(int x) {
        int rev = 0;
        while(x != 0){
            int lastdigit = x % 10;
            // Overflow condition
            if(rev > INT_MAX/10 || rev < INT_MIN/10){
                return 0;
            }
            rev = (rev*10) + lastdigit;
            x = x/10;
        }
        return rev;
    }
```
**Time complexity**
O(log₁₀N)

**Space complexity**
O(1)
