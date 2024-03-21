[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-24ddc0f5d75046c5622901739e7c5dd533143b0c8e959d652212380cedb1ea36.svg)](https://classroom.github.com/a/IF3rQO50)
# Quicksort Pivots

in the lectures I only briefly mentioned strategies for determining a good pivot
for quicksort. The implementation on the slides simply picks the leftmost
element in the part of the array that we consider as a pivot. I also mentioned a
few other ways of picking a good pivot, e.g. randomly.

Median-of-three is also a good way of picking a pivot -- inspect the first,
middle, and last elements of the part of the array under consideration and
choose the median value. Using the probabilities for picking a pivot in a
particular part of the array (in the same way as we did on slide 34), argue
whether this method is more or less (or equally) likely to pick a good pivot
compared to simply choosing the first element. Assume that all permutations are
equally likely, i.e. the input array is ordered randomly.

Your answer must derive probabilities for choosing a good pivot and
quantitatively reason with them.

Add your answer to this markdown file. [This
page](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/writing-mathematical-expressions)
might help with the notation for mathematical expressions.


## Answer

Looking at slides 34, we can see that we have quarters of a standard array that are bad for finding a good pivot, and one solid good set of numbers in the middle. That, with the right combinations, the median can be either good or bad. A pivot is bad if it gives us a number outside of the good values, it's closer to the worst case that way. I decided to label good and bad pivots like this. 

[ $Lo$ | $G$ | $Hi$ ] 

It's important to make a distinction between wether a bad pivot is from the high or low part of the list as in some combinations can make good median values ($Lo$ $G$ $Hi$ for example). Based on these we can find all the combinations of values that will produce a bad pivot, which is when more than one bad pivot from the same side of the list occur. And find how many times they can occur.

$Lo$ $Lo$ $Lo$ | $Hi$ $Hi$ $Hi$ (each only 1 permutation exists)

Because G represents half of the data, it makes it hard to compare with the other two pivots because they represent only a quarter of the data. If we split G into two sides, Low good pivots and High good pivots, it is easier to compute probablity because every choice has the same size (4 * 4 * 4) and we won't have to find weighted probabilities. 

$Lo$ $Lo$ $G$ | $Hi$ $Hi$ $G$ (each 6 permutations because of low and high good pivots)

$Hi$ $Hi$ $Lo$ | $Lo$ $Lo$ $Hi$ (each 3 permutations)

This adds up to 20 bad cases. With 64 possible combinations We have a $31.25\% $ Chance of getting a bad median and slowing down our algorithm, and therfore a $68.75\% $ Chance of getting a good median and having a faster case. This is a little worse than twice as fast as a default pivot picking process (at random) so finding a Median of three values is actually faster. 
