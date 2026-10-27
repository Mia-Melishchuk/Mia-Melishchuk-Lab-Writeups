# Code
```
class Solution:
    def findJudge(self, n: int, trust: list[list[int]]) -> int:
        if n == 1:
            return 1
        elif len(trust) == 0:
            return -1           # judge cannot be identified if len(trust) = 0 and n > 1
        

        trustingPeople = [0] * n
        trustedPeople = [0] * n
        
        for relationship in trust:
            trustingPeople[relationship[0] - 1] += 1
            trustedPeople[relationship[1] - 1] += 1
        
        for i in range(0, n):
            if trustingPeople[i] == 0 and trustedPeople[i] == (n - 1):
                return i + 1
        
        return -1
```
# Description
For this problem, the goal was to find the judge, or the person in the town of n people who trusted nobody and who everyone else (n - 1 people) trusted. 
First, I handled the special cases that come with these specifications: if n is 1, then there is only one person in the town and they are the judge; and if n > 1 but the 2D matrix of trust relationships is empty, then the judge cannot be identified because nobody trusts anyone. 
Once I got those out of the way, I made two arrays of length n, with one being for the trusting person in each relationship and the other being for the trusted people in each relationship. 
Then, I looped through the trust matrix and, in each iteration, incremented each person's place in their array to show that that person either trusts someone or is trusted by someone. 
Once that was done, I looked through the two arrays simultaneously looking for a person who trusts nobody (the value at their index in trustingPeople was 0) and who is trusted by everybody (the value at their index in trustedPeople was n - 1). 
If this person existed, their number was returned. If not, I returned -1. 
# Analysis
For the runtime, I have two for loops: one for the length of trust and one of length n. The length of trust is not necessarily defined by n, but we know mathematically that it cannot exceed (n * (n-1))/2. 
Combined with the second loop, the runtime in the worst case is (n * (n-1))/2 + n, or O(n^2). 

For the space complexity, I am creating two arrays of length n, so the space complexity is 2n or O(n) asymptotically. 
