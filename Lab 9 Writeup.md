# Code
```
class Solution:
    def minCostClimbingStairs(self, cost: list[int]) -> int:
        stepCost = [0] * len(cost) # create array with cost.length spaces
        for i in range(len(cost)):
            if i < 2:
                stepCost[i] = cost[i] # fill in the cost to reach the first two steps
            else:
                # cost of current step + minimum cost to get in its range
                stepCost[i] = cost[i] + min(stepCost[i-1], stepCost[i-2])
        return min(stepCost[-1], stepCost[-2])
```
# Description
For this problem, the goal was to find the minimum cost to reach the top of a staircase if each step has a different cost to reach and you can only jump up to two steps at a time.
To solve this problem, I created an array called stepCost to represent the total minimum cost it would take to reach each step in the staircase. 
Then, I loop through the costs of each step and, for the first two steps, put the costs directly into stepCost. 
After the first two steps, the cost to reach any subsequent step is just the cost of that step plus the minimum cost to reach any step in its "range" (one of the two steps before it). 
This ensures that, for each step, the minimum cost to reach it is stored in stepCost. 
Since the top of the staircase is the imaginary place after the last index in the array, the minimum cost to reach it is the minimum of the last two items in stepCost because the last two steps are the "range" of the top. 

# Analysis
The runtime complexity of this solution is O(n), where n is the number of steps, since I only traverse through the array of costs one time. All other operations are constant time.

The space complexity is also O(n) since I am creating stepCost, which is the same length as the input array. 
