---
layout:     post
title:      How to learn word2vec 
category: blog
description: word2vec的小白起步之路。
---

标签： word2vec MathJax
---

## 插播一则消息：MathJax
word2vec涉及的公式推导太多，所以借助MathJax在html中显示LaTeX数学公式，效果赞赞的。
- [LaTeX完整教程][1]
- [介绍MathJax的中文博客文章][2]
- [在Jekyll中使用MathJax][3]
### 1. 关于博客环境：
- Github Pages
- Jekyll
- rdiscount
- MathJax
- Markdown
在post.html中嵌入MathJax :
```
    <script type="text/javascript"
      src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
    </script>
```
### 2. Problem
markdown和MathJax的冲突：
> Keep in mind that the browser interprets your text before MathJax does.

#### How to fix it?
在layout 文件里加上 :
```
    MathJax.Hub.Config({
      tex2jax: {
        skipTags: ['script', 'noscript', 'style', 'textarea', 'pre']
      }
    });
```
让MathJAx忽略非latex代码块或者一般的代码块：
```
    MathJax.Hub.Queue(function() {
            var all = MathJax.Hub.getAllJax(), i;
            for(i=0; i < all.length; i += 1) {
                all[i].SourceElement().parentNode.className += ' has-jax';
            }
        });
```


对于"\_"和"{}"，markdown会按自己的方式“理解”，于是MathJax就不懂了。好在有[解决方案][4]。
## Multi-Layer Neural Network
A.3-layer network: Input Layer,Hidden Lyer,Output layer.
Except input units,each unit has a bias.
### preassumption calculation
\\begin{equation}
net_{j} = \sum_{i=1}^{d}x_{i}w_{ji}+w_{j0}=\sum_{i=0}^{d}x_{i}w_{ji}=w_{j}^{t}x
\\end{equation}
Specifically, a signal $x_{i}$ at the input of synapse $i$ connected to nueron $j$ us multiplied by the synaptic weight $w_{ji}$.
$i$ refers input layer,$j$ refers hidden layer.$w_{j0}$ is the bias.$x_{0}=+1$.

- Each neuron is represented by a set of linear synaptic links, an externally applied bias,
and a possibly nonlinear activation link.The bias is represented by a synaptic link connected to an input fixed at $+1$.
- The synaptic links of a neuron weight their respective input signals.
- The weighted sum of the input signals defines the induced local field of the neuron in
question.
- The activation link squashes the induced local field of the neuron to produce an output.
Output layer:
\\begin{equation}
y_{j}=f(net_{j})
\\end{equation}
$f()$ is the \emph{activation function}.It defines the output of a neuron in terms of
the induced local field $net$ .\\

\xymatrix {
 x_{0}=+1 \ar[ddr]|(0.6){w_{j0}} &  &\\
 x_{1} \ar[r]|(0.6){w_{j1}} & B & C\\
 x_{2} \ar[r]^(0.6){w_{j2}} & net_{j} \ar[r]^(0.6){f()} & y_{j} \\
x
}


For example:
\\begin{equation}
net_{k}=\sum_{j=1}^{n_{H}}y_{i}w_{kj}+w_{k0}=\sum_{j=0}^{n_{H}}x_{i}w_{ji}=w_{k}^{t}y
\\end{equation}
$n_{H}$is the number of hidden layers.

So:
\\begin{equation}
g_{k}(x)=f(\sum_{j=1}^{n_{H}}w_{kj}+f(\sum_{i=0}^{d}x_{i}w_{ji}+w_{j0})+w_{k0})
\\end{equation}
The activate function of output layer can be different from hidden layer while each unit can have different activate function.

%%                  BP Algorithm                        %%
### BP Algorithm
The popularity of on-line learning for the supervised training of multilayer perceptrons
has been further enhanced by the development of the back-propagation algorithm. 
Backpropagation, an abbreviation for "backward propagation of errors",is the easiest way of supervised training.We need to generate output activations of each hidden layer.
The partial derivative $\partial J /\partial w_{ji}$ represents a sensitivity factor, determining the
direction of search in weight space for the synaptic weight $ w_{ji}$.
Learning:
\\begin{gather}
\mathcal T =\{ x(n),d(n)\}_{n=1}^{N}\\
e_{j}(n)=d_{j}(n)-y_{j}(n)
\\end{gather}
the instantaneous error energy of neuron $j$ is defined by

\\begin{gather}
J(w)=\frac 12 \sum_{k=1}^{c}(e_{k})^{2}=\frac 12||t-\delta||^{2} \\
\\end{gather}
In the batch method of supervised learning, adjustments to the synaptic weights of the
multilayer perceptron are performed \emph{after} the presentation of all the %N% examples in the
training sample $\mathcal T$ that constitute one \emph{epoch} of training.  In other words, the cost function
for batch learning is defined by the average error energy $J(w)$.
- firstly define the training bias of output layer:

\\begin{gather}
\Delta w=-\eta\frac {\partial J(w)}{\partial w} \\\\
w(m+1)=w(m)+\Delta w(m)
\\end{gather}

\\begin{gather}
\frac {\partial J}{\partial w_{kj}}=\frac {\partial J}{\partial net_{k}}\frac {\partial net_{k}}{\partial w_{kj}} \\
\frac {\partial J}{\partial net_{k}}= \frac {\partial J}{\partial \delta _{k}}\frac {\partial \delta _{k}}{\partial J}=-(t_{k}-\delta _{k})f'(net_{k}) \\
\Delta w_{kj}=\eta \frac {\partial J}{\partial net_{k}}=\eta (t_{k}-\delta _{k}))f'(net_{k})y_{j} 
\\end{gather}

- input->hidden


  [1]: http://www.forkosh.com/mathtextutorial.html
  [2]: http://mlworks.cn/posts/introduction-to-mathjax-and-latex-expression/
  [3]: http://cyukang.com/2013/03/03/try-mathjax.html
  [4]: http://weiyangthecatalyst.name/2013/11/24/solve-markdown-mathjax.html
