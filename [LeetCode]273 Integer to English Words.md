# [LeetCode]273 Integer to English Words

## 题目描述
[LeetCode 8 String to Integer (atoi)](https://leetcode.com/problems/string-to-integer-atoi/)

Convert a non-negative integer to its english words representation. Given input is guaranteed to be less than 231 - 1.

For example,

	123 -> "One Hundred Twenty Three"
	12345 -> "Twelve Thousand Three Hundred Forty Five"
	1234567 -> "One Million Two Hundred Thirty Four Thousand Five Hundred Sixty Seven"

**Hint**:

Did you see a pattern in dividing the number into chunk of words? For example, 123 and 123000.

Group the number by thousands (3 digits). You can write a helper function that takes a number less than 1000 and convert just that chunk to words.

There are many edge cases. What are some good test cases? Does your code work with input such as 0? Or 1000010? (middle chunk is zero and should not be printed out)

## 题目大意
将非负整数转化为其英文单词表示。给定输入确保小于 2 ^ 31 - 1

提示：

是否发现了将数字拆分成一组单词的模式？例如，123和123000。

将数字以千为单位分组（3位数）。可以写一个帮助函数，输入一个小于1000的数，然后将其转化为单词。

有许多边际样例。好的测试样例是什么？你的代码可以正确处理诸如0或者1000010的输入吗？（单词中间的0不应该输出）

## 要点分析
**除法与取模**

使用除法和取模运算将数字以千为单位拆分成数组

**Edge Case**

Zero的处理。

	
## python源码
递归版本，参考[LeetCode Discuss：https://leetcode.com/discuss/55477/recursive-python](https://leetcode.com/discuss/55477/recursive-python)
	
``` python
class Solution(object):
    def numberToWords(self, num):
        """
        :type num: int
        :rtype: str
        """
        to19 = 'One Two Three Four Five Six Seven Eight Nine Ten Eleven Twelve ' \
               'Thirteen Fourteen Fifteen Sixteen Seventeen Eighteen Nineteen'.split()
        tens = 'Twenty Thirty Forty Fifty Sixty Seventy Eighty Ninety'.split()
        def words(n):
            if n < 20:
                return to19[n-1:n]
            if n < 100:
                return [tens[n/10-2]] + words(n%10)
            if n < 1000:
                return [to19[n/100-1]] + ['Hundred'] + words(n%100)
            for p, w in enumerate(('Thousand', 'Million', 'Billion'), 1):
                if n < 1000**(p+1):
                    return words(n/1000**p) + [w] + words(n%1000**p)
        return ' '.join(words(num)) or 'Zero'
```

## Tips
### 1 enumerate(sequence, [start=0])
	参数 sequence -- 一个序列、迭代器或其他支持迭代对象。
		 start -- 下标起始位置。
	enumerate() 函数用于将一个可遍历的数据对象(如列表、元组或字符串)组合为一个索引序列，
	同时列出数据和数据下标，一般用在 for 循环当中。
``` python
for p, w in enumerate(('Thousand', 'Million', 'Billion'), 1):
	if n < 1000**(p+1):
   		return words(n/1000**p) + [w] + words(n%1000**p)
<=>
if n < 1000:
	return words(n/1000) + ['Thousand'] + words(n%1000)
if n < 1000**2:
	return words(n/1000**2) + ['Million'] + words(n%1000**2)
if n < 1000**3:
	return words(n/1000**3) + ['Billion'] + words(n%1000**3)
	
```	

	
### 2 ' '.join(words(num)) or 'Zero'
	x or y	布尔"或"	- 如果x是非 0，它返回x的值，否则它返回y的计算值.
	<=>' '.join(words(num)) if ' '.join(words(num)) else 'Zero'

	 
