---
title: "Random Problems"
collection: teaching
type: "Computer Science"
permalink: /teaching/2022-randomproblems-teaching
#venue: "University 1, Department"
date: 2022-06-22
location: "City, Country"
---

This section contains Leetcode problems that are a bit more general than problems we have encountered so far.  In other words, there are many methods to solve problems efficiently.  

Leetcode Problem #2098 - Subsequence of Size K with the Largest Even Sum 
=====

[Here's the problem](https://leetcode.com/problems/subsequence-of-size-k-with-the-largest-even-sum/)

How should we solve this problem? 
First, we can sort this array from the largest to the lowest. In some problems, sorting an array is not an ideal starting point (i.e. finding an index position of some numbers).  However, in this case, we are only interested in returning the largest even sum of subsequence with length k.  Because we are dealing with a subsequence, we can sort this array first.  
- Now, for whatever subsequence of length k, we must have an even number.  How do we get an even number?  There are two cases :  Even + Even = Even and Odd + Even = Even.  Thus, after sorting an array, if the k largest numbers add up to an even number, we simply return this number.  Otherwise, this means the sum of k largest numbers is odd.  How do you get an odd number?  It is Odd + Even = Odd.  Thus, either (1) We have to swap Odd with Even or (2) swap Even with Odd number. 
- What do I mean by this? Let's say we sorted the array from the largest to the lowest. Assume that the sum of k largest elements is odd number.  Then let's find the lowest even and odd numbers among the k largest elements.  Let's denote them lowest_even and lowest_odd.  Next, from k+1th element (in Python, our for loop will start from k), we will swap these numbers in the following way :  if, say, k+1th element is even, then we (1) check first whether the lowest_odd exists.  If lowest_odd exists, then we will swap lowest_odd with k+1th element. Then we update our sum (in my code, this sum is denoted by result).  

{% highlight python %}

class Solution:
    def largestEvenSum(self, nums: List[int], k: int) -> int:
        nums.sort(reverse = True )
        sum_k = sum(nums[:k])
        
        if sum_k % 2 == 0:
            return sum_k 
        
        lowest_even = float("inf")
        lowest_odd = float("inf")
        
        highest_even = 0
        highest_odd = 0 
        
        for i in range(0, k):
            if nums[i] % 2 == 0:
                lowest_even = min(lowest_even, nums[i])
            else:
                lowest_odd = min(lowest_odd, nums[i])
        result = -1 
        for i in range(k, len(nums)):
            if nums[i] % 2 == 0 and lowest_odd != float("inf"):
                result = max(result, sum_k - lowest_odd + nums[i])
            elif nums[i] % 2 == 1 and lowest_even != float("inf"):
                result = max(result, sum_k - lowest_even + nums[i])
        return result 



{% endhighlight %}
