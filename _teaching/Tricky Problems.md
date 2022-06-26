---
title: "Tricky Problems"
collection: teaching
type: "Computer Science"
permalink: /teaching/2022-trickyproblems-teaching
#venue: "University 1, Department"
date: 2022-06-25
location: "City, Country"
---

This section contains Leetcode problems that are a bit more general than problems we have encountered so far.  In other words, there are many methods to solve problems efficiently.  

Leetcode Problem #744 - FInd the Smallest Letter Greater than Target 
=====

[Here is the problem](https://leetcode.com/problems/find-smallest-letter-greater-than-target/)

So I didn't get this problem in a single try.  I forgot about the fact that the letters wrap around for this problem.  So, if target is "z" and our letters is ["a","b"].  Then the answer is "a".  We will use binary search. 
- As usual, we will use mid = low + (high - low ) // 2 to prevent overflowing happening. Also, low and high will be 0 and len(letters) - 1 respectively. 
- Now, since we are looking for the smallest character in the array that's larger than target, we have to use "if target >= letters[low]" (pay attention to the greater than or equal to inequality). Try the case with strict inequality for a test case of ["c", "f", "j"] with target letter "c".  You will get time limit exceeded. 
- Next, when we exit the While loop of our binary search, we have to do a bit more postprocessing work for this problem, because of that wrapping. Let's consider a test case, where we have ["c", "f", "j"] for an array, letters, and target letter of "j".  The expected answer is "c", since we are essentially dealing with an array like this ["c", "f", "j", "c", "f", "j", ... ].  (I know.. this problem is not exactly my favorite problem).  So if we simply return letters[low], then we get "j" instead of "c".  How do we deal with this?  If low == len(letters) - 1 (in other words, when low is pointing at the last index), that's the case where we have to be a bit careful. So if low == len(letters) - 1 is True, then we have to check whether (1) target is greater than or equal to the last element of this letters.  If True, then we return the FIRST element of the array letters (letters[0]).  (2) If target is less than the last element of the array, we return the last element ( try letters = ["c", "f", "j"] with target "g".  The answer we want is "j"). 

![Visual Solution Leetcode 744](/images/Leetcode744.jpeg)

Below is the code. 
{% highlight python %}

class Solution:
    def nextGreatestLetter(self, letters: List[str], target: str) -> str:
        low, high = 0, len(letters) - 1
        
        while low < high: 
            mid = low + (high - low) // 2
            if letters[mid] <= target:
                low = mid + 1
            elif letters[mid] > target:
                high = mid

                
        if low == len(letters) - 1:
            if target >= letters[low]:
                return letters[0]
            else:
                return letters[-1]
        else:
            return letters[low]
        

{% endhighlight %} 

Leetcode Problem #1423 - Maximum Points You Can Obtain from Cards 
=====
[Here is the problem](https://leetcode.com/problems/maximum-points-you-can-obtain-from-cards/)


