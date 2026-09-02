# Problem Explanation
Given two strings s & t, determine if they're isomorphic.

Examples :
```
Input: s = "egg", t = "add"

Output: true

Explanation:

The strings s and t can be made identical by:

Mapping 'e' to 'a'.
Mapping 'g' to 'd'.

Input: s = "f11", t = "b23"

Output: false

Explanation:

The strings s and t can not be made identical as '1' needs to be mapped to both '2' and '3'.
```
## Naive approach
### Algorithm
* For every character check it's occurence pattern in string s and string t and store the positions.
* Then match if the occurence pattern of both strings are same or not.
### Code
```
bool isIsomorphic(string s, string t) {
        int n = s.size();
        if(t.size() != n)return false;
        for(int i=0; i<n; i++){
            vector<int> posInS,posInT;
            for(int j=0; j<n; j++){
                if(s[j] == s[i]) posInS.push_back(j);
                if(t[j] == t[i]) posInT.push_back(j);
            }
            if(posInS != posInT) return false;
        }
        return true;
    }
```
* **Time Complexity** - O(n^2)
* **Space Complexity** - 2 * O(n)
## Optimized approach
### Algorithm
* Take two unordered maps :-
1. mapST : maps a character in S -> a character in T
2. mapTS : maps a character in T -> a character in S
* Only need one pass through the strings. At each index we check :-
1. The current character, has it been previously mapped?
2. If yes then is the character that it was mapped to the same character to which it is now supposed to be mapped to?
3. If no then create new mapping.
### Code
```
bool isIsomorphic(string s, string t) {
        int n = s.size();
        if(t.size() != n) return false;
        unordered_map<char,char>mapST;
        unordered_map<char,char>mapTS;
        for(int i=0; i<n; i++){
            char c1 = s[i];
            char c2 = t[i];
            // check mapping from s -> t
            if(mapST.count(c1)){
                if(mapST[c1] != c2) return false;
            }
            else{
                mapST[c1] = c2;//create new mapping
            }
            // check mapping from t -> s
            if(mapTS.count(c2)){
                if(mapTS[c2] != c1) return false;
            }
            else{
                mapTS[c2] = c1;//create new mapping
            }
        }
        return true;
    }
```
* **Time complexity** - O(n)
* **Space complexity** - O(1)
