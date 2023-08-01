# 2-lift-neural-net

**Overview**
In this project, guided by recent-(ish) results in graph theory, I investigate the possibility of reducing the number of training parameters
in hidden neural network layers by a factor of 2 with little to no reduction in network performance, by constructing such layers from random 2-lifts 
of a layer with 1/2 the number of input and output vertices and 1/4 the number of training parameters.

In graph theory, a bipartite graph is a graph whose vertices can be separated into two distict sets,
such that all edges in the graph have exactly one endpoint in either set. Hence, we can consider a single layer of a neural network as a bipartite graph, 
where the input and output nodes are the two distinct sets of vertices. A bipartite graph where every vertex pair in the distinct sets is connected by an edge 
(like a dense neural network layer) is called a complete bipartite graph (1).

The spectral gap of a graph is defined as the difference between its two largest eigenvalues. Graphs with a larger spectral gap are better connected, 
and hence have better mixing properties. Ramanujan graphs are d-regular graphs with spectral gap at least 2√(d-1): This bound is determined as the
largest possible gap for a d-regular graph as the number of vertices goes to infinity. An alternative definition of this condition for (c,d)-regular 
bipartite graphs requires that the spectral gap must be at least √(c-1)+√(d-1). Marcus, Spielman, and Srivastava (2015) gave a probabilistic proof that 
infinite families of bipartite Ramanujan graphs can be constructed by taking repeated 2-lifts of one such graph. Because finite complete bipartite graphs 
are Ramanujan, any such graph can be the seed of an infininte family of Ramanujan graphs by appropriate choice of 2-lifts (2).

Intuitively, neural networks should perform better if each layer has good expansion properties (i.e. good mixing properties), because such structure 
corresponds to better distributed flow of information through the network structure. Additionally, there is evidence that the brain has good expansion 
properties when viewed as a graph. Due to (1) and (2), we can therefore hypothesize that it is possible to construct non-dense neural network layers with 
optimal mixing by performing optimal 2-lifts of a smaller dense neural network layer.

Here we run into a roadblock because the proof in Marcus-Spielman-Srivastava is not constructive. However, J. Friedman (2003) shows that random lifts are 
nearly Ramanujan with high probability. Hence in this project I construct a custom neural network layer in Tensorflow as a random 2-lift of a smaller dense layer, 
include it in a neural network for an image classification task, and keep track of how its spectral gap corresponds to the loss and accuracy of the resulting network.

**Sources**
Y. Bilu and N. Linial: Lifts, discrepancy and nearly optimal spectral gap. Combinatorica 26 (2006), 495-519. http://dx.doi.org/10.1007/s00493-006-0029-7.

J. Friedman: Relative expanders or weakly relatively Ramanujan graphs. Duke Math.J . 118(1) (2003), 19–35.

A. Marcus, D. Spielman, and N. Srivastava: Interlacing families I: Bipartite Ramanujan graphs of all degrees. Annals of Mathematics 182 (2015), 307-325.

**Acknowledgements**
I would like to thank Darren Upton (Jefferson Laboratories, Old Dominion University Physics) for helpful discussions & troubleshooting.
This project was motivated by texts I read under the guidance of my MS thesis advisor, Prof. Thomas Koberda (University of Virginia Mathematics).
