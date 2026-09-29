## Code
```
class Solution:
    def getParentPath(self, folderName):
        # takes ending off of the folder name
        num = 0
        for i in range(len(folderName)):
            if folderName[i] == '/':
                num = i
        return folderName[0:num]

    def isSaved(self, fList, folderName):
        # if the folder or any of its parent folders are saved in our final array
        for i in fList:
            if folderName == i:
                return True
        fParent = self.getParentPath(folderName)
        if fParent != "":
            return self.isSaved(fList, fParent)
        return False

    def removeSubfolders(self, folder: list[str]) -> list[str]:
        folder.sort(key=len)

        goodFolders = []

        for i in folder:
            if not self.isSaved(goodFolders, self.getParentPath(i)):
                goodFolders.append(i)

        return goodFolders
```
## Explanation
For this problem, the goal was to return an array of all of the folder paths without any subfolders of those paths remaining in it. 
To do this, after thinking about various other ways to do it, the simplest way to start was by sorting the input array by length to make sure that any possible subfolders come after their parent.
I wrote a method that would return the entire path of a file except the final folder, so if it is run multiple times it would ultimately remove the entire path.
Then, I iterate through the input array and, for each path in the array, check if any parent of that path is saved in the separate array of "good folders", which holds the final folders for the solution.
If the folder we are looking at has no parents in the return array, it is placed in the return array.

## Complexity
The first thing that is done is folder.sort(), which uses Timsort to sort the input array. This has a time complexity of O(*n* lg*n*) and a space complexity of O(*n*).
After this, iterating through the input array has a linear runtime, and at each item we iterate through the return array (which is of length *n* in the worst case).
The runtimes of the other actions depend on the length of each item in the array, but not on the input size, so it would be ignored in the big-O simplification. The runtime would be O(*n^2*).
Since we are creating the return array, the space complexity comes out to around 2*n* in the worst case, so O(*n*). 
