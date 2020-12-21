

## 首先

根据Gu Working Paper (2019) 做好章节5.3中的Dynamic Effect Estimation，根据章节5.1中提及到的Rice and Strahan, 2010中的美国银行关于在其他州开立分支机构的解禁的政策：

因为Main Regression中是Firm Year，所以，在拿到Rice and Strahan的数据后，需要将公司数据和各州数据进行合并，最终结果将是每一个公司的每一年观察值都会有一个特定的值。

> Deregulation Details: 
>
> 1970年，只有12个州无限制地允许银行开设州际分支机构，另外有16个州禁止银行开立分支机构；20实际70年代以来，不允许银行开立分支机构的政策已经逐步开始在转变，1978年，Maine开始通过一项法律准许银行控股公司进入其他州，随后，其他州也逐步通过了类似的法律。但是这些法律并没有命令允许银行开立州际分支机构。1994年，IBBEA法案终于打通了这种限制，并且显著增加了银行间的竞争，拓展了信贷供给规模，降低了资金成本并且减少了金融市场中的费用成本。
>
> 美国各州允许银行开立分支机构需要根据金融机构的**四个**条件来判断：
>
> 1. the minimum age of the target institution
>
> 2. de novo interstate branching
>
> 3. the acquisition of individual branches
>
> 4. a statewide deposit cap
>
> Rice and Strahan 2010年推行了一个时间序列指数，涵盖1994至2005期间的数据。指数数值从0到4，数值越高代表越少的解除监管(deregulation)。
>
> Gu 2019 WP中援引了D'Acunto, Liu, Pflueger, and Weber 2018中的观点，一个周如果是一个解除监管的州，则它至少移除了四种限制中的一种，这个州的指数数值则会小于4。

然后Gu的文章用了一个交互项`Deregulation*Inflexibility`，也可以算做一个`Dummy variable`，如果公司`i`的总部此个州内某一年的`deregulation`的政策是低于4，也就是说对银行业设置州际分支机构是有松动可能的，那么此公司此年份的观察值则为记录的值，否则为`0` 。在做这一步的时候没有必要完全引用Gu文章中的Control Variables，使用之前讨论过的Controls。

###存在的问题

* Rice and Strahan的数据来源，Google 吗？

* 交互项interaction item真的是dummy吗？处理方式如何.

  * 设置`Deregulation`，如果一个公司的总部所在的州在当年或者当年之前实施了Deregulation，那么这个公司的`Deregulation`的值则赋予1，否之为0，Gu的文章中是这么定义的。

  

## 第二

在做好Bank Regulation之后，参考Gu 2019 Table 6. 

> 预期的结果会是，将credit supply做为一个shock，inflexible的公司在这个credit shock之后的tax avoidance会降低，公司逐步从inflexible到flexible，财政状况会逐渐变好。

## 第三

考虑分组的问题，分组问题主要是去衡量financial constraints，分组具体可以通过mean, median或者按照top 30 以及bottom 30进行比较，中间的40可以忽略等等，分组方式可以通过如下几种分组方式尝试：

​	1 通过Gu et al. 文章中的contraction和expansion的分组进行分组比较

​	2 通过cash holdings的值进行分组比较

​	3 ...K-Z index, Denis and Sibilkov 2009 measure,operating leverage等等
