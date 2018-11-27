# Q
Roman numerals are represented by seven different symbols: I, V, X, L, C, D and M.

Symbol       Value
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
For example, two is written as II in Roman numeral, just two one's added together. Twelve is written as, XII, which is simply X + II. The number twenty seven is written as XXVII, which is XX + V + II.

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not IIII. Instead, the number four is written as IV. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as IX. There are six instances where subtraction is used:

I can be placed before V (5) and X (10) to make 4 and 9. 
X can be placed before L (50) and C (100) to make 40 and 90. 
C can be placed before D (500) and M (1000) to make 400 and 900.
Given a roman numeral, convert it to an integer. Input is guaranteed to be within the range from 1 to 3999.

Example 1:
```
Input: "III"
Output: 3
Example 2:

Input: "IV"
Output: 4
Example 3:

Input: "IX"
Output: 9
Example 4:

Input: "LVIII"
Output: 58
Explanation: L = 50, V= 5, III = 3.
Example 5:

Input: "MCMXCIV"
Output: 1994
Explanation: M = 1000, CM = 900, XC = 90 and IV = 4.
```
# My 错了 如IL 可以是49，只要是小于右边的数字都应该被理解为减法
```
class Solution(object):
    def romanToInt(self, s):
        """
        :type s: str
        :rtype: int
        """
        result = 0
        dic = {'I': 1, 'V': 5, 'X': 10, 'C': 100, 'L':50, 'D': 500, 'M': 1000}
        i = 0
        while len(s) - i > 0:
            if s[i] == 'I':
                if i+1 < len(s) and s[i+1] == 'V':
                    result += 4
                    i += 2
                elif i+1 < len(s) and s[i+1] == 'X':
                    result += 9
                    i += 2
                else:
                    result += 1
                    i += 1
            elif s[i] == 'X':
                if i+1 < len(s) and s[i+1] == 'L':
                    result += 40
                    i += 2
                elif i+1 < len(s) and s[i+1] == 'C':
                    result += 90
                    i += 2
                else:
                    result += 10
                    i += 1
            elif s[i] == 'C':
                if i+1 < len(s) and s[i+1] == 'D':
                    result += 400
                    i += 2
                elif i+1 < len(s) and s[i+1] == 'M':
                    result += 900
                    i += 2
                else:
                    result += 100
                    i += 1
            else:
                result += dic[s[i]]
                i += 1
        return result
```
# Better
```
class Solution:
    def romanToInt(self, s):
        """
        :type s: str
        :rtype: int
        """
        dict_ = {
           'I':1,'V':5,'X':10,'L':50,'C':100,'D':500,'M':1000 
        }
        res = i = 0
        while i < len(s):
            if i+1<len(s) and dict_[s[i+1]] > dict_[s[i]]:
                res += dict_[s[i+1]]-dict_[s[i]]
                i +=2
            else :
                res += dict_[s[i]]
                i +=1
        return res
```