# Problem Explanation
Return the maximum possible frequency of an element after performing at most k operations.

**Example 1 -**
```
Input: nums = [1,2,4], k = 5
Output: 3
Explanation: Increment the first element three times and the second element two times to make nums = [4,4,4].
4 has a frequency of 3.
```
## Approach 1 - By binary search
### Algorithm
* First sort the array.
* Maintain a prefix array of sum of elements in the array.
* Now for each index in the array do binary search and find out the max. possible frequency of an element by performing atmost k operations.
* In bSearch take two pointers, l at 0, and r at target_idx.
* Our window is from mid to target_idx, first we'll find the no. of operations it will take for all the elements in the window to be equal to target_idx.
* If the no. of operations is greater than k, then we'll make the window smaller.
* And if the no. of operations is smaller or equal to k, then we'll make the window larger.
* Then atlast we'll return the frequency.
### Code
```
class Solution {
public:
    int bSearch(vector<int>& nums, int k, vector<long>& prefSum, int target_idx){
        int l = 0;
        int r = target_idx;
        int best_idx = target_idx;
        while(l <= r){
            int mid = l + (r - l)/2;
            long count = target_idx - mid + 1;

            long windowSum = nums[target_idx] * count;
            long currSum = prefSum[target_idx] - prefSum[mid] + nums[mid];

            int ops = windowSum - currSum;

            if(ops > k){
                l = mid + 1;
            }
            else{
                best_idx = mid;
                r = mid - 1;
            }
        }
        return target_idx - best_idx + 1;
    }
    int maxFrequency(vector<int>& nums, int k) {
        int n = nums.size();

        sort(begin(nums), end(nums));

        vector<long> prefSum(n);
        for(int i=1; i<n; i++){
            prefSum[i] = prefSum[i-1] + nums[i];
        }

        int result = 0;

        for(int target_idx = 0; target_idx < n; target_idx++){
            result = max(result,bSearch(nums,k,prefSum,target_idx));
        }

        return result;
    }
};
```
* **Time Complexity - O(n log n)**
* **Space Complexity - O(n)**
