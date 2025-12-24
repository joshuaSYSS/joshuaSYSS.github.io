# IIMOC 2025 Blog
The International Invitational Math Optimization Challenge (IIMOC) 2025 is a global competition focused on mathematics and computer science. Each team is assigned a challenging yet ultimately unsolvable optimization problem and has four weeks to submit its best solution. The team with the lowest loss wins, and special awards are presented for creativity and the most effective approach.

This year, I invited YAN Yachao to team up with me for this challenge, and we formed the team [Kui Wong Fan Club](https://iimoc.org/teams.html?team=Kui%20Wong%20Fan%20Club), which amusingly misspelled my name. The contest started on November 22nd and ended on December 21st.

## Permutation
On November 27th, after forming the team, I decided to tackle the sample problem while YAN Yachao prepared for the ICPC Hong Kong regional contest. The problem is interactive and requires finding a hidden permutation by asking a series of questions.

Initially, I wrote a simple brute force solution that involved the following steps: First, I determined where `n` was located, then for each number from `1` to `n-1`, I tried each index and made a guess. Unsurprisingly, this approach placed us among the lowest scores on the leaderboard.

Next, I made a few minor optimizations:
1. Reduced the range of numbers to be queried from `n` to `n-1`, since the last number only has one candidate index and doesn't need to be queried.
2. Queried only the indices that were unknown.
3. When finding the index of `n`, I paired it with `1` for querying. Thus, instead of using `n` for subsequent guesses, we simply used `1` or `n`, depending on which number's index was determined first.

However, these optimizations had a limited impact on reducing the number of queries. The primary improvement needed was to find each integer more efficiently. I implemented a binary search approach. We first found `1` or `n` normally, and then, using that number along with some case handling, we could infer the remaining `n-2` integers. The final integer could then be deduced. This became my final solution, although I recognized that the method for finding `1` or `n` could be further optimized if I were more motivated.

## Packing the Polyominoes
On December 1st, I decided to start working on the official problem independently, with plans to collaborate with YAN Yachao later. At first glance, this problem seemed simple, but turned out to be quite tricky. After some queries with Gemini, we concluded that the problem could be reformulated as a Rectangle Packing issue, which is a well-known NP-hard problem. I reviewed several papers on this topic and shared them with Gemini for coding. Our solution included the following steps:
1. Set the width of our final rectangle to the square root of the total number of cells.
2. Rotate all polyominoes to achieve the "flattest" orientation.
3. Place each polyomino one by one according to its height.

We achieved a decent score, but it was still in the 1 million range, a significant distance from the top participants who scored around 2 million. During this process, I made a few critical optimizations, which helped us close the gap:
1. Instead of fixing a width, we searched for the best solution around the square root of the total number of cells.
2. We switched to the Skyline algorithm, which is reminiscent of dropping Tetris blocks, but we modified it to drop blocks in a way that minimizes the y-coordinate.
3. We merged the smallest and largest sqrt(n) polyominoes to see if the smaller one could fit within the rectangle of the larger one.

On December 2nd, I continued refining this solution. However, after experimenting with various optimizations, I realized that considering each shape merely as a rectangle limited our potential. With Gemini's help, we adjusted the Skyline algorithm to drop shapes more intelligently by allowing them to move down one cell at a time if possible. This led to a significant score increase, from 1,367,526 to 2,020,664. This validation confirmed my belief that better solutions should consider each shape in its entirety, rather than simply as rectangles. 

Further optimizations included:
1. After dropping a shape, check if it can be moved left or right to utilize more space.
2. Evaluating all eight configurations of the shape to determine which orientation resulted in the lowest y-coordinate.

In the evening, YAN Yachao and I met to discuss my progress. I also mentioned a concept I had been pondering: a smooth surface. While optimizing the code, Gemini had proposed a smooth Skyline algorithm, but the resultant score was inferior to our previous results. Nevertheless, I felt the idea had merit; we needed to craft a smoother surface. He suggested another optimization: to ensure that the surface was smooth (reducing the sum of differences between adjacent surface cells) while also minimizing "waste" cells (where empty space is directly above a filled cell). Therefore, in the Skyline algorithm, instead of simply placing it in a location that reduces the y-coordinate, we can also combine these few elements into it. At last, we place the polyomino that minimizes the following:<br>
L = (y-coordinate) * 10 + (waste cells) * 5 + (smooth) * 2<br>
After implementing this formula, we obtained a score of 2367501.

On December 3rd, I thought to myself that this formula can be fine-tuned, as we simply made up some numbers. After some tuning, we finally reached 2423104, which is very close to the top participant's score of 2435686.

On December 4th, I continued to fine-tune the parameters for searching the best solution for each width in the Skyline algorithm. The score indeed increased, but I feel that this solution is too close to the time limit for it to pass all system tests, as the extreme case, Case 19, ran for 4732ms, with only cells = 96958 and K_max = 7. I may increase this width jump margin before we submit the final solution, in case we still decide to use this algorithm at the end.

On December 13th, the best score on the leaderboard was updated and improved by almost 100000, which showed that there is still potential for improvement. I increased the jump margin width for extreme cases, but lowered the jump margin width as the search width decreases. Our score increased by around 80000.

On December 17th, I suspect that the email sent by the organizer caused many teams to attempt this problem again, as the number of submissions increased significantly compared to the past few days, and we dropped to 7th place. I decided to continue setting up more cases for the jump margin, and we've finally surpassed the 244,000 mark.

The result of the contest has been released on December 24th. We have secured the 8th place out of 209 teams. The score can definitely be improved, as I played with Simulated Annealing before the deadline of the contest, and it returned a decent score (although the program exceeded the time limit).
