---
layout:     post
title:      How to learn word2vec 
category: blog
description: word2vec的小白起步之路。
---
标签： nlp

---


## Multi-Layer Neural Network
A.3-layer network: Input Layer,Hidden Lyer,Output layer
Except input units,each unit has a bias.

### preassumption calculation

$$
net_{j}=\sum_{i=1}^{d}x_{i}w_{ji}+w_{j0}=\sum_{i=0}^{d}x_{i}w_{ji}=w_{j}^{t}x
$$

Specifically, a signal $x_{i}$ at the input of synapse $i$ connected to nueron $j$ us multiplied by the synaptic weight $w_{ji}$\\
$i$ refers input layer,$j$ refers hidden layer.$w_{j0}$ is the bias.$x_{0}=+1$\\

- Each neuron is represented by a set of linear synaptic links, an externally applied bias,
and a possibly nonlinear activation link.The bias is represented by a synaptic link connected to an input fixed at $+1$.
- The synaptic links of a neuron weight their respective input signals.
- The weighted sum of the input signals defines the induced local field of the neuron in
question.
- The activation link squashes the induced local field of the neuron to produce an output.
