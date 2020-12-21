### Conversation with Xiaohu

#### 20200423

##### BRI

首先谈一谈BRI: Branching Restrictiveness Index的生成，在Rice and Strahan的文章里有一个表格，统计了1994年到2005年的每一个州的对银行控股公司开立分支机构的法律，具体统计了有：

* BRI, branching restrictiveness index
* 法律的生效时间，具体日期
* IBBEA对每个州的四个条件之一：机构年限 Minimum age of institution for acquisitions
* IBBEA对每个州的四个条件之一：是否允许新设全新机构, Allows de novo interstate branching
* IBBEA对每个州的四个条件之一：是否允许收购其他金融机构的分支机构, interstate branching by acquisition of single branch or portions of an institution
* IBBEA对每个州的四个条件之一：被收购机构的州存款上限，越高代表收购该州内机构越难, statewide deposit cap on branch acquisitions. 

我根据这张表格，将其1990年至2018年的数据进行了补全，补全的根据是：

* 1994年之前的数据，我设置为BRI = 4
* 2005年之后到2018年的数据，我设置了BRI = 2005年数据
* 重新根据Gu et al. 的文章设置了BRI Dummy，设置标准为：如果BRI指数等于4，则BRI Dummy等于0；如果BRI指数小于4，则认为该州对于他州银行控股公司进入该州设立分支机构有松动，因此BRI Dummy(在Gu的文章里面是Deregulation)等于1

已经在Dropbox > data > Measure 里面上传了这个SAS格式数据。

#### 沟通结果

1. 州匹配的时候是否选用正确的variable，小虎分享的一张图片中可能需要使用zipcode
2. 尝试调整一下sample period, 删除/不删除金融行业, winsor outlier/ no outlier winsorized.
3. 在Gu的文章中，dummy*inflex系数应该是正数
4. 回归中是否使用lag的问题
5. 使用dfbeta将最负1%系数删掉，让系数为正。

> 我在想，因为gu的文章是leverage，我们这个是tax avoidance，如果按照字面意思来讲的话，银行金融机构的放开，可能对于leverage来说是有正的增长的影响，但是tax avoidance可能就另说了吧。因为银行金融机构的增加，让企业会有更多的银行来进行审查，那么它对tax avoidance的作用有可能不是正的？



> Xiaohu's comment
>
> 银行貌似对公司的审查力度比较有限 tax avoidance并不是做假账 这个政策的松绑是被认为会减轻inflexibility带来的问题 因为inflexibility的负面影响降低 自然这部分企业就不需要再像过去一样avoid 那么多taxes了 不知道这样解释你是不是更清楚了 但是你说的那点也是有可能的 如果是这样 那应该会负显著 先看看结果 需要的时候我再和他们讨论下

