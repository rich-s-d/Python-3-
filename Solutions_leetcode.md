# question 11
```py
class Solution(object):
    def maxArea(self, height):
        """
        :type height: List[int]
        :rtype: int
        """
        
        areas =[]
        
        for i, a in enumerate(height):
            for j, b in enumerate(height[i+1:], i+1):
                area = min(a, b) * (j - i)
                areas.append(area)
        
        return max(areas) 
```
