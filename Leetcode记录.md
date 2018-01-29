##Leetcode记录



### 1. Two Sum

Given an array of integers, return **indices** of the two numbers such that they add up to a specific target.

You may assume that each input would have **exactly** one solution, and you may not use the *same* element twice.

**Example:**

```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,

return [0, 1].

```

**solution**

```python
class Solution(object):
    def twoSum(self, nums, target):
        if len(nums) <= 1:
            return False
        buff_dict = {}
        for i in range(len(nums)):
            if nums[i] in buff_dict:
                return [buff_dict[nums[i]], i]
            else:
                buff_dict[target - nums[i]] = i
```



**my solution**

```python
#方法一：
	class Solution(object):
    def twoSum(self, nums, target):
        for i in range(len(nums)):
            for j in range(i+1,len(nums)):
                if (nums[i]+nums[j]==target):
                    return [i,j]
                else:
                    continue
#我这就很lowB了
'''
提交后最后一个测试用例未通过，显示运行时间过长，算法效率太低，辣鸡代码
'''

#方法二：
class Solution(object):
    def twoSum(self, nums, target):
        if len(nums)<=1:
                return False
        for i in range(len(nums)):
            buff = target - nums[i]
            if buff in nums[i+1:]:
                index = i+nums[i+1:].index(buff)+1  # 此处本来是直接index=nums[i+1:]，有个测试用例为([3,3],6),这种情况会return [0,0]，答案错误。
                return [i,index]
'''
这个测试通过了，主要思路就是用target减去目前的数，再看此数是否在剩下的nums[i+1:]里面
'''
```





### 2. Longest Substring Without Repeating Characters

Given a string, find the length of the **longest substring** without repeating characters.

**Examples:**

Given `"abcabcbb"`, the answer is `"abc"`, which the length is 3.

Given `"bbbbb"`, the answer is `"b"`, with the length of 1.

Given `"pwwkew"`, the answer is `"wke"`, with the length of 3. Note that the answer must be a **substring**, `"pwke"`is a *subsequence* and not a substring.

**my solution & solution**

```python
'''
这题不太会，看discuss里面别人答案做的
'''
def lengthOfLongestSubstring(self, s):
    """
    :type s: str
    :rtype: int
    """
    start = maxlength = 0 #初始化头和maxlength
    dic = {} #dict 用于保存 每个字符 对应的 索引序号
    for i,ch in enumerate(s):
        if ch in dic and start<=dic[ch]: 
          #注意，后面那个判断条件 在例如p****p**时起作用，不知道怎么描述
            start = dic[ch] + 1
        else:
            maxlength = max(maxlength, i - start + 1) #窗口大小可能会变得比maxlength小，所以不能直接用maxlength= i-start+1，注意
        dic[ch] = i
    return maxlength
  
```
**Leetcode 提供的思路[在这](https://leetcode.com/problems/longest-substring-without-repeating-characters/solution/)**



*****

一天看两题，还是抄的，凉透了真是2018/1/28/23:16

![img](file:///D:\QQData\885200181\Image\C2C\F3D427E38D8A481180EC444474806E09.png)

:family_man_girl:want a GF like llj wuwuwu...

********







