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
