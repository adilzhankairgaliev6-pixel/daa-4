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

Mission 2. How is the longest common subsequence different from the longest common substring? My Shared core is bigger than the number of letters that are the same at the same place: why?

Mission 3. What does the prefix function tell you, and why does the pointer in the text never go back in KMP? What is the Border length of my marker and what does it mean?

Mission 4. Why must you compare the letters after the hashes are equal? What happens to the cost of Rabin-Karp if many windows have the same hash?

Mission 5. What are the two states of a person in your DP, and how do you get the answer for a person from its children? Why does a greedy "test the person with most links first" not always give the cheapest answer?

## AI use

The syllabus requires you to say which AI tools you used and for what. Write the tool (ChatGPT, Copilot, other) and what you asked it: explain an idea, find an error, review code. Write "none" if you did not use any. If you took code or text from a book or a website, give the source here.

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
