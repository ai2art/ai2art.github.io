---
title:  Stable Diffusion 入门教程
---

## 快速上手

如果你有Nvidia显卡（显存不小于4G左右），可以下载<a href="http://www.stablediffusion.cc/#tools" target="_blank">免费AI创作软件（自带简单使用教程）</a>


(待完成……)

## 文本工程(Prompt Engineering)

Stable Diffusion可以根据文本提示生成一幅画， 但并不是所有文本提示都能生成**优质的**的画面，而只有在画面优质的基础上，才谈得上生成的图片是否满足需求。

怎样找到一个提示语，它既能生成优质的画面，同时又满足需求——这是一个有技巧的过程，国外的玩家称这个过程为“文本工程(Prompt Engineering) ”。 文本工程是AI作画过程中最重要的环节。 虽然名称里有Engineering，但这个过程并不像算法调参那样严格，并且你不需要对AI的底层算法有多少了解，这更多的是一种经验积累。 

下面我们就来首先讨论一下我们在进行文本工程时的一些最佳实践。（由于目前开源的stable diffusion [^1] 模型是由英文语料训练而成的，因此我们这里要讨论的怎样找好的英文提示语。）

[^1]: <a href="https://stability.ai/blog/stable-diffusion-announcement" target="_blank">stable diffusion 官网</a>


 > **最佳实践一：保持其他默认参数不变，先通过调整提示语，让生成图像“看得过去”。**

由于提示语是影响图片生成最重要的因素，因此在没有得到好的提示语之前，精调其他参数(如CFG，sampling_steps等参数) 一般来说得不到优质的图片。 其他参数的精调，只是锦上添花，无法让乌鸡变凤凰。 

“他山之石，可以攻玉”。 找到好的提示语的一个基本方法是去一些 <a href="/projects/stable-diffusion-cn/#prompt" target="_blank">gallery网站</a>，看看别人是怎么写提示语的。 当然如果你有明确想画的元素，你也可以通过这些网站的搜索功能，根据英文关键词过滤出更匹配的内容。

我打包了一个<a href="/projects/stable-diffusion-cn/#tools" target="_blank">stable diffusion工具</a>，甚至集成了提示语的中英文翻译功能，给各位爱好者提供保姆级服务 ：）


你可以从这些网站上找到你感兴趣的画风或者主题，看看这些图片的提示词是怎样写的。从这些好的例子中吸收灵感，把这些提示语作为出发点，然后做一些局部修改，放到<a href="/projects/stable-diffusion-cn/#tools" target="_blank">生成工具</a> 中来，看看能生成怎样的图片。

> **最佳实践二： 借鉴、参考、修改、混合……这是基本的方法，简单，粗暴，有效。**

提示语中单词的增增减减、反复试验生成效果是找到好的提示语的基本途径。 

某种意义上，寻找好的提示语是一门“玄学”。 它在试图通过某种直观的方式来理解怎样让AI生成更好的图片，而这和AI模型的底层算法是没有直接关联的。因此你也没有必要严格遵守科研工程上由简到繁的原则， 大胆去试，不行重来。

> **最佳实践三： 提示语尽量描述具体一点，不要吝惜夸奖。** 

事实上，根据大多数经验，提示语长一点往往能生成更好的图片。 不要怀疑AI是否能理解太长的描述, 长短对它来说差别不大。 例如

> <cite>white futuristic mage house covered in plants, hanging vines, floating inside an enormous spherical chamber, cinematic, epic, dramatic lighting, cinematic view, epic sky, detailed, concept art, low angle, high detail, warm lighting, volumetric, godrays, vivid, beautiful, trending on artstation, by jordan grimmer, huge scene, grass, art greg rutkowski</cite> 

这是我从网上摘抄的一段效果不错的典型提示词，你会发现这段话还是比较长的，你可以拿来验证一下生成图片的效果。 注意你可以随手加一些 beautiful, elegant, masterpiece，trending on art station之类空泛的夸奖词语。 如果你愿意，你可以把AI想象成一个会迷失在表扬里的小盆友，你夸得越狠，它就表现得越好。 当然从机器学习的角度来说，这是由于训练数据中优质的图片往往和正面的评价相关联，因此提示语中出现正面的评价，也让模型在生成过程中给优质的图片以更大的参考权重。

