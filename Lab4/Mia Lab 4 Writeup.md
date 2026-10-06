# Code
```
class Solution:
    def maxProduct(self, nums: list[int]) -> int:
        max1 = max(nums[0], nums[1])
        max2 = min(nums[0], nums[1])
        if len(nums) == 2:
            return (max1 - 1) * (max2 - 1)

        for i in range(2, len(nums)):
            if nums[i] > max1:
                temp = max1
                max1 = nums[i]
                max2 = temp
            elif nums[i] > max2:
                max2 = nums[i]

        return (max1 - 1) * (max2 - 1)
```
# Explanation
In this problem, we are given an array of ints and are asked to find the two highest items, subtract 1 from each of them, and return the product. 
To do this, I have two variables to hold the two values and initially set them to the first two items in the array (since it is guaranteed to have at least two items), with the larger one being max1 and the smaller being max2.
If the array has more than two items, I iterate through the rest of them one by one. 
If the current item is greater than max1, it becomes the new max1 and max2 is set to the value of the old max1.
If the current item is less than or equal to max1 but greater than max2, then it becomes the new max2.
Once we have iterated through the whole array once, max1 will be the greatest item in the array and max2 will be the second greatest.
Finally, we return the product of max1 - 1 and max2 - 1. 

# Analysis
For the time complexity, I first run the max() and min() functions, each of which are O(1) (*technically*, they are each O(*n*) but *n* is 2 in our situation because it takes two integer arguments so it's O(2)). 
The main loop iterates through the whole array (minus the first 2 items) exactly one time in all cases, and assignment operations are constant time so this solution has an O(*n*) runtime.

For the space complexity, I initialize 3 variables (max1, max2, and temp to do the assignment). These variables exist regardless of *n*, so the space complexity is O(1). 
