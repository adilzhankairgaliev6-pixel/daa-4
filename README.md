# Assignment 4. Patient Zero

Student ID:251988
Name:Adilzhan Kairgaliyev
Group:SE-2540

This file is the report. Fill it in as you go. How to start: `START_HERE.md`. The task: `docs/Assignment4.pdf`.

## Program output

The 9 lines your program prints on your data (`java -cp out Main`):

    Mutations:85
    Shared core:1022
    Marker hits:5
    First hit:5315
    Border length:4
    Shared words:418
    Tests needed:42
    Cheapest testing:171
    Longest chain:28

My outbreak report (a screenshot of `output/outbreak.html`):

![outbreak](output/outbreak.png)

## Questions

Answer in your own words, two or three sentences each.

Mission 1. What does the cell d[i][j] of your table mean, and how is it computed from other cells?
The cell d[i][j] represents the minimum number of edits required to transform the first i characters of the first strain into the first j characters of the second. I calculate this value based on neighboring cells by taking the minimum cost among three possible options. Each edit has a cost of 1; however, if the characters are identical, the diagonal transition incurs no additional cost.

Mission 2. How is the longest common subsequence different from the longest common substring? My Shared core is bigger than the number of letters that are the same at the same place: why?
A substring consists of consecutive characters, whereas a subsequence consists of characters that appear in the same relative order, though they need not be consecutive. My "shared core" metric accounts for more than just identical characters in the same positions, because insertions and deletions can cause the sequences to shift relative to one another. The shared characters remain in the same order but end up in different positions and the Longest Common Subsequence (LCS) algorithm is still able to identify them.

Mission 3. What does the prefix function tell you, and why does the pointer in the text never go back in KMP? What is the Border length of my marker and what does it mean?
For each position in the pattern, the prefix function indicates the length of the longest prefix that matches a suffix ending at that position. The pointer in the text never moves backward; when a mismatch occurs, I simply shift back within the pattern using the table, while continuing to advance through the text. The border length of my pattern is 4, which means that after a full match, I shift back by 4 characters rather than returning to 0 this allows for the detection of overlapping occurrences.

Mission 4. Why must you compare the letters after the hashes are equal? What happens to the cost of Rabin-Karp if many windows have the same hash?
Different words can end up with the same hash because there are fewer possible hash values ​​than there are words. Therefore, when hashes match, I compare the actual letters; otherwise, I might count false positives. If there are many identical hashes, I have to perform letter-by-letter comparisons frequently, and the algorithm—which should ideally run in fast, linear time can, in the worst case scenario, become slow, performing much like a naive search.

Mission 5. What are the two states of a person in your DP, and how do you get the answer for a person from its children? Why does a greedy "test the person with most links first" not always give the cheapest answer?
A person can be in one of two states: either they are checked, or they are not. If they are checked, the cost for that branch is the person’s own cost plus the optimal cost for each of their children. If they are not checked, then every one of their children must be checked; otherwise, some connections would remain unchecked. A greedy approach prioritizing the person with the most connections is not always optimal: in a chain of three people with costs 1, 10, and 1, a greedy strategy would select the middle person, at a cost of 10, whereas it would be cheaper to check the two people at the ends, at a total cost of 2.

## AI use

I used Claude (Anthropic) while working on this assignment. AI helped me fix my Java setup (the old Java 8 vs JDK 25 problem, PATH, running tools/Check.java), and with Git and GitHub (creating the repository, push errors, merging after I edited the README on GitHub). Claude explained edit distance, LCS, the prefix function and KMP, Rabin-Karp with a rolling hash, and the DP on a tree, step by step, with small examples. Claude pointed out mistakes in my steps and in how I ran things.

## Timing (Mission 7)

Milliseconds, average of 3 runs, from `java -cp out Bench`.

| test | size | time |
|---|---|---|
| naive search | 20 000 / 40 000 / 80 000 |108,5 / 162,3 / 374,8|
| KMP | 20 000 / 40 000 / 80 000 |3,7 / 1,1 / 0,7|
| edit distance | 500 / 1000 / 2000 / 4000 |9,2 / 12,2 / 37,4 / 150,5|

What do the numbers say about how the time grows? When you double the size, by how much does each time grow? Two or three sentences.

## Complexity

n is the length of the text (or of a strain), m the length of the pattern, k the length of the window, v the number of people. Fill in every algorithm you wrote.

| algorithm | time | space | assumptions |
|---|---|---|---|
| Edit distance |O(n*m)|O(n*m)|(n+1)×(m+1) table, cell testing in O(1)|
| LCS |O(n*m)|O(n*m)|the same, max/diagonal rule|
| Prefix function and KMP |O(n+m)|O(m)|the pointer in the text does not go back, the rollbacks in total are no more than n|
| Rabin-Karp (shared words) |O(n+m)|O(m)|The hash is updated in O(1) time; if there are many identical hashes, comparing the characters can take up to O(n·k) time.|
| Tree DP |O(v)|O(v)|Each person and each connection is visited once.|

## Before you submit

- The four files in `data` and the screenshot `output/outbreak.png` are in the repository.
- `java tools/Check.java` shows all examples right.
- This README is filled in, the program output and the section AI use included.
- The work is pushed to main (at least one commit per mission) and the repository is public.
- The link is attached in Moodle.
