---
title: Election Simulator
nav_order: 6
has_children: true
has_toc: false
summary: Due Nov 12
---

# Election Simulator
{: .no_toc .mb-2 }

Winning the Electoral College with the minimum popular votes.[^1]
{: .fs-6 .fw-300 }

[^1]: Keith Schwarz. 2020. Recursion to the Rescue! In Nifty Assignments 2020. <http://nifty.stanford.edu/2020/schwarz-recursion-to-the-rescue/>

The President of the United States is not elected by a popular vote, but by a majority vote in the Electoral College. Each state, [plus DC](https://en.wikipedia.org/wiki/Twenty-third_Amendment_to_the_United_States_Constitution), gets some number of electors in the Electoral College, and whoever they vote in becomes the next President. Right before the 2016 election, [NPR reported](https://www.npr.org/2016/11/02/500112248/how-to-win-the-presidency-with-27-percent-of-the-popular-vote) that 23% of the popular vote would be sufficient to win the election, based on the 2012 election data. They arrived at this number by looking at states with the highest ratio of electoral votes to voting population. This was a correction to their originally-reported number of 27%, which they got by looking at what it would take to win the states with the highest number of electoral votes. But the optimal strategy turns out to be neither of these and instead uses an unlikely coalition of small and large states.

{% assign module = site.modules | where: 'title', page.title | first %}
{{ module }}

Assuming the following simplifications, what's the fewest number of popular votes needed to win the presidency in each election year since 1828?

1. A simple majority of the popular votes in a state will win all of the state's electors. For example, in a small state with 999,999 people, 500,000 votes will win all its electors.[^2]
1. A majority of the electoral votes is needed to become president. In the 2008 election, 270 votes were needed because there were 538 electors. In the 1804 election, 89 votes were needed because there were only 176 electors.[^3]
1. Electors never defect.[^4]

[^2]: In most states, a [plurality suffices](https://en.wikipedia.org/wiki/United_States_presidential_election_in_Michigan,_2016) to win the electors, and some states [split their electoral votes in other ways](https://en.wikipedia.org/wiki/United_States_presidential_election_in_Maine,_2016).
[^3]: Technically, it's possible to [win the presidency without winning the Electoral College](https://en.wikipedia.org/wiki/Twelfth_Amendment_to_the_United_States_Constitution).
[^4]: The electors in the Electoral College are [free to vote for whomever they please](https://en.wikipedia.org/wiki/Faithless_electors_in_the_United_States_presidential_election,_2016) but the expectation is that they'll vote for the candidate that won their home state.

Note
: The historical election data here was compiled from a number of sources. In many early elections, state legislatures chose electors rather than voters so in some cases we estimated the voting population based on the overall US population at the time and the total fraction of votes cast. This may skew some of the earlier election results. However, to the best of our knowledge, data from 1868 and forward is complete and accurate. Let us know if you find any errors in the data!

## Specification

Implement an `ElectionSimulator` class that can compute the minimum number of popular votes needed to win the Electoral College given the turnout during an election year.

`ElectionSimulator(List<State> states)`
: Constructs a new `ElectionSimulator` for the given list of `states`.

`Set<State> simulate()`
: Returns the set of states with the minimum number of popular votes needed to win the election.

An `ElectionSimulator` class implemented using pure recursive backtracking will be too slow to run on large elections. As an example, all 50 states, plus DC, participated in the 2016 election. That means that there are 2<sup>51</sup> possible subsets to explore when trying to find the optimal combination. Unfortunately, 2<sup>51</sup> is 2,251,799,813,685,248, which is such a huge number that even checking a billion combinations each second would take about a month to process.

One way to speed up the process is to avoid re-simulating election subproblems that have already been computed. In the 2016 election, the threshold for electoral votes needed to win the presidency was 270, so there are at most only 271 · 52 = 14,092 unique combinations that need to be computed. Use the provided `Memo` class to memoize (save) each unique combination to speed up the `ElectionSimulator`.

Design your recursive backtracking method to represent these subproblems by including two parameters: the current electoral vote threshold and the current index into the list of states. Our task is to solve the following **constrained optimization** problem: "What is the coalition of states that minimizes the popular vote while satisfying the electoral vote threshold and using only states at or after the given index?"

## Web app

To launch the web app, **Open Terminal** <svg class="inline-icon" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 82" fill-rule="evenodd" stroke-linejoin="round" stroke-miterlimit="2" id="terminal"><path d="M44.518 70.139H100v11.097H44.518z"></path><path d="M7.845 73.347L0 65.502l28.826-28.828L0 7.845 7.845 0l36.673 36.674L7.845 73.347z" fill-rule="nonzero"></path></svg>, paste the following command, and press Enter.

```sh
javac Server.java && java Server; rm *.class
```

Then, open the **Network** <svg class="inline-icon" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 71" fill-rule="evenodd" stroke-linejoin="round" stroke-miterlimit="2" id="wifi"><path d="M0 20.693l9.091 9.091c22.592-22.592 59.225-22.592 81.818 0L100 20.693c-27.593-27.59-72.363-27.59-100 0zm36.364 36.364L50 70.693l13.637-13.637c-7.502-7.545-19.727-7.545-27.273.001zM18.182 38.875l9.091 9.091c12.544-12.544 32.91-12.544 45.455 0l9.091-9.091c-17.544-17.545-46.046-17.545-63.637 0z" fill-rule="nonzero"></path></svg> dropdown and select host 0.0.0.0:8000.

## Grading

**Mark** the program to submit it for grading. In addition to the automated tests, the final submission will also undergo code review for [internal correctness]({{ site.baseurl }}{% link quality/index.md %}) on comments, variable names, indentation, data fields, and code quality.
