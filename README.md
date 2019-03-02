# Puzzle 1

*Given an undirected graph containing $n$ $(n > 2)$ nodes, the probability that arbitrary pairs of nodes are connected by an edge is $p$. Given two nodes randomly, what is the probability that there exists a path between them?*

## Lemma:

For any undirected graph which contains $m$ nodes and the probability that arbitrary pair of nodes are connected by an edge is $p$, the probability that the graph is connected is $f(m)$, where $f(m) = 1 - \sum_{i=1}^{m-1}C_{m-1}^{i-1}f(i)(1 - p) ^ {i(n-i)}$

### Proof of lemma:

The graph may have many connected components. For arbitrary node $v$, the probability that the size of components that $v$ belongs to is $i$ is equal to $g(i)$, where $g(i) = C_{n-1}^{i-1}f(i)(1 - p)^{i(n-i)}$. We can get the proof based on $\sum_{i=1}^{n}g(i) = 1$.

## Solution:

There exists $C_{i}^2$ paths in a connected components, so the answer is $\frac{1}{C_{n}^{2}}\sum_{i=1}^{n}C_{i}^{2}f(i)$


# Puzzle 2

*Consider a particle that moves along a set of m + 1 nodes, labeled 0, 1, . . . , m, that are arranged around a circle. At each step the particle is equally likely to move one position in either the clockwise or counterclockwise direction. Suppose now that the particle starts at 0 and continues to move around according to the preceding rules until all the nodes 1, 2, . . . , m have been visited. What is the probability that node i, i = 1, . . . , m, is the last one visited?*

## Solution:

Define event $A_i$ as node i is the last one visted and event $A_{i-1,i+1}$ as node $i-1$ is visited before node $i+1$. We can simply get $P(A_{i-1,i+1}) + P(A_{i+1,i-1}) = 1$ (complementary events), $P(A_i|A_{i-1,i+1}) = P(A_i|A_{i+1,i-1}) = c$ (symmetry) and $P(A_i) = P(A_{i-1,i+1}) * P(A_i|A_{i-1,i+1}) + P(A_{i+1,i-1}) * P(A_i|A_{i+1,i-1})$ (Bayes' formula) . So $P(A_i) = c$ is correct for any $i = 1, . . . , m$ or $P(A_i) = \frac{1}{m}$.


# Puzzle 3

*Let $\textbf{X} = (X_1, X_2, ..)$ be a sequence of iid. discrete random variables such that $p_i = P(X_j = i)$. For a given pattern $i_1, ..., i_n$ let $T = T(i_1, ..., i_n)$ denote the number of random variables that we need to observe until the pattern appears. How to calculate $E[T]$?*

## Solution:

Let's first consider whether the pattern has an overlap which means that for some $1 \le k \le n$ and any $j = 1, 2, ..., k$ we have $i_j = i_{n-k+j}$.

### Case 1: No overlaps

First of all, we can simply get $T = j + n$ iif. the pattern does not occur within the first $j$ values and $(X_{j+1}, ..., X_{j+n}) = (i_1, ..., i_n)$. In other words, $P(T = j + n) = P(T > j, X_{j+1:j+n+1}=i_{1:n+1})$. However, whether $T > j$ is only determined by the first $j$ values. Consequently, $P(T = j + n) = pP(T > j)$ where $p = \prod_{j=1}^np_{i_j}$. Summing both sides over all $j$ yields, $1 = \sum_{j=0}^{\infty}{P(T = j + n)} = p\sum_{j=0}^{\infty}P(T > j)$. Combining with $P(T > j) = \sum_{k=1}^{\infty}P(T = j + k)$ we can get $E[T] = 1 / p$.

### Case 2: Has Overlaps
We can add an element at the tail to get a new pattern without overlap. Then we can get the solution by reusing the discussions in case 1.


# Puzzle 4

*Consider a Markov chain with $T$ states transition matrix $P$ where some of row sums are less than 1 (to ensure that it is not a closed Markov chain). How to calculate the mean spent time of transient states?*

## Solution:

Define $s_{ij}$ as the expected number of time period that the Markov chain is in state $j$ given initial state $i$ and $\theta_{ij} = 1 if i == j else 0$. Then we can get $s_{ij} = \theta_{ij} + \sum_{k=1}^{T}{p_{ij} * s_{kj}}$ where $p_{ij} = P(s_{t+1}=j|s_{t}=i)$. Convert it to matrix form so $S = I + PS$ or $S = (I - P)^{-1}$.


# Puzzle 5

*2-dimensional random walk problem with given two stop time like -2 and 3. How to calculate the expected stop time?*

## Wald's first identity:

Suppose $X_i$ is idd random variables and $S_T = \sum_{i=1}^{T}{X_i}$. Given stop time $T$ satisfing $E[T] < \inf$, then $E[S_T] = E[X_1] * E[T]$.

## Wald's second identity:

Suppose $X_i$ is idd random variables satisfing $E[X_i] = 0$ and $E[X_i^2] < \inf$. If $E[T] < \inf$, then $E[S_T^2] = E[T] * E[X_i^2]$.

## Wald's third identity:

Suppose $X_i$ is idd random variables satisfing $X_i >= 0$ and $E[X_i] = 1$. Given stop time $T$ satisfing $E[T] < \inf$, then $E[\prod_{i=1}^{T}{X_i}] = 1$.

## Solution:

Based on Wald's first identity, we get the expected state is zero for any time. So in the stop time, $E[S_T] = P(s_T = 3) * 3 + P(s_T = -2) * 2 = 0$.
Based on Wald's second identity, $E[T] = E[S_T^2] / E[X_i^2] = (4 * 3 / 5 + 9 * 2 / 5) / (0.5 * 1 ^ 2 + 0.5 * (-1) ^ 2) = 6$.