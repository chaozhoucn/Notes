#### 20200903

* Bertrand test
* 同时也需要做implied contract, public policy
* following Serfling, -1/0/1/2



#### 20200912

for stata, data20200912 是 bertrand test -3 to 3

for stata, data20200911 是 bertrand test -2 to 2

在做Bertrand test的时候，需要做一些调整：

* 使用的sample是good faith dummy中通过处理dfbeta之后的sample

  > balance ETRs
  > replace gaap_etr = . if gaap_etr < 0
  > replace cash_etr1 = . if cash_etr1 < 0
  > replace cash_etr2 = . if cash_etr2 < 0
  >
  > dfbeta, cash_etr1, 2998 obs dropped
  > regress cash_etr1 gf_dummy
  > dfbeta gf_dummy
  > summarize _dfbeta_1, detail
  > drop if _dfbeta_1 > 0.005 & _dfbeta_1 !=.
  >
  > dfbeta, gaap_etr, 802 obs dropped
  > regress gaap_etr gf_dummy
  > dfbeta gf_dummy
  > summarize _dfbeta_2, detail
  > drop if _dfbeta_2 > 0.0095 & _dfbeta_2 !=.

* 需要加上control进行测试
* 需要对gf_n1/gf_n2/gf_0/gf_1/gf_2或者添加gf_n3/gf_3进行测试

大概结果是：

* 使用good_faith_dummy所使用的dfbeta

* 不加control，使用gf_n1/gf_n2/gf_0/gf_1/gf_2，cluster (gvkey):

  ![](C:\Users\chaoz\Pictures\Snipping Tools\Screenshot 2020-09-12 150004.png)

* 不加control, 使用gf_n1/gf_n2/gf_0/gf_1/gf_2，cluster (state)

  ![](C:\Users\chaoz\Pictures\Snipping Tools\Screenshot 2020-09-12 151112.png)

* 不加control，bertrand 为 -1 to 1，cluster (gvkey)

  ![](C:\Users\chaoz\Pictures\Snipping Tools\Screenshot 2020-09-12 153241.png)

* 不加control，bertrand 为 -1 to 1, cluster (state)

  ![](C:\Users\chaoz\Pictures\Snipping Tools\Screenshot 2020-09-12 153429.png)

* 不加control，bertrand为-1 to 2, cluster (gvkey)

  其中gf_2为>=2

  ![](C:\Users\chaoz\Pictures\Snipping Tools\Screenshot 2020-09-12 154529.png)

* 不加control, betrand 为 -1 to 3, cluster (gvkey)

  ![](C:\Users\chaoz\Pictures\Snipping Tools\Screenshot 2020-09-12 212211.png)

* 加上control, betrand -1 to 3, cluster gvkey

  ![](C:\Users\chaoz\Pictures\Snipping Tools\Screenshot 2020-09-12 212724.png)

* 不加control, bertrand -3 to 3, cluster gvkey

  ![](C:\Users\chaoz\Pictures\Snipping Tools\Screenshot 2020-09-12 213302.png)

* 不加control, bertrand -3, 0, 3, cluster gvkey

  ![](C:\Users\chaoz\Pictures\Snipping Tools\Screenshot 2020-09-12 213427.png)

* 加上control, bertrand -3, 0, 3, cluster gvkey

  ![](C:\Users\chaoz\Pictures\Snipping Tools\Screenshot 2020-09-12 220530.png)

* 加上control, n1/0/3

  ![](C:\Users\chaoz\Pictures\Snipping Tools\Screenshot 2020-09-14 184531.png)

* 加上control, n1/0/1/2/3

  ![](C:\Users\chaoz\Pictures\Snipping Tools\Screenshot 2020-09-14 184649.png)

* 加上control, n2/n1/1/2

  ![](C:\Users\chaoz\Pictures\Snipping Tools\Screenshot 2020-09-14 184938.png)

* 加上control, data20200911数据，-2/-1/0/1/2

  ![](C:\Users\chaoz\Pictures\Snipping Tools\Screenshot 2020-09-14 185219.png)

* 加上control, -1/0/1/2

  ![](C:\Users\chaoz\Pictures\Snipping Tools\Screenshot 2020-09-14 185359.png)

* 加上control, -1/0/2



##### **暂停测试 regression，转向至画图，confidence interval and coefficient**

* -6 to 6 year
* -5 to 5 year
* -4 to 4 year
* -3 to 3 year
* try different cluster method, such as cluster gvkey or cluster state
* also try to plot the BRI change.



使用confidence interval and coefficients +-6 来重新测试bri dummy

20200917 update: 重新转到BRI dummy，使用Bertrand测试BRI dummy和Cash ETRs的关系，需要使用dfbeta，让0年以前的不显著，让0年之后的显著

#### 20200918 和小虎语音

做这些测试是让settings有效

0之后多半是正显著

0之前可以正可以负，但是要不显著











