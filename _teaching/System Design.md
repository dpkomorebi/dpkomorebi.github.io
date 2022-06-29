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

So the format of timestamp is "Year:Month:Day:Hour:Minute:Second", separated by ":".  Now, looking at the description of retrieve function, we notice that, if granularity is set to "Day", then we don't care about things that come next - "Hour", "Minute" and "Second".  So this tells us that we can design a list in such a way that we can sort this list based on the input of granularity.  
- We use split() method to get rid of ":" and create a list "mod_time" that stores given timestamp input in the following way 
- ["Year", "Year" + "Month", "Year" + "Month" + "Day", ... , "Year" + "Month" + "Day" + "Hour" + "Minute" + "Second"]. 
- We create a dictionary called "time" that corresponds to "mod_time".  If we are given granularity = "Day", then time["Day"] will return 2 and will sort the array "storage" (this will store both id and timestamp) using lambda function. 

I've attached a visual representation of our array "storage".  


![Visual Solution Leetcode 635](/images/Leetcode635.jpeg)


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
