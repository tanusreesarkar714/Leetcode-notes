# Problem Explanation

Given a string s , we have to rearrange it's characters such that **the one with higher frequency appears first**. 

If multiple characters have same frequency, then any of them can appear first (i.e. **in case of same frequency, the order doesnot matter**).
The strings can also have capital letters and digits, alongside the small letters.

Example : 

```
> Input:
> s = "tree"
> 
> Frequencies:
> t -> 1
> r -> 1
> e -> 2
> 
> Output:
> "eert" or "eetr"
> we can return the string in any order
```

## **Method I - Sorting**

### Algorithm
1. Store in a structure the frequency of each character in the given string.
2. Then sort the string on the basis of frequency, and if frequency of many characters is same then whoever comes first in a-z,i.e.ascii no.(or the opp.)

The sorting is done here with lambda and not comparator, bcz comparator is a function which have to be written outside the main, while lambda is written inside main and it can use all the variables of main.

```
string frequencySort(string s) {
        vector<int> freq(128,0);
        for(char ch : s) freq[ch]++;//hash

        auto cmp = [&](char a,char b){
            if(freq[a] == freq[b]) return a < b;
            return freq[a] > freq[b];
        };

        sort(s.begin(),s.end(),cmp);
        return s;
    }
```

**Time complexity**

O(n) where n is the length of the string.
* for array it is O(n)
* for sorting it is O(n log n)
So total: **O(n) + O(n log n) = O(n log n)** (the sort dominates)

**Space complexity**

O(1) - because freq array is fixed size 128 regardless of input size → constant space, not O(n)

## **Method II - Sorting only K distinct characters**

### Algorithm
1. Count frequency of each characters that appears in the string.
And this can be done in 2 ways,either by using an array/vector of 128 size(which we're trying to avoid) or by an unordered map.
* Unordered maps are :-
* Dynamic buckets that grows as needed,so no wasted slots like in vector,array.
* Indexing is done by key
* Holds one pair per key as it appears, no wasted slots
2.  Now move it into a vector
3. Now sort it using comparator
4. Build the result string 
ans.append(int,char) mane char ta int e thaka no. ta jodi 2 hoye thn 2 baar ans string e add koro

```
string frequencySort(string s) {
        unordered_map<char,int> freq;
        for(char ch : s) freq[ch]++;

        vector<pair<char,int>> freqArr;
        for(auto &it : freq) freqArr.push_back({it.first,it.second});

        auto cmp = [&](pair<char,int>p1, pair<char,int>p2){
            return p1.second > p2.second;
        };

        sort(freqArr.begin(),freqArr.end(),cmp);

        string ans = "";
        for(auto &it : freqArr){
            ans.append(it.second,it.first);
        }
        return ans;
}
```

**Time complexity**
*O(n + k log k)*, where n = length of s, k = number of distinct characters (at most 62: lowercase + uppercase + digits).

* Counting frequencies: O(n) — one pass over s.
* Building freq vector: O(k) — one entry per distinct char.
* Sorting freq: O(k log k) — sorting k pairs.
* Building ans with append: O(n) total — across all iterations, the total characters   appended equals n (sum of all frequencies).

**Space complexity**
*O(n + k) → effectively O(n)*

* freq map: O(k)
* freqArr vector: O(k)
* ans string: O(n)
