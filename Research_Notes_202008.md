#### Research notes

##### 20200803

小虎帮忙修改了code，润色了一下放在了`code`文件夹，`20200727xd.sas`

> 小虎加上了某一个州是否通过了good faith

 * 加上了dynamic tests所需要的变量

 * tasks:
    * 合并BRI dataset...`done`
    * 加入`stata` 是否还是会出现 `observations` 和 `20200530.dta` 不一致的情况...`done`
    * 查看 **mean** 等等变量...`done`
    * 结果和我的code结果一致
    * 现在需要通过怎么调整让结果显著
      * 首先查看一下最晚通过good faith law的州
      * 查看一下有些州是不是又取消了good faith law，还是需要回到 *firing* 这个文章的阅读上来。
      * 同时可以查看ssrn上关于WDL/Good faith相关的文章看看
      * 在ssrn上找了一篇"the cost of WDL"，这篇文章中通过good faith exception的一共有12个州，有数据的是13个州，跟 `firing` 文章相比少了Utah，并且Oklahoma在1985年5月通过 good faith 但是在1989年的法庭宣判中又拒绝了 good faith，因此，相比 firing 文章的14个少了2个
      * 重新整理sas code并且将这个结果告诉小虎
      * 结果和之前的 `firing` 文章并没有太大的区别

20200805

小虎重新分享了一篇文章：Fairhurst, Liu & Ni 2020, Employment protection and tax aggressiveness: Evidence from wrongful discharge laws，按照这篇文章来重新核实 

* sample period from 1970 to 2000
* two years following the final adoption of the Good Faith Exception
* Good Faith is an indicator variable that takes the value of 1 if a firm headquartered in state has adopted the Good Faith Exception as of year *t* 
* 基本上还是要回到`firing costs and capital structure`这篇文章
* 会不会跟sample period有关系？Fairhurst, Liu & Ni 2020是1970 to 2000，Serfling 2016是1967 to 1995
* 小虎可能要重新跟co-author沟通一下重新计算1967年到2018年的数据，包括cash ETRs



20200814

小虎更新了data，`measures>compustat_taxavoid_64_19`，需要做的事情是：

* 重新算inflexibilities
  * **inflexibility的计算需要compustat_1964_2019的数据**
* 重新计算bri
* 重新计算good faith exception
  * 首先WDL的数据都是需要包含的，在Xiaoran Ni的文章中，implied contract exception and public policy exception都包含在control当中
  * 所有的WDL的数据都根据最`先`通过年份来录入，之后再通过SAS进行个别的修改，根据Serfling的文章，revisions of good faith counts 2, revisions of implied contract counts 2，所以大概只需要再额外添加四行命令来更改revision
  * 所有的WDL的数据重新整理，只保留年份
  * 保存数据至excel>state_level WDL>tab wdl 20200816
  * 数据结果不理想，小虎需要确定好86年到2000年/95年的数据，但是以前通过的公司进行删除
    * 首先处理wdl源数据，将1986年之前通过的州删除，仅仅只保留1986年之后通过good faith exception的州
    * 重新计算good faith dummy
    * 重新run regressions
* 合并整个datasets
* 重新run regressions
* 对比summary，找出问题



20200820

* 现在不需要使用格式齐备的表格模式，可以直接在STATA中查看回归结果，copy到Excel中，在copy之前，需要在excel中将格式调整为文本`text`；
* 因此可以删除esttab命令之后的一些变量，方便查看，也加快运行速度；
* summary
* with control
* without control
* dfbeta，在处理dfbeta的时候，需要严谨，如果删除bottom 1%，则对应需要删除top 1%
  * 处理dfbeta时，发现dfbeta_2每次的值都不一致？

20200821

* Xiaoran Ni sample period 1970 to 2000
* Serfling sample period 1967 to 1999
* 暂时选定的sample period 1967 to 2000
* dfbeta最好只用一个，选定cash_etr1使用dfbeta，可以选择删除bottom/top或者only top
* 发现1964年到1986年之间，cash_etr1 and cash_etr2没有值
* 现在从1987年至2000年之间，来测试dfbeta以及cash_etr1 cash_etr2的结果，同时dfbeta不满足于1%， 5%，可以稍微少删一点，截至时间2000年也需要重新来衡量。
* gaap_etr需要满足大概10%显著，同时保持cash_etr大概5%显著
* control可以选择性删除类似DA, cash, cashflow or working capital

