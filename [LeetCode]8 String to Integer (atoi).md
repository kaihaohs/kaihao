# [LeetCode]8 String to Integer (atoi)

## 题目描述
[LeetCode 8 String to Integer (atoi)](https://leetcode.com/problems/string-to-integer-atoi/)

Implement atoi to convert a string to an integer.

**Hint**: Carefully consider all possible input cases. If you want a challenge, please do not see below and ask yourself what are the possible input cases.

**Notes**: It is intended for this problem to be specified vaguely (ie, no given input specs). You are responsible to gather all the input requirements up front.

**Requirements for atoi**
The function first discards as many whitespace characters as necessary until the first non-whitespace character is found. Then, starting from this character, takes an optional initial plus or minus sign followed by as many numerical digits as possible, and interprets them as a numerical value.

The string can contain additional characters after those that form the integral number, which are ignored and have no effect on the behavior of this function.

If the first sequence of non-whitespace characters in str is not a valid integral number, or if no such sequence exists because either str is empty or it contains only whitespace characters, no conversion is performed.

If no valid conversion could be performed, a zero value is returned. If the correct value is out of the range of representable values, INT_MAX (2147483647) or INT_MIN (-2147483648) is returned.

## 题目大意
实现atoi函数将字符串转换为整数。

**提示**：仔细考虑所有输入用例。如果想给自己挑战，请不要看下面的内容并询问自己所有可能的输入用例。

**注意**：这道题有意描述地比较含糊（亦即，没有给出输入用例）。你需要自己发掘所有的输入要求。

**atoi的要求**：

函数首先尽可能多的丢弃空白字符，直到发现第一个非空字符位为止。 接着从这个字符开始，读入一个可选的正负号，然后尽可能多的读入数字，最后将它们解析成数值。

字符串中在合法数字后可以包含额外的非法字符，对于这些字符只需丢弃即可。

如果字符串的非空字符不是一个有效的整数，或者，当字符串为空或者只包含空白字符时，不需要执行转换。

如果不能够执行有效的转换则返回0。如果得到的数值超出了整数范围，返回INT_MAX (2147483647) 或者 INT_MIN (-2147483648)。

## 要点分析
**Input Edge Case**

How to catch exceptions and corner case？往往一个函数或者程序的输入是有很多Edge Case的，为了程序的**robustness**，我们需要处理这些异常的Case。

	
## python源码
	
``` python
class Solution(object):
    def myAtoi(self, str):
        """
        :type str: str
        :rtype: int
        """
        if len(str) == 0:
            return 0
        str = str.strip()
        start = 1 if str[0] in ('+','-') else 0
        res = 0
        for i in range(start, len(str)):
            if not str[i].isdigit():
                break
            res = res*10 + ord(str[i]) - ord('0')
        res *= (-1 if str[0] == '-' else 1)
        return max(-2147483648, min(res,2147483647))
```

## Tips
### 1 用max和min减少if else
	max(min_value, min(res, max_value))
	
### 2 str.strip([chars])
	[可指定移除字符串头尾的任意字符](默认为空格）
	 chars -- 移除字符串头尾指定的字符
	 
### 3 isdigit()	
	 方法检测字符串是否只由数字组成(单个字符和字符串都可以)
	 
### 4 ord()
	ord() 函数是 chr() 函数（对于8位的ASCII字符串）或 unichr() 函数（对于Unicode对象）的配对函数
	它以一个字符（长度为1的字符串）作为参数，
	返回对应的 ASCII 数值，或者 Unicode 数值，
	如果所给的 Unicode 字符超出了你的 Python 定义范围，则会引发一个 TypeError 的异常。
	ord(char) - ord('0')