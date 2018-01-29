###Median of Two Sorted Arrays

There are two sorted arrays **nums1** and **nums2** of size m and n respectively.

Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).

**Example 1:**

```
nums1 = [1, 3]
nums2 = [2]

The median is 2.0

```

**Example 2:**

```
nums1 = [1, 2]
nums2 = [3, 4]

The median is (2 + 3)/2 = 2.5
```



**solution**

```python
class Solution:
    # @return a float
    def findMedianSortedArrays(self, A, B):
        l=len(A)+len(B)
        return self.findKth(A,B,l//2) if l%2==1 else (self.findKth(A,B,l//2-1)+self.findKth(A,B,l//2))/2.0
            
            
    def findKth(self,A,B,k): #在A,B两个list中 找出第k个小的数
        if len(A)>len(B): #确保A这个list是比较短的那个，这样 二分 时效率较高
            A,B=B,A
        if not A: #如果A是空，那么直接返回B[k]
            return B[k]
        if k==len(A)+len(B)-1:#如果k是最大值，那么直接在返回max(A[-1],B[-1]),因为已经sorted
            return max(A[-1],B[-1])
        i=len(A)//2 
        j=k-i
        if A[i]>B[j]:
            #Here I assume it is O(1) to get A[:i] and B[j:]. In python, it's not but in cpp it is.
            return self.findKth(A[:i],B[j:],i) #这个不太理解，递归调用？到底怎么运行的？哦 我的天哪，这真是太神奇了，真想拿脚踢作者的屁股
        else:
            return self.findKth(A[i:],B[:j],j)
"""

"""
```

**my solution**

```python
class Solution:
    def findMedianSortedArrays(self, nums1, nums2):
        """
        :type nums1: List[int]
        :type nums2: List[int]
        :rtype: float
        """
        n=len(nums1)
        m=len(nums2)
        if(n>m):
            nums1,nums2=nums2,nums1
            n,m=m,n
        if not nums1:
            return (nums2[(m+n)//2] if (m+n)%2==1 else (nums2[(m+n-1)//2]+nums2[(m+n)//2])/2)
        L1=L2=R1=R2=c1=c2=low=0
        high=2*n
        while(low<=high):
            c2=m+n-c1
            L1=(nums1[(c1-1)//2] if c1!=0 else 0)
            R1=(nums1[c1//2] if c1!=2*n else 2*n)
            L2=(nums2[(c2-1)//2] if c2!=0 else 0)
            R2=(nums2[c2//2] if c2!=2*m else 2*m)
            
            if(L1>R2):
                high=c1-1
            elif L2>R1:
                low=c1+1
            else:break
        
        return (max(L1,L2)+ min(R1,R2))/2.0
"""
没有通过最后面的那几个测试用例，也没太搞得懂这个算法，哭
这个参考下面那位博主的程序，其中不知道到底怎么回事，有点小问题

Input:
[100000]
[100001]

Output:
50001.00000

Expected:
100000.50000
"""

```

leetcode提供的[思路](https://leetcode.com/problems/median-of-two-sorted-arrays/solution/)

-------



另外参考[这位csdn博主](http://blog.csdn.net/hk2291976/article/details/51107778)

其中**分治**这个思路感觉很好，总结下来好像leetcode提供的程序也是这个思路，嗯，maybe

直接引用其中重点部分，默默感谢

> ## **割和第k个元素**
>
> 对于单数组，**找其中的第k个元素特别好做**，我们用割的思想就是：
>
> > **常识1：**如果在k的位置割一下，然后A[k]就是L。换言之，就是如果左侧有k个元素，A[k]属于左边部分的最大值。（都是明显的事情，这个不用解释吧！）
>
> # **双数组**
>
> 我们设: 
> **Ci**为第i个数组的割。 
> **Li**为第i个数组割后的左元素. 
> **Ri**为第i个数组割后的右元素。
>
> ![这里写图片描述](http://img.blog.csdn.net/20160409212629209)
>
> ## **如何从双数组里取出第k个元素**
>
> 1. 首先Li<=Ri是肯定的（因为数组有序，左边肯定小于右边）
> 2. 如果我们让L1<=R2 && L2<=R1
>
> ![这里写图片描述](http://img.blog.csdn.net/20160409212649178)
>
> 1. 那么左半边 全小于右半边，如果左边的元素个数相加刚好等于k，那么第k个元素就是Max(L1,L2)，参考上面常识1。
> 2. 如果 L1>R2，说明数组1的左边元素太大（多），我们把C1减小，把C2增大。L2>R1同理，把C1增大，C2减小。
>
> ### **假设k=3**
>
> 对于 
> [1 4 7 9] 
> [2 3 5]
>
> 设C1 = 2，那么C2 = k-C1 = 1 
> [1 4/7 9] 
> [2/3 5]
>
> 这时候，L1(4)>R2(3)，说明C1要减小，C2要增大，C1 = 1，C2=k-C1 = 2 
> [1/4 7 9] 
> [2 3/5]
>
> 这时候，满足了L1<=R2 && L2<=R1，第3个元素就是Max(1,3) = 3。
>
> 如果对于上面的例子，把k改成4就恰好是中值。



2018/1/29/23:03



