# The problem
You are given an array ```prices``` where ```prices[i]``` is the price of a given stock on the ith day.

You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock.

Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return 0.

# The strategy

This problem is a classic on many coding interviews. The first instinct you probably have is to brute force it: 
* We go through each day and compare it each day that comes after. 
* We keep track of a ```maxPrice```
* If the current comparison exceeds ```maxPrice```, we have our new ```maxPrice```

This solution, however, is O(n^2) time; we'd need two for loops to compare each day to each other day. Is there a better way? The answer, of course, is yes