当然提示词过长也有点浪费，比如说不要超过大约80个单词，多出来词语会被计算机截断舍弃。

到目前为止，我们重点关注的应该是生成图片的画风怎样，色调怎样，图像中是否有我们期待的关键人物、物品、环境等等元素。 至于这些元素在画面中，是否符合我们期待的逻辑关系是相对次要的，因为我们往往可以通过暴力枚举的方式，在生成图片中找到符合我们想要的逻辑关系的那张。

> **最佳实践四： 提示语中添加艺术家的名字，这对生成图片的画质、风格影响很大。**

例如： by DaVinci, in the style of Van Gogh, by Greg Rutkowski and Tyler Edlin 等都是在gallery网站上经常能看到的提示语。 



我一般常按照如下方式来组织提示语，仅供参考：



| 画面内容描述       | 艺术家描述         | 其他补充修饰        |
|-------------------|-------------------|--------------------|
| a painting of a cute black cat  walk on a cyberpunk street | by Greg Rutkowski and Tyler Edlin | ultra detailed, digital art,  octane render, 4k, micro details... |

<br/>
这里还有一个艺术家风格的表格，你可以拿去参考，你可以有选择的根据画面内容和期待的风格选择艺术家。
<br/>

<table>
  <thead>
    <th>风景地貌</th>
    <th>插画人物</th>
    <th>经典名家</th>
    <th>科幻未来</th>
  </thead>
  <tbody>
    <td>Tyler Edlin,Mark Simonetti</td>
    <td>Justin Gerard, Wayne Barlowe, Victor Adame Minguez, Jesper Ejsing, Gerald Brom, Greg Rutkowski</td>
    <td>DaVinci, Pablo Picasso, Van Gogh, Winslow Homer, M.C. Escher</td>
    <td>Jim Burns, John Harris, Dean Ellis, H.R. Giger</td>
  </tbody> 
</table>

<br/>
这个表格远没有涵盖所有艺术家(已收录的艺术家完整列表 和 补充修饰词，详见<a href="/projects/stable-diffusion-cn/#tools" target="_blank">qq群</a>的群文件)。 

当然“萝卜青菜，各有所爱”，你需要通过自己不断的摸索试验，才能真正找到适合自己的艺术家提示词，毕竟这是一门“玄学”！

> **补充知识点一： 提示语可以“分词”化，不需要像人说话一样是完整的句子。**

对于模型而言，提示语中词语本身的重要性，一般来说远大于这些词语间的语法逻辑关系，或者说模型无法精确理解一句话的含义，因此精确的语法逻辑顺序意义不大，因此你可以用逗号的形式，把重要的描述性词语分割、罗列出来即可。 例如：

> <cite>a portrait of wizard, yellow hat, crystal ball, by artgerm and greg rutkowski and alphonse mucha, anthropomorphic, deep focus, fantasy, intricate, elegant, highly detailed, digital painting, artstation, concept art, matte, sharp, illustration, hearthstone</cite>

这种分词描述的一个好处是你可以在词的粒度上描述图画，或者调整前后顺序，而不必拘泥于一定要是完整的句子。 当然，如果你用 <cite>a portrait of wizard wearing a yellow hat and holding a crystal ball</cite> 这样完整的表述方式也不会有人拦着，对计算机来说可能二者差别不大。


> **补充知识点二： 提示语中词语的顺序对出图效果有影响，最重要的概念放在前面。**

一般来说越靠前的词语在生成图片时，权重越高，例如你想强调这幅画符合那种画风，你可以把艺术家之类的描述尽量放前面，例如：

> <cite>masterpiece of artgerm and greg rutkowski, hearthstone, fantasy, intricate, elegant, a portrait of wizard, yellow hat, crystal ball, anthropomorphic, deep focus, highly detailed, digital painting, artstation, concept art, matte, sharp, illustration</cite>

而如果你想强调画中“帽子”的元素，你可以这样写：

> <cite> a yellow wizard hat, crystal ball, by greg rutkowski, terrifying, horror, poorly lit，anthropomorphic, deep focus, fantasy, intricate, elegant, highly detailed, digital painting, artstation, concept art, matte, sharp, illustration, hearthstone</cite>

