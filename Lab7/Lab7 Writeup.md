# Code
```
class Solution:
    def floodFill(self, image: list[list[int]], sr: int, sc: int, color: int) -> list[list[int]]:

        def change(row, col, ogcolor, newcolor):
            if ogcolor != newcolor:
                image[row][col] = newcolor
                
                if col - 1 >= 0:
                    if image[row][col - 1] == ogcolor:
                        change(row, col - 1, ogcolor, newcolor)

                if col + 1 < len(image[row]):
                    if image[row][col + 1] == ogcolor:
                        change(row, col + 1, ogcolor, newcolor)

                if row - 1 >= 0:
                    if image[row - 1][col] == ogcolor:
                        change(row - 1, col, ogcolor, newcolor)

                if row + 1 < len(image):
                    if image[row + 1][col] == ogcolor:
                        change(row + 1, col, ogcolor, newcolor)

        
        change(sr, sc, image[sr][sc], color) 
        return image
```
# Description
For this problem, we were given a 2D array of colors representing the pixels that create an image.
Given a starting location and a target color, the goal was to change the starting pixel and the pixels of the same color surrounding it into the target color. 
To solve this problem, I created a recursive function called change() that takes 4 parameters: the row and column of the pixel being changed, the original color of the starting pixel, and the target color.
First, I check if the target color is already the same as the color of the starting pixel, because in that case nothing needs to be done. 
After that, I set the pixel to the new color and I look at each adjacent pixel in each of the four directions, make sure it is within the dimensions of the matrix, and check if it is the same color as the starting pixel was.
If it was, then I called change() on that pixel to continue expanding the search area. 
In the main floodFill function, I put the starting pixel into the recursive function, let it take its course, and returned the modified image.
# Analysis
The runtime complexity of my solution is O(n). In the worst case scenario, every pixel would need to be changed and therefore would require one recursive call to change it.
All of the if statements are constant time, so the amount of work done is directly proportional to the number of pixels that have to be changed, and is therefore O(n).

The space complexity is also O(n), because every recursive call takes up space in memory and there are at most n recursive calls. 
