# Code
```
class Solution:
    def isValid(self, s: str) -> bool:
        opens = []

        for i in s:
            if i == "(" or i == "[" or i =="{":
                opens.append(i)
            elif len(opens) > 0:
                if ((opens[-1] == "(" and i == ")") or (opens[-1] == "[" and i == "]") or (opens[-1] == "{" and i == "}")): 
                    opens.pop()
                else:
                    return False
            else:
                return False
        
        if len(opens) == 0:
            return True
        else:
            return False
```
# Description
For this problem, the goal was to look at the input string and determine whether it was valid by checking if every open bracket has a corresponding closing bracket, that the brackets are closed in the order they were opened, and that every closing bracket has a corresponding open bracket. 
To do this, I made a stack of open brackets called opens and looped through the input string, and every time an open bracket came in, it was pushed onto the stack. 
Every time a closing bracket came in, I first checked if the stack had anything in it (if it was empty, then the closing bracket doesn't have a corresponding open bracket and I would return false).
If the stack wasn't empty, I checked if the closing bracket in the input string matched the bracket at the top of the stack and popped. If it matched, I popped it off the stack and if it didn't, I returned false.
After the loop ended, I checked whether the stack was empty. If there were any items left in the stack, that would mean that open brackets didn't have any corresponding closing brackets and I returned false. 
If the stack was empty, I returned true. 
# Analysis
The time complexity of the program is O(n), with n being the number of characters in the input string, because I iterate through the input string one time and all of the if statements and other operations are constant time.

The space complexity is also O(n) because I create the stack and in the worst case scenario, the input string is made up of only open brackets so the stack would be the same size as the input string.
