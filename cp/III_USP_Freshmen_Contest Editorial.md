# III USP Freshmen Contest

[Link to Contest](https://codeforces.com/gym/101375)

## A. MaratonIME stacks popcorn buckets

Recall that 1 + 2 + 3 + ... + n = n * (n + 1) / 2.

We also dropped n - 1 candies.

Hence, the answer is just n * (n + 1) / 2 - (n - 1).

## B. MaratonIME challenges USPGameDev
Just perform the Distance Formula on the two points towards the origin and compare them.

However, be aware that when comparing floating numbers directly through == for determining whenever a draw occurs, you may not obtain an intended result. It is due to the nature of floating numbers.

To handle this, you have two options:

- Take the absolute difference between the two distances and check is the difference smaller than a small number, like 1e-5.
- Recall the Distance Formula for (x1, y1) and (x2, y2) is d = sqrt((x1 - x2)^2 + (y1 - y2)^2). We just take the square of both sides and get d^2. Now, we can compare both sides through their distance squared without any floating numbers.

## C. MaratonIME eats japanese food

Hint: Notice the constraints.

Let's say we have Q = 5000 queries, and all of them are adding plates. By iterating through all plates, the time complexity is O(0 + 1 + 2 + 3 + ... + 4999) = O(Q^2). Q^2 is 25,000,000, which is less than 10^9, a normal critical point between TLE and AC.

Hence, the solution is to use some data structures, like map, to store the coordinates and the radius.

For query A, we iterate through all plates and check are they overlapping. Assuming we want to insert a plate (x1, y1, r1) and the i-th plate is (x2, y2, r2). If the plates overlap, then (x1 - x2)^2 + (y1 - y2)^2 < (r1 + r2)^2.

For query R, we simply check does the key (coordinates) in the map exist or not, and is the associated value equals the radius.

## D. MaratonIME in the golden moment

Let's write out the answer for an array h_1, h_2, h_3, ..., h_n:

h_1 * h_2 + h_1 * h_3 + ... + h_1 * h_n + h_2 * h_3 + ... + h_2 * h_n + ... + h_(n-1) * h_n

Factorize the numbers.

h_1 * (h_2 + h_3 + ... + h_n) + h_2 * (h_3 + h_4 + ... + h_n) + ... + h_(n-1) * (h_n)

Now, the pattern is obvious. But how do we solve this in O(N)?

We iterate from i = 1 to i = n - 1, and maintain a sum (initially it is equal to the sum of the entire array).

result += h_i * (sum - h_i)

Now, we subtract the sum from h_i.

sum -= h_i

## E. MaratonIME does (not do) PAs

In my opinion, the hardest problem in this problemset.

I'll show that we can obtain the minimal answer by finishing the task in ascending completion time. We'll consider the case of n = 2, and you should be able to generalize this to all n.

![iiiuspe](https://github.com/user-attachments/assets/02ae44f7-7532-43fb-a581-7fab4e388533)

In this image, you can see that we will add the green part to the answer no matter how we order the tasks. Hence, let's now assume all tasks start from time s.

![iiiuspe2](https://github.com/user-attachments/assets/4e8e86c5-24fc-4c36-a167-636002f89bce)

WLOG, assume t1 >= t2. Notice that no matter how we order the two tasks, the second task must have a penalty of t1 + t2. Hence, it depends on how we order the first task. If we place t1 first, the result is t1 + (t1 + t2). If we place t2 first, the result is t2 + (t1 + t2).

Hence, we should sort the tasks in ascending completing time.

## F. MaratonIME educates

We first sum up all people, and divide them by 5. If the sum is not divisible, we use one more car to take them.

Hence, the answer is ceil(sum / 5).

## G. MaratonIME does a competition

Just maintain the score of 4 teams (with array or whatever), and simulate the process.

score[team] += a[i]
team = (team + 1) % n

## H. MaratonIME gets candies

Doesn't this look familiar? It's just your favorite algorithm - binary search!

log_2(1e9) = 30, which is far less than 50.

Double check the edge cases, flush the output, and you should be fine.

## I. MaratonIME divides fairly

Assume sum is even.

A fair division occurs iff a = b.

Assume sum is odd.

A fair division occurs iff |a - b| == 1

Hence, if the division isn't fair, the result is (sum / 2) and (sum / 2 + sum % 2).

## J. MaratonIME goes to Mito

Notice when c_i = M, the answer must be No.

Otherwise, maintain a 2D array initialized by 1, to denote the walkable space. For each tree, simply add itself and its surrounding for a total of 6 (unless it's at the corner).

Now, maintain a 2D visited_yet array and perform flood fill (BFS) on the graph.

Here, notice 2 things:

- You should start from all available squares on the first column
- DFS will lead to TLE. Consider an empty grid. There are a lot of possible paths, hence BFS is a better choice.

## K. MaratonIME bot

I will describe the solution for C++. It potentially requires more handling for other languages.

A word is defined as spaces surrounding it (or for the last word, excluding the symbol).

We can use while(cin >> str) to keep reading each word. Maintain a flag that whenever Sussu occurs. After EOF, the while loop is broken and str has the last word. Check is it a question, and if it is not, check the flag of Sussu, and is the last word Sussu#, where # is the symbol.

## L. MaratonIME doesn't like odd numbers

Recall odd + odd = even, even + even = even, and odd + even = odd.

Hence, we will take all even numbers, and take an even number of odd numbers. To do this, just place the odd numbers in an array, sort it in descending order (as we prioritize taking the maximum), and get an even number of odd numbers.

## Conclusion
The difficulty was a bit easy, but it's reasonable.

Solved: 12 / 12

Ranking: 19 / 960 (20-2-2025)
