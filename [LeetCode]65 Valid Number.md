# [LeetCode]65 Valid Number

## 题目描述
[LeetCode 65 Valid Number](https://leetcode.com/problems/valid-number/)

Validate if a given string is numeric.

	Some examples:
	"0" => true
	" 0.1 " => true
	"abc" => false
	"1 a" => false
	"2e10" => true

**Note:** It is intended for the problem statement to be ambiguous. You should gather all requirements up front before implementing one.

## 题目大意

给定一个字符串，验证其是否为数字。

**提示**：题目给的问题陈述是模糊的，你需要自己把需要的各种情况找到。


## 要点分析
**Gather Cases**

一个数字有多种多样的表现形式，这道题考查能不能把各种情况都能考虑到，也就是考虑问题要全面。其次考察将各种条件聚合在一起的能力。

**确定有穷状态自动机(DFA)**

建立DFA最难的部分，你需要把每种状况都考虑到!!!

0 初始无输入或者只有space的状态

1 输入了数字之后的状态

2 前面无数字，只输入了dot的状态

3 输入了+/-状态

4 前面有数字和有dot的状态

5 'e' or 'E'输入后的状态

6 输入e之后输入+/-的状态

7 输入e后输入数字的状态

8 前面有有效数输入之后，输入space的状态

![DFA](http://normanyahq.github.io/static/files/valid_number_dfa.svg)

## python源码(一维DFA)
	
``` python
class Solution(object):
    def isNumber(self, s):
        """
        :type s: str
        :rtype: bool
        """
        s = s.strip()
        # Difficult part -> Define State (Draw it!)
        state = [{},
                 {'sign':2, 'digit':3, 'dot':4},
                 {'digit':3, 'dot':4 },
                 {'digit':3, 'dot':5, 'exp':6},
                 {'digit':5},
                 {'digit':5, 'exp':6},
                 {'sign':7, 'digit':8},
                 {'digit':8},
                 {'digit':8}
                ]
        currentState = 1
        for c in s:
            flag = 'null'
            if c >= '0' and c <= '9':#c.isdigit():
                flag = 'digit'
            elif c in ('+','-'):
                flag = 'sign'
            elif c == '.':
                flag = 'dot'
            elif c == 'e':
                flag = 'exp'
            if flag not in state[currentState]:
                return False
            currentState = state[currentState][flag]
        return True if currentState in (3,5,8) else False
```

## python源码(Magic版本)
	
``` python
class Solution(object):
    def isNumber(self, s):
        """
        :type s: str
        :rtype: bool
        """
        try:
            float(s)
        except:
            return False
        return True
```

## Tips
### 1 确定有穷状态自动机-DFA
	（1）设计并定义各个状态
		二维数组或者字典数组,画出状态转移的图是key！
	（2）设计标志位和当前状态，循环遍历字符串
		根据状态转移表转移状态，最后判断状态是否正确即可。
	
### 2 单个字符的判断
	（1）isdigit（）字符串也可
	（2）c >= '0' and c <= '9'
	 
	