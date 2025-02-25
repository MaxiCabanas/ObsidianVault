Dot product is an operation that can help us to know how similar the direction of two vectors are. 

# Input and result
Taking two vectors as input, the operation returns a number with value in the range [1, -1]

```
1 = both vectors directions are equal
0 = both directions are perpendicular
-1 = both directions are opposite
```
# How it works
An easy way to think about this operation is to think that we have a light source exactly perpendicular to our second vector, we cast the shadow of the first vector onto the second vector, and then we take the length of this shadow as a result of the operation.

Although normalized vectors are not actually required for the operation, for this explanation let's say we have two normalized vectors $\vec{x}$ and $\vec{y}$, the dot product will looks like:

![](Media/Pasted%20image%2020250223163439.png)

This is a very intuitive way of thinking about dot product in a functional way, its easy to see that if $\vec{y}$ is perpendicular to $\vec{x}$ there will be no shadow, or a shadow of length 0. If both vectors have equal directions the shadow will have the same direction of $\vec{x}$ (1) and if they are opposite will have the length of $\vec{x}$ multiplied -1 (-1 in this case).

To know how this is actually calculated mathematically see the sources.

sources:
https://mathinsight.org/dot_product