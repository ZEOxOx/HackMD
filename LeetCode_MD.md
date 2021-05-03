# a.Leet Code 刷題紀錄

###### tags: Leet Code

## 1.Two Sum

* <font color="#0080FF">**Code**</font>

```python=+
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        for i in range(len(nums)):
            for j in range(i+1,len(nums)):
                if(nums[i] + nums[j] == target):
                    return [i,j]         
"""
Runtime: 48 ms, faster than 57.66%
Memory Usage: 14.2 MB, less than 98.18%
"""
```

![](https://i.imgur.com/aKitedR.png)

## 2.Invert Binary Tree

* <font color="#0080FF">**Code**</font>

```python=+
class Solution:
    def invertTree(self, root: TreeNode) -> TreeNode:
        if not root:
            pass
        else:
            root.left,root.right = self.invertTree(root.right),self.invertTree(root.left) 
        return root
        
"""
Runtime: 32 ms, faster than 57.26%
Memory Usage: 14.2 MB, less than 74.02%
"""
```

![](https://i.imgur.com/GB2ePe0.png)

## 3.Delete Node in a Linked List

* <font color="#0080FF">**Code**</font>

```python=+
class Solution:
    def deleteNode(self, node):
        node.val = node.next.val
        node.next = node.next.next
"""
Runtime: 32 ms, faster than 94.65%
Memory Usage: 14.9 MB, less than 30.96%
"""
```

![](https://i.imgur.com/2es7qXO.png)

## 4.Reverse String

* <font color="#0080FF">**Code**</font>

```python=+
class Solution:
    def reverseString(self, s: List[str]) -> None:
        s.reverse()
"""
Runtime: 184 ms, faster than 95.26%
Memory Usage: 18.8 MB, less than 21.89%
"""
```

![](https://i.imgur.com/YssQc3k.png)

## 5.First Unique Character in a String

![](https://i.imgur.com/5FWT5X4.png)

* <font color="#0080FF">**Code**</font>

```python=+
import collections
class Solution:
    def firstUniqChar(self, s: str) -> int:
        
        a=OrderedDict(Counter(s))
        for i,k in a.items():
            if k==1:
                return s.find(i)
        return -1
"""
Runtime: 56 ms, faster than 97.03%
Memory Usage: 14.4 MB, less than 69.10%
"""
```

## 6.Two City Scheduling

* <font color="#0080FF">**Code**</font>

```python=+
class Solution:
    def twoCitySchedCost(self, costs: List[List[int]]) -> int:
        ans = 0
        ls = []
        for i  in range(len(costs)):
            ls.append([(costs[i][0] - costs[i][1]),i])
        ls.sort()
        
        half = (len(costs) / 2)
        for j in range(len(costs)):
            
            if(j >= half):
                ans += costs[(ls[j][1])][1]
            else:
                ans += costs[(ls[j][1])][0]
        return ans
"""
Runtime: 36 ms, faster than 84.52%
Memory Usage: 14.2 MB, less than 89.46%
"""
```

![](https://i.imgur.com/52hxI6X.png)