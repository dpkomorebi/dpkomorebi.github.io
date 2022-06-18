---
title: "Binary Search"
collection: teaching
type: "Computer Science"
permalink: /teaching/2022-binarysearch-teaching
#venue: "University 1, Department"
date: 2022-06-15
location: "City, Country"
---

Let's first talk about "Binary Search".  Just to be clear, in data structure, we also have "Binary Search Tree".  In Leetcode problems, a lot of seemingly hard problems can be solved efficiently (time complexity and space complexity wise) by Binary Search.  Beccause the time complexity of Binary Search is  $\quad O(\log n) $.  For instance, if we have an array of length $\quad 2^{31} -1 $, then Binary Search will only traverse 31 times to find the number we want. Imagine how long it will take from a linear scan !  The most difficult part using Binary Search to solve problems is (1) when to use Binary Search and (2) if we can use it, how to transform the original problems into forms that we can easily visualize solutions using Binary Search.  While the concept behind Binary Search is simple, writing a bug free algorithm is rather tricky.  Let's take a look at a Leetcode problem. 

Leetcode Problem #704 - Binary Search
=====

{% highlight python %}

def BinarySearch(nums, target):
    # nums is an array and target is a number we hope to find. If the target exists, then we return its index number 
    # If the number doesn't exist, we return -1 

    # nums must be sorted.  If nums is not sorted, we sort it first.

    low, high = 0, len(nums) - 1

    while low < high:
        mid = low + (high - low) // 2
        # To prevent overflow

        if nums[mid] < target:
            # In this case, our search space lies to the right portion of mid.
            low = mid + 1
        elif nums[mid] > target : 
            high = mid 
        else:
            return mid 
    # if we can't find the number, we return -1 
    if nums[low] == target: 
        return low
    else:
        return -1 

{% endhighlight %}

Graphical explanation of Binary Search. 

![Swiss Alps](/images/Binary_search_1.jpeg)

In addition to the overflow problem, you have to be careful about the condition in the While loop. Here, we have strictly less ( low < high).  In some cases, you may see (low <= high).  If you use "low <= high" in the code above and do not modify anything else, this code will not return the answer (or get stuck in the loop).  So, if the condition in the while loop is (low <= high), then the following code works. Notice that we have "high = mid + 1" instead of "high = mid". 

{% highlight python %}
def BinarySearch(nums, target):
    # nums is an array and target is a number we hope to find. If the target exists, then we return its index number 
    # If the number doesn't exist, we return -1 

    # nums must be sorted.  If nums is not sorted, we sort it first.

    low, high = 0, len(nums) - 1

    while low <= high:
        mid = low + (high - low) // 2
        # To prevent overflow

        if nums[mid] < target:
            # In this case, our search space lies to the right portion of mid.
            low = mid + 1
        elif nums[mid] > target : 
            high = mid - 1 
        else:
            return mid 
    # if we can't find the number, we return -1 
    return -1 

{% endhighlight %}


======

Leetcode Problem #33 - Search in Rotated Sorted Array. 
======

[Here is the problem.  ](https://leetcode.com/problems/search-in-rotated-sorted-array/)
Well, since the time complexity for this problem must be in $O(\log n)$, we can use Binary Search.  However, we have rotation happening in this array.
My approach was a bit more intuitive than the model solutions in the problem.  We use Binary Search to find the rotation index.  


Leetcode Problem #702 - Search in a Sorted Array of Unknown Size 
======

[Here is the problem.](https://leetcode.com/problems/search-in-a-sorted-array-of-unknown-size/)
This one isn't that much different from the previous problem.  The difference is that we have an array of unknown size.  However, the solution for this problem is very similar to the one we have seen so far.  So what are our "low" and "high"?  "low" would be 0.  How about "high"?  We can use While loop to find a reasonable value of "high".  See the code below for an implementation.  

{% highlight python %}

class ArrayReader:
   def get(self, index: int) -> int:

class Solution:
    def search(self, reader: 'ArrayReader', target: int) -> int:
        low = 0
        # let's find high
        high_val = reader.get(0)
        high = 1
        while high_val < target:
            high = high * 2
            high_val = reader.get(high)
        
        
        def BinarySearch(low, high):
            
            while low < high:
                mid = low + (high - low) // 2
                mid_value = reader.get(mid)
                if mid_value < target:
                    low = mid + 1
                elif mid_value > target:
                    high = mid
                else:
                    return mid
            if reader.get(low) == target:
                return low
            else:
                return -1
            
            # This is another version of Binary Search
            # while low <= high:
            #     mid = low + (high - low) // 2
            #     mid_value = reader.get(mid)
            #     if mid_value < target:
            #         low = mid + 1
            #     elif mid_value > target:
            #         high = mid - 1
            #     else:
            #         return mid
            # return -1
        
        return BinarySearch(0, high)

{% endhighlight %}

Leetcode problem 
=====
