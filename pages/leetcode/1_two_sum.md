### 1. Two Sum

[View Problem in Leetcode](https://leetcode.com/problems/two-sum/description/)

##### Analysis:

My Appraoches:

1. A brute force approach would be to generate all index pairs `[a,b]` and for each pair evalute:

`nums[a] + nums[b] == target`. If a match is found then return the index pair. This approach will take two much computing power. Specifically `O(N^2)`. 

2. Another approach could be sorting the array `O(N log N)`, and use a two pointer approach: 

`left = 0` `right = len(nums)`

Check the sum of `nums[left] + nums[right]` while `left < right` and adjust them accordingly based on their actual difference with `target`. Once the sum is equal we just retunr `[left, right]`. We can always optimize this to avoid checking for the same value of `right` or `left` that was checked before.

3. If we want to optmize it a little more, we can use an algorithm that will run in `O(N)` with help of extra memory. In this case a `map[target - nums[i]]index` where `index` corresponds to index at which the key was created. In another words, for each number in the array, we are computing the difference with target and saving that difference as a key and the value will be the index of the number we used. Since there is a solution, there is going to be a point at which `map[nums[i]] == maps[target - nums[index]]`. This will allows us to return `[index, i]`.

##### Code:
```go
func twoSum(nums []int, target int) []int {
    track := map[int]int{}

    for i, num := range nums {
        if index, ok := track[num]; ok {
            return []int{i, index}
        }else{
            track[target-num] = i
        }
    }
    return []int{}
}
```