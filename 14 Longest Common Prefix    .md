# Q
Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string "".

Example 1:
```
Input: ["flower","flow","flight"]
Output: "fl"
Example 2:

Input: ["dog","racecar","car"]
Output: ""
Explanation: There is no common prefix among the input strings.
```
Note:

All given inputs are in lowercase letters a-z.

# Better Ans
学到的东西
1. sorted()将list排序，根据第一个字母，第二个字母这样排。这样子把第一个和最后一个flower比较即可，因为排在最后的和第一个存在最大不同。不用每个都比较
```
>>> c = ['flower', 'flow', 'flight']
>>> sorted(c)
['flight', 'flow', 'flower']
```
2. if strs:判断中""是会判断为存在
3. str.startswith()
```
>>> help(str.startswith)
Help on method_descriptor:

startswith(...)
    S.startswith(prefix[, start[, end]]) -> bool

    Return True if S starts with the specified prefix, False otherwise.
    With optional start, test S beginning at that position.
    With optional end, stop comparing S at that position.
    prefix can also be a tuple of strings to try.
```

```
class Solution:
    def longestCommonPrefix(self, strs):
        """
        :type strs: List[str]
        :rtype: str
        """
        if not strs:
            return ""
        sort_string = sorted(strs)
        result = ''
        for char in sort_string[0]: 
            if sort_string[-1].startswith(result+char):
                result +=char
            else:
                break
        return result
```


## None 与""的区别
万物皆对象

""print出来的结果是null
```
In[3]: type(None)
Out[3]: NoneType

In[4]: type('')
Out[4]: str
```
```
>>> a = []
>>> if a:
...     print(1)
...
>>> a = [None]
>>> if a:
...     print(1)
...
1  # NoneType 也是一种对象
>>> a = [""]
>>> if a:
...     print(1)
...
1 # "" is str
```




