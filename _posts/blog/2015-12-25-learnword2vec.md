---
layout:     post
title:      How to learn word2vec 
category: blog
description: word2vec的小白起步之路。
---


标签（空格分隔）： word2vec
---
## 插播一则消息：MathJax
[LaTeX完整教程][1]
[介绍MathJax的中文博客文章][2]
word2vec涉及的公式推导太多，所以借助MathJax在html中显示LaTeX数学公式，效果赞赞的。在页面中嵌入MathJax :
```javascript
    <script type="text/javascript"
      src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
    </script>
```
在head里加上两句话,开启美元符$的inline模式：
```javascript
    <script type="text/x-mathjax-config">
      MathJax.Hub.Config({tex2jax: {inlineMath: [['$','$'], ['\\(','\\)']]}});
    </script>
```
但是还有一个问题，就是markdown和MathJax的冲突：
> Keep in mind that the browser interprets your text before MathJax does.

对于"\_"和"{}"，markdown会按自己的方式“理解”，于是MathJax就不懂了。好在有[解决方案][3]。
When $a \ne 0$, there are two solutions to \(ax^2 + bx + c = 0\) and they are
$$x = {-b \pm \sqrt{b^2-4ac} \over 2a}.$$
\subsection{Multi-Layer Neural Network}
A.3-layer network: Input Layer,Hidden Lyer,Output layer\\
Except input units,each unit has a bias.
\subsubsection{preassumption calculation}
\\begin{equation}
net_{j} = \sum_{i=1}^{d}x_{i}w_{ji}+w_{j0}=\sum_{i=0}^{d}x_{i}w_{ji}=w_{j}^{t}x
\\end{equation}
Specifically, a signal $x_{i}$ at the input of synapse $i$ connected to nueron $j$ us multiplied by the synaptic weight $w_{ji}$\\
$i$ refers input layer,$j$ refers hidden layer.$w_{j0}$ is the bias.$x_{0}=+1$\\

- Each neuron is represented by a set of linear synaptic links, an externally applied bias,
and a possibly nonlinear activation link.The bias is represented by a synaptic link connected to an input fixed at $+1$.
- The synaptic links of a neuron weight their respective input signals.
- The weighted sum of the input signals defines the induced local field of the neuron in
question.
- The activation link squashes the induced local field of the neuron to produce an output.


  [1]: http://www.forkosh.com/mathtextutorial.html
  [2]: http://mlworks.cn/posts/introduction-to-mathjax-and-latex-expression/
  [3]: http://weiyangthecatalyst.name/2013/11/24/solve-markdown-mathjax.html
