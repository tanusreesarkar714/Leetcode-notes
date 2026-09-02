# Problem Explanation
Given two strings s and t, return true if t is an anagram of s, and false otherwise.
Example 1 :
```
Input: s = "anagram", t = "nagaram"
Output : true
```
since nagaram er letters gulo ektu eidik oidik korle tumi anagram peye jachcho
Example 2 :
```
Input: s = "rat", t = "car"
Output : false
```
## Algorithm
### Naive approach
1. Sort both the strings.
2. If both the strings are now equal then return true, else return false.
### Code
```
bool isAnagram(string s, string t) {
        if(s.length() != t.length()) return false;
        sort(s.begin(),s.end());
        sort(t.begin(),t.end());
        return (s == t);
    }
```
* **Time complexity** - N log N + M log M
* **Space complexity** - O(1)
### Optimized solution
1. First check if the lengths of both the strings are equal. If not, return false immediately as they cannot be anagrams.
2. Initialize a frequency array of size 26(for all lowercase english letters) & set it to 0.
3. Traverse the first string & increment the frequency of each character.
4. Traverse the 2nd string & decrement the frequency of each character.
5. Finally check if all the elements in the frequency array are zero. If not, return false since they're not anagrams.
6. If all frequencies are zero, then the strings are anagrams and the function returns true.
### Code
```
bool isAnagram(string s, string t) {
        if(s.length() != t.length()) return false;
        int freq[26] = {0};
        for(int i=0; i<s.length(); i++){
            freq[s[i]-'a']++;
        }
        for(int i=0; i<t.length(); i++){
            freq[t[i]-'a']--;
        }
        for(int i=0; i<26; i++){
            if(freq[i] != 0) return false;//they are not anagrams
        }
        return true;
    }
```
* **Time complexity** - O(n)
* **Space complexity** - O(1)
