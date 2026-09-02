# Problem Explanation
The beauty of a string is the difference in frequencies between the most frequent and least frequent characters.
* For example, the beauty of "abaacc" is 3 - 1 = 2.
Given a string s, return the sum of beauty of all of its substrings.
Example :
```
Input: s = "aabcb"
Output: 5
Explanation: The substrings with non-zero beauty are ["aab","aabc","aabcb","abcb","bcb"], each with beauty equal to 1.
```
## Algorithm
* Loop over all the substrings.
* Prepare a hashmap for every substrings we come across.
* Find max and min frequency for every substrings.
* Then add this difference.
## Code
```
int beautySum(string s) {
        int n = s.length();
        int sum = 0;

        // Loop over all substrings
        for(int i=0; i<n; i++){
            unordered_map<char,int> freq;
            for(int j=i; j<n; j++){
                // Increase frequency of current character
                freq[s[j]]++;

                int maxi = INT_MIN;
                int mini = INT_MAX;

                // Find max and min frequency
                for(auto it : freq){
                    maxi = max(maxi,it.second);
                    mini = min(mini,it.second);
                }

                // Add the difference to sum
                sum += (maxi-mini);
            }
        }

        return sum;
    }
```
