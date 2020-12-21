#### 2020年7月Research

##### 202007 communication with Xiaohu

1. balance sample: 所有regression都用一样的observations，N都调整成一致的数据，确保cash etr1, cash etr2等等都是同时有值的。if cash etr1 NE dot, and cash etr2 NE dot, 大概写上dependent variables以及size等大型变量不missing，就是一个balance sample。

   需要把baseline regression， 3/5/10 years with control都加上balance sample

2. etr measure rolling window, and be dependent variables then run regressions

3. Alternative shock (baseline DiD, Bertrand test, and IPW)

   “baseline DiD"

   另外一个regulation change，银行branch index，让inflexible公司变得flexible，现在是将flexible公司变得inflexible

   限制公司过分裁员的法律，good faith exception

   不需要使用interaction item

   直接使用dummy，通过了该法律的是1，没有通过该法律是0

   回归在2000年之后就不需要再run了

   有两种回归：一种是通过了法律的州直接进行回归

   另外一种回归是所有的州都进行回归

   "Bertrand test"

   firing cost, table vi

   将 good faith 拆分成-1， 0， 1， 2+或者-2， -1，0，1+ 

   dummy 只对应那一年

   "IPW"

   Inverse probabilities weighting

   默认所有的州都没有通过法律，设置参数预测这个州是不是可以通过相关的法律，高权重没有通过的州是control，结果是dependent variable: ETR, 小虎有code

4. cross-sectional tests

   to do list number 2

   Cash holdings; 

   k-z index; 

   Denis & Sibilkov (2009) measure; 
   
   EFN measure (Demirguc-Kunt and Maksimovic, 1998); 
   
   Operating leverage (higher or lower OL avoids more taxes, Gu et al. RFS (2018))
   
   measure 可以使用 good faith interaction
   
   

##### 20200722 start to update

* ETR Rolling Windows
  * ETR Rolling Windows已经包含在了原来计算inflexibility里面
  
  * 在20200530.dta这个STATA文件中
  
  * 需要选用什么区间的 winsorization 对 Rolling Windows of Tax Avoidance进行winsorization? 5/95 or 1/99?
  
  * 首先summarize rolling windows of GAAP ETR/Cash ETR1/Cash ETR2，然后对GAAP ETR/Cash ETR1/Cash ETR2进行5/95的winsorization.
  
    > **不对GAAP/Cash ETR1/Cash ETR2进行winsorization处理，需要做的是将小于0的值处理成空值。**
  
    > 根据20200615.do的处理：
    >
    > at_log, leverage1, control_cashflow, control_capx, control_wc是1/99 winsorization
    >
    > da, tobinq, leverage2, control_cash, inflex_3y, inflex_5y, inflex_10y是5/95 winsorization
  
  * 根据同小虎的沟通，**20年的Tax avoidance已经实用性不大**，所以在balance sample的过程中，并没有加入Rolling windows of GAAP/ETR1/ETR2 20 years，并且，在Summarize过程中也将20年上述变量也忽略了。其实在之前已经做过一部分的balance sample，问题是：balance sample是不是需要所有参与regression的观察值**一致**？
  
  * DFbeta命令的处理？
  
  * 加入了3/5/10年的rolling windows of tax avoidance作为dependent variables baseline regressions with controls
  
  * 20200724，根据coauthor的要求，先按照
  
    > drop if at ==. 
    >
    > drop if gaap_etr ==.
    >
    > drop if cash_etr1 ==.
  
    对sample进行balance，这样删除的观察值可能会比较多，也暂时不需要用dfbeta。分别对original ETRs和Rolling windows of ETRs进行balance sample. 

#### 20200724

* 已经将balance过的variables处理好了，并且也跑了回归，结果是20200724.rtf

#### 20200730

* 从excel导入数据到SAS，合并wrongful discharge laws到主表

* 经过和小虎讨论，每一个公司根据年份应该会有变化，而我在20200730的处理中，仅仅是合并了州的数据，并没有包含fyear这个变量，导致公司的dummy没有随着时间的变化而变化

* 小虎comments

  > 我们之所以用DiD或者那些regulation changes 是因为inflexbility的measures（就是3年 5年 10年那些）可能是有内生性问题的 或者说就是这些变量的大小 有可能是有其他因素影响的 导致不是完全单纯的measure了inflexibility 另外用inflexibility做x ETR做y 得出的系数 不管是正相关还是负相关 其实都有可能是假相关 假设两个毫不相关的变量 正好运转方向相反 那你就可以得到一个完美的显著的负系数 为了阻止这种情况的发生 我们就需要找到一个event或者regulation change来衡量inflexibility的变化（而且这种变化是公司自身不能影响的）这时候再比较这种event之前之后ETR的变化 就能够大概告诉我们inflexibility对ETR的真实影响了 这就像做实验一样

  > 假设你想看肥胖对癌症的影响 最简单的OLS 就是用癌症的概率做y 体重做x 这种回归出来的结果 有可能就是不可信的 因为这种回归没办法得出因果关系 
  > 为了得到因果关系 我们可以随机找100个人 50个人吃有效减肥药 50个人不吃 然后这个时候我们再跑回归 这个回归就不再需要体重这个变量了 而直接是P（cancer）=减肥药小组dummy（1=吃了药 0=没吃药）+controls 
  > 这个应用到我们的文章 就是
  > ETR=exception dummy（1=通过了 0=没通过）+controls 我们这样设计是因为我们相信这个exception law的通过会导致公司变得不flexible

* 重新更改excel表格，加入1990至2018年的fyear数据

