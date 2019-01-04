# Puzzle 1

*Given an undirected graph containing $n$ $(n > 2)$ nodes, the probability that arbitrary pair of nodes are connected by an edge is $p$. Given two nodes randomly, what is the probability that there exists a path between them?*



Lemma:

For any undirected graph which contains $m$ nodes and the probability that arbitrary pair of nodes are connected by an edge is $p$, the probability that the graph is connected is $f(m)$, where $f(m) = 1 - \sum_{i=1}^{m-1}C_{m-1}^{i-1}f(i)(1 - p) ^ {i(n-i)}$



Proof of lemma:

The graph may have many connected components. For arbitrary node $v$, the probability that the size of components that $v$ belongs to is $i$ is equal to $g(i)$, where $g(i) = C_{n-1}^{i-1}f(i)(1 - p)^{i(n-i)}$. We can get the proof based on $\sum_{i=1}^{n}g(i) = 1$.



Solution:

There exists $C_{i}^2$ paths in a connected components, so the answer is $\frac{1}{C_{n}^{2}}\sum_{i=1}^{n}C_{i}^{2}f(i)$


# Puzzle 2
*Consider a particle that moves along a set of m + 1 nodes, labeled 0, 1, . . . , m, that are arranged around a circle. At each step the particle is equally likely to move one position in either the clockwise or counterclockwise direction. Suppose now that the particle starts at 0 and continues to move around according to the preceding rules until all the nodes 1, 2, . . . , m have been visited. What is the probability that node i, i = 1, . . . , m, is the last one visited?*


Solution:
Define event $A_i$ as node i is the last one visted and event $A_{i-1,i+1}$ as node $i-1$ is visited before node $i+1$. We can simply get $P(A_{i-1,i+1}) + P(A_{i+1,i-1}) = 1$. Based on Bayes' formula, $P(A_i) = P(A_{i-1,i+1}) * P(A_i|A_{i-1,i+1}) + P(A_{i+1,i-1}) * P(A_i|A_{i+1,i-1})$. Another truth is that $P(A_i|A_{i-1,i+1}) = P(A_i|A_{i+1,i-1}) = constant$ because the clock and the flip horizontal one is the same when 12 align to the node $i$. So we can get for any $i$, $P(A_i) = constant = \frac{1}{m}$.
