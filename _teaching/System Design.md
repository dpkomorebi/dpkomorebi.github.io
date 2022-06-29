---
title: "System Design"
collection: teaching
type: "Computer Science"
permalink: /teaching/2022-systemdesign-teaching
#venue: "University 1, Department"
date: 2022-06-28
location: "City, Country"
---

Let's solve problems in System Design together. 

Leetcode Problem #635 - Design Log Storage System 
=====

[Here is the problem from Leetcode](https://leetcode.com/problems/design-log-storage-system/)


{% highlight python %}
class LogSystem:

    def __init__(self):
        
        self.storage = []
        self.time = {"Year":0, "Month":1, "Day":2, "Hour":3, "Minute":4, "Second":5}
        

    def put(self, id: int, timestamp: str) -> None:
        time = timestamp.split(":")
        mod_time = [time[0], time[0] + time[1], time[0] + time[1] + time[2], time[0] + time[1] + time[2] + time[3], time[0] + time[1] + time[2] + time[3] + time[4], time[0] + time[1] + time[2] + time[3] + time[4] + time[5]]
        self.storage.append([ id, mod_time])
        

    def retrieve(self, start: str, end: str, granularity: str) -> List[int]:
        index = self.time[granularity]
        start_time = start.split(":")
        end_time = end.split(":")
        st, lt = "", ""
        for i in range(index + 1):
            st += start_time[i]
            lt += end_time[i]
        modified_storage = sorted(self.storage,  key = lambda x : x[1][index])
        result = []
        for num in modified_storage:
            if st <= num[1][index] and num[1][index] <= lt:
                result.append(num[0])
        return result 
        

{% endhighlight %}
