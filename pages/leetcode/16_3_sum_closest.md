### 16. 3Sum Closest

[View Problem in Leetcode](https://leetcode.com/problems/3sum-closest/description/)

My analysis:

1. A brute force approach would be to generate all posible triplets and compare their sum with the target, keeping track of the minimum difference and the sum that corresponds to that difference. 
2. Generating / checking all possible triples is the expensive part of the problem. It would be great to optmize as much as we can. 
    1. We can sort the initial array.
    2. Have an inital value of the sum, which will correspond to `a, b, c = 0, 1, 2` where `sum = nums[a] + nums[b] + nums[c]` and the difference is going to be equal to the distance between the numbers, that is:
    
    `diff = AbsoluteValue(target - sum)`

    3. Use a similar approach to the [3Sum](./15_3_sum.md) Problem. Loop the entire array fixing an position `i`, such that `i < len(arr) - 2`. For each position use a two pointer approach comparing the sum and difference with the recorded one, updating as necessary. For each iteration we could always avoid doing the same for repeated values.

##### Code:
```go
func threeSumClosest(nums []int, target int) int {
    // Sort the initial array
    sort.Ints(nums)

    sum := nums[0] + nums[1] + nums[2]
    diff := math.Abs(float64(target - sum))

    for i := -0; i < len(nums) - 2; i++ {
        // Skip duplciates entries
        if i > 0 && nums[i] == nums[i - 1]{
            continue
        }

        left, right := i + 1, len(nums) - 1

        for left < right {
            iterSum := nums[i] + nums[left] + nums[right]
            iterDiff := math.Abs(float64(target - iterSum))
            if iterDiff < diff {
                diff = iterDiff
                sum = iterSum
            }

            if iterSum < target {
                left++
            } else if iterSum > target {
                right--
            } else {
                return iterSum
            }
        }
    }

    return sum
}
```