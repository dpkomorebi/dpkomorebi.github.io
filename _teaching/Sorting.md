---
title: "Sorting"
collection: teaching
type: "Computer Science"
permalink: /teaching/2022-sorting-teaching
#venue: "University 1, Department"
date: 2022-06-30
location: "City, Country"
---

We will look at some sorting problems.  I don't think they're particularly hard, but have to be careful with your logic.

Leetcode problem #2279 - Maximum Bags with Full Capacity of Rocks 
=====
[Here is the link to the problem](https://leetcode.com/problems/maximum-bags-with-full-capacity-of-rocks/)

Since we are just returning the maximum number of bags that could have full capacity after placing additional rocks, we can modify the array to our advantage.  Let's create an array, called "diff", and this array will store the difference of capacity[i] - rocks[i], i from 0 to (length of capacity) - 1. We can sort diff array from lowest to the highest. Let's create another variable called "counter", which store # of full capacity bags.  Starting from 0 index, if the diff[i] == 0, then we don't need to place additional rock so we increment count by 1 and move to the next one.   
- Time Complexity is $O(n \log n)$, since sorting costs $n\log n$ and we need to do a linear scan, which would cost us $O(n)$ in the worst case. 
- Space Complexity is $O(n)$, because we create an array called "diff." 

{% highlight python %}

class Solution:
    def maximumBags(self, capacity: List[int], rocks: List[int], additionalRocks: int) -> int:
        n = len(capacity)
        diff = [0] * n
        for i in range(n):
            if capacity[i] - rocks[i] > 0:
                diff[i] = capacity[i] - rocks[i]
        
        diff.sort()
        count = 0 
        for i in range(n):
            if additionalRocks == 0:
                return count 
            if diff[i] == 0:
                count += 1
            else:
                if additionalRocks >= diff[i]:
                    additionalRocks -= diff[i]
                    count += 1
                else:
                    return count 
        return count 
                
        

{% endhighlight %}