再比如说这样描述后，你发现画出来画风太阴暗了，你可以把terrifying, horror, poorly lit这些词尽量放到后面一点，或者把直接去掉。 

AI也希望你讲话有重点，开门见山！ 或者你觉得一个概念至关重要，你甚至可以重复三遍，变着方儿让AI get到你想表达的意思。

## 参数理解

当你已经基本找到你想要的提示语之后，下面是时候关注其他几个主要参数的用法了。

这些参数直接和AI输出图像时的具体运算方式相关。 当然这里我们不会聊具体数学公式，而是来看这些参数的意义如何，调节时最佳实践如何。

### CFG （Classifier Free Guidance）

这是一个有点“科幻”的参数。 它决定了AI要严格遵守提示语的指令到什么程度。 一头是： 小子别顾虑太多，提示语你参考着来就行，我就随便说说，主要靠你自由发挥，我信你！ 另一头是：嗨AI，你要严格按照提示语来画画，不要调皮，我是你爹全听我的（不然，我就拔插头）！ 

根据CFG取值大小，我们大致上，可以这么分类：

- CFG < 6: AI, 去裸奔，去肆意驰骋你的“想象力”吧。
- 7< CFG < 11: AI，咱们精诚合作，不分彼此。 
- 12< CFG < 15: AI，你要认真对待我的指令，要听话哦
- CFG > 16: AI，我说你做，别废话……


究竟该把CFG的值选在哪个档位没有严格的标准，或者说这取决于你期望AI怎样看待你的提示语。 比如说：你没怎么用心筛选提示语，对它的出图效果没什么信心，你可能应该选择一个 CFG<6的值。 但如果你对自己提示语的效果信心爆棚，你完全可以先选一个CFG>12 的值先试试看。

一般来说，完全放任AI自由发挥和不给任何自由都不是好的选择（吃的米饭越多，你会越来越发现中庸之道确实有它的道理。）所以我们往往会选择 7< CFG < 11 这个档位作为CFG的默认值。 这个区间是AI和人类彼此合作的档位，一般来说是更好的选择。 在我看来，这个档位也恰好反映了目前AI技术的发展程度，我们正处于一个AI和人类各取所长，才能实现最佳表现的时代。

#### Sampling Steps

这个规定了AI生成图片时的时长（步数）。 AI出图的过程可以想象成一场考试，而sampling steps 规定了考试时间。 如果时间太长，AI已经完成试卷，并且还检查好几遍了，这么拖着大家都累（AI没法提前交卷）
如果时间太短，AI还没答题完成，就强迫AI交卷，得分肯定也高不到哪去。

作为一个默认值，sampling steps ~ 50 是一个不错的盲选。

在对画质基本没有影响的条件下，我们一般希望 sampling steps 越小越好，毕竟steps越少，出图的速度越快；当然如果你电脑的性能足够快，然后对画质的要求精益求精，你完全可以选择一个大一点的sampling steps，比如 > 100。

（在粗筛看提示词效果阶段，由于我的GPU性能一般，所以我一般选sampling steps 为20~30左右以提高输出效率；在精筛优化阶段，我一般会选择steps 在50~100左右，这样可以提高画质） 

#### Sampling Method

（待补充）

#### batch size 和 batch count

电脑出图时，同时并行输出图片的张数，比如 batch_size=5 意味着同时输出五张图。 主要在电脑容量和性能允许的前提下，我们当然希望同时出图的数目越多越好。 但batch_size
越大，对GPU显存 和 CPU内存的消耗越多，因此batch_size 设置太大，可能会因显存不够而
报错，那比如说我的显存没法同时输出5张图（只能出一张图），而我就是要5张图怎么办呢？

很简单，让程序跑5次不就可以了，这对应了batch count这个参数。 你期望程序跑几次就把batch count设成几。 比如我的电脑只能一次出1张图，而我想要5张图，那么我就可以把batch count 设为5，让电脑跑5次。 用时间换空间，非常公平！ 谁让我的显存只有区区 6G 呢

#### eta

（待补充）

## 技术架构

如需转载，请联系作者本人，并注明出处。

## 参考资料 