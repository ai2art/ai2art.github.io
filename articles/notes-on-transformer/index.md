---
title:  Notes on Transformer
---

# {{ page.title }}


## Transformers


### 1.1 什么是 attention？

give a set of elments $\{e_i\}$, which described by a **value vector** $\{v_i\}$, the output without "attention" might be defined as a average:

$$ {\rm out} = {1\over N}\sum_i v_i $$

To work better, we introduce "attention" for every $x_i$ relative to a query, described by a **query vector** $q$, 

$$ {\rm out} = \sum_i f_{\rm attn}(q, k_i) v_i $$

here $k_i$ is called the **"key vector"** of $x_i$


### 1.2 什么是 self attention?

1) To be specific, we regard $e_i$ as "words" from a sentence. Every word is related to a "feature vector" $x_i$, which is taken from a "vocabulary embedding matrix", or calculated from some previous functions.

2) 我们引入三个操作 $Q$、 $K$ 和 $V$, 他们作用在 $x_i$ 上分别得到 $e_i$ 的query vector，key vector and value vector:

$$ q_i = Q(x_i), k_i=K(x_i), v_i = V(x_i) \label{eq1}\$$, 具体实现中 通常选择 Q，K，V 是用矩阵表示的三个线性操作， $f_{\rm attn}(\cdot)$ 通常选为

$$f_{\rm attn}(q_i, k_j) = {\rm softmax}\left(q_i\cdot k_j\over \sqrt{d_k}\right)$$, 其中$q$ 和 $k$ 的维数相同都是$d_k$. 因此对于一个句子中的 $e_i$ 对应的output是：

$$ {\rm out}_i = \sum_j {\rm softmax}\left(q_i\cdot k_j\over \sqrt{d_k}\right) v_j$$

由于一个句子有$M$个词，因此 ${\rm out}_i$ 可以看作一个 $M\times d_v$ 的矩阵

3) 补充1：future mask 

对于causal model，（$i$ 标记词在句子中出现的位置）

$$ {\rm out}_i = \sum_j {\rm softmax}\left(a_{ij}\right) v_j$$

其中  $$a_{ij}=\left\{\begin{array} ({q_i\cdot k_j\over\sqrt{d_k}}~~\text{j<=i}\\{\rm -Infy}~~\text{j>i}\end{array}\right.$$


4) 补充2： positional Embedding

不妨将 $i$ 看作词的位置序号。对于初始层，一般选 $x_i = \tilde{x}_i + p_i$，其中$\tilde{x}_i$是 textual embedding, $p_i$是positional Embbeding （对于Image 或 Graph 需要有其他feature 来取代这里的 positional embedding）

（对于中间层，$x_i$ 是上一层的输出） 


5) 补充3：MultiHead

一般选择多个feature map 即 $（Q, K, V）$, 即 $(Q, K, V)\rightarrow (Q^{(\alpha)}, K^{(\alpha)}, V^{(\alpha)})$, 

$$ {\rm out}_i^{(\alpha)} = \sum_j {\rm softmax}\left(a_{ij}^{(\alpha)}\right) v_j^{(\alpha)}$$

最终的输出，我们也许可以选择average，但过于粗糙，因此我们引入如下操作：

$${\rm out}_i= W [{\rm out}_i^{(0)}, {\rm out}_i^{(1)},\cdots]$$

即concat 再加一个线性变换作为最终输出

6) 补充4: Residual

当输入 $x_i$ 和 输出${\rm out}_i$ 维度相同时，我们可以引入残差结构，另外会进一步引入Norm结构，即


$${\rm out}_i= {\rm Norm}(x_i + W [{\rm out}_i^{(0)}, {\rm out}_i^{(1)},\cdots])$$

7) 补充5： 对于encoder-decoder structure，encoder结构如前文所述，一般decoder的Value vector 和 Key Vector 由encoder的输出来定义，

对于类似gpt的decode only的结构，Value vector 和 Key Vector 还是由前面引入的K，V 矩阵来实现，和encoder的唯一不同之处只是最后的输出层，接了一个全连通的 softmax 输出下一个词在vocabulary中的分布概率。

8) gpt 的整个流程可以这么简单理解：

(1) 给定一个包含M个词的句子 $(e_0,e_1,e_2,\cdots e_{M-1})$， 

(2) 初始先通过embedding映射为：$x_0, x_1,\cdots x_{M-1}$

(3) 每经过一层 transformer (记为 $t$)，这组矢量映射为：$\left(x_0^{(t-1)}, x_1^{(t-1)},\cdots x_{M-1}^{(t-1)}\right)\rightarrow \left(x_0^{(t)}, x_1^{(t)},\cdots x_{M-1}^{(t)}\right)$

(4) 最后一层$T$, 将$M$个词的输出concat 拉平作为输入（拉平后的向量维度是 $M*d_v$），然后接一个输出向量维数为 $\|V\|$ 的全连通层，再softmax，得到下一个词在vocabulary上的概率分布，这个概率分布可以通过交叉熵来训练