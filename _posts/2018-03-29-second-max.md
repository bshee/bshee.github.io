---
layout: post
title: Second Max
# date: 2018-03-29 19:45:00 -0700
categories: blog
language: python
tags: python
---
{% highlight python %}
def second_max(numbers):
    if len(numbers) < 2: return None
    top = numbers[:2]
    if top[0] == top[1]:
        top[0] = None
    elif top[0] > top[1]:
        top[0], top[1] = top[1], top[0]
    for number in numbers[2:]:
        if number != top[1] and (top[0] == None or number > top[0]):
            top[0] = number
            if top[0] > top[1]: top[0], top[1] = top[1], top[0]
    return top[0]
{% endhighlight %}

The defined function takes a list of numbers and returns the second max or `None` if it does not exist. The list can contain duplicates.

This problem is essentially a small twist on the **find the max** of a list. A naive approach may be to first remove any duplicates, e.g. converting the list to a set and then back to a list, and sorting the list in descending order to return the second element. Here, we take a longer approach in terms of lines of code, but we find the solution in one iteration through the `numbers`.

Let's break down the code.

First, we take care of case where `numbers` is a small list, so a second max would always be `None`.

The star of this function is the `top` list. There are two conditions we want to enforce in `top`:
1. `top` contains the two distinct max values that we have found so far
2. `top` is sorted in ascending order, so that the first element of `top` is the second max found so far

After assigning `top` to the first two elements of `numbers`, we enforce these two conditions in the `if` checks. Specifically, `top[0]` should be `None` to handle an edge case where `numbers` starts off with the same two values. Otherwise we swap the two values in `top` if needed.

The rest of `numbers` is iterated through with a `for` loop on `numbers[:2]`. We need to make sure the iterated number is not a duplicate of our current max, `top[1]` to satisfy the first condition. To satisfy the second condition, `top` will accept the iterated number if we have not found a second max yet (`top[0] == None`) or if the number found would replace the second max due to being larger. Once accepted, we need to do a bit of housekeeping to make sure `top` is still sorted.

Some closing notes:
1. The code to solve this problem in a linear fashion is much more complex than it would be to just find the max.
1. Swapping values in Python neatly utilizes tuples and unpacking.
1. Extending the code to solve the more general find the *nth* max would require sorting `top`.
