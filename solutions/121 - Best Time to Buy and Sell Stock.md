# The problem
You are given an array ```prices``` where ```prices[i]``` is the price of a given stock on the ith day.

You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock.

Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return 0.

# The strategy

This problem is a classic on many coding interviews. The first instinct you probably have is to brute force it: 
* We go through each day and compare it each day that comes after. 
* We keep track of a ```maxPrice```
* If the current comparison exceeds ```maxPrice```, we have our new ```maxPrice```

This solution, however, is O(n^2) time; we'd need two for loops to compare each day to each other day. Is there a better way? The answer is yes.

Whenever you have to compare an element to its other elements in an array or list, you should think of the **two-pointers** technique. This is a technique that lets us compare two elements in one loop. So, what we once needed *two* for loops to accomplish, we can now accomplish with *one*.

The **two-pointers** techinique has two components:
* The iterating pointer. This is the pointer that will iterate across each element in the list like normal
* The sliding pointer. This is the pointer that we will use to grab values to compare to

# The solution

Our code will start with two pointers:
```
pointer_one = 0
pointer_two = 1
```
`pointer_one` will be our sliding pointer, and `pointer_two` will be our iterating pointer. As we go through the list comparing, we need a variable to keep our highest result in:
```
maxProfit = 0
```
Now, as we go through our list we want to compare our iterating and our sliding pointer:
```
for i in range(1, len(prices)):
    if (prices[pointer_two] - prices[pointer_one] > maxPrice):
        maxPrice = prices[pointer_two] - prices[pointer_one]
    pointer_one += 1
```
So far with this code, we haven't slid our sliding pointer at all. So, all it effectively accomplishes is comparing each item to the first item.

The question is, how do we know when to slide our sliding pointer? Think about our goal: we're looking the maximum difference in the two pointers. That means the comparisons we're looking for are ones where `pointer_two` is the highest and `pointer_one` is the lowest. 

We're already finding the highest `pointer_two` by sliding it over each element of the list. But how do we find the lowest for `pointer_one`? Well, `pointer_two` is already doing the iterating for us. That means we can **piggyback** `pointer_one`'s search off of `pointer_two`'s. If `pointer_two` finds a new lowest, we simply move `pointer_one` to that location. 

Let's update our for loop to do that:
```
for i in range(1, len(prices)):
    if (prices[pointer_two] - prices[pointer_one] > maxPrice):
        maxPrice = prices[pointer_two] - prices[pointer_one]
    
    if (prices[pointer_two] < prices[pointer_one]):
        pointer_one = pointer_two
    
    pointer_two += 1
```

And just like that, we're able to do two searches for the price of one for loop. 

Putting it all together, our final solution is:

```
def maxProfit(self, prices: List[int]) -> int:
    maxProfit = 0

    # Two pointers method
    pointer_one = 0
    pointer_two = 1

    for i in range(1, len(prices)):
        if (prices[pointer_two] - prices[pointer_one] > maxProfit):
            maxProfit = prices[pointer_two] - prices[pointer_one]

        if (prices[pointer_two] < prices[pointer_one]):
            pointer_one = pointer_two

        pointer_two += 1

    return maxProfit
```
