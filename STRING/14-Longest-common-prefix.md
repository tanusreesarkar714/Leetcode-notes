## Algorithm
* Sort the array
* Then compare the first and last strings of the array, and the moment you find a uncommon character, break the loop.
* Return the common prefix
* **first.size() and last.size() returns size_t (unsigned), so if either string is empty, first.size() - 1 underflows to a huge number (SIZE_MAX) instead of going negative. i.e. why we're instead storing it on int to avoid this condition.**
## Code
```
string longestCommonPrefix(vector<string>& strs) {
        if(strs.empty()) return "";
        int n = strs.size();
        sort(strs.begin(), strs.end());
        string first, last;
        first = strs[0];
        last = strs[n-1];
        string ans = "";
        int minLen = min(first.size(),last.size());
        for(int i=0; i<minLen; i++){
            if(first[i] != last[i]) break;
            ans += first[i];
        }
        return ans;
    }
```
