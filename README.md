# Puzzle 1

*Given an undirected graph containing $n$ $(n > 2)$ nodes, the probability that arbitrary pair of nodes are connected by an edge is $p$. Given two nodes randomly, what is the probability that there exists a path between them?*



Lemma:

For any undirected graph which contains $m$ nodes and the probability that arbitrary pair of nodes are connected by an edge is $p$, the probability that the graph is connected is $f(m)$, where $f(m) = 1 - \sum_{i=1}^{m-1}C_{m-1}^{i-1}f(i)(1 - p) ^ {i(n-i)}$



Proof of lemma:

The graph may have many connected components. For arbitrary node $v$, the probability that the size of components that $v$ belongs to is $i$ is equal to $g(i)$, where $g(i) = C_{n-1}^{i-1}f(i)(1 - p)^{i(n-i)}$. We can get the proof based on $\sum_{i=1}^{n}g(i) = 1$.



Solution:

There exists $C_{i}^2$ paths in a connected components, so the answer is $\frac{1}{C_{n}^{2}}\sum_{i=1}^{n}C_{i}^{2}f(i)$