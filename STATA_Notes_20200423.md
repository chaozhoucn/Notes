### STATA中运用esttab生成表格范例和解释

Code: 

> eststo clear
> estpost summarize inflex_5y inflex_10y inflex_20y inflex_38y, detail
> esttab using table.rtf, replace collabels("N" "Mean" "Std" "Min" "P50" "Max") cells("count (fmt(%12.0fc)) mean (fmt(%4.3f)) sd (fmt(%4.3f)) min (fmt(%4.3f)) p50 (fmt(%4.3f)) max (fmt(%4.3f))") coeflabels(inflex_5y "Inflexibility 5 Years" inflex_10y "Inflexibility 10 Years" inflex_20y "Inflexibility 20 Years" inflex_38y "Inflexibility 38 Years")noobs nonumbers compress title(Summary)
>
> eststo clear
> eststo: qui xi: areg gaap_etr inflex_5y i.fyear, absorb(gvkey) cluster(gvkey) robust
> estadd local Year_Fixed_Effect "Yes", replace
> estadd local Firm_Fixed_Effect "Yes", replace
> estadd scalar Adjusted_R_Squared = e(r2_a)
> eststo: qui xi: areg cash_etr1 inflex_5y i.fyear, absorb(gvkey) cluster(gvkey) robust
> estadd local Year_Fixed_Effect "Yes", replace
> estadd local Firm_Fixed_Effect "Yes", replace
> estadd scalar Adjusted_R_Squared = e(r2_a)
> eststo: qui xi: areg cash_etr2 inflex_5y i.fyear, absorb(gvkey) cluster(gvkey) robust
> estadd local Year_Fixed_Effect "Yes", replace
> estadd local Firm_Fixed_Effect "Yes", replace
> estadd scalar Adjusted_R_Squared = e(r2_a)
> esttab est1 est2 est3 using table.rtf, append se drop(_If* _con*) b(3) stats(Year_Fixed_Effect Firm_Fixed_Effect N Adjusted_R_Squared, fmt(%3s %3s %12.0fc %4.2f) label("Year Fixed Effect" "Firm Fixed Effect" "Adjusted R Squared")) title(Regression of Inflexibility 5 Years) mtitles("GAAP ETR" "Cash ETR1" "Cash ETR2") rename(inflex_5y Inflexibility 5 Years) mgroups("A" "B", pattern(1 0 1))

部分代码释义：

> mgroups("A" "B", pattern(1 0 1))

这行代码的意思是将所有储存在eststo中的模型分组，其中`1`代表 *A* 分组的第一个模型，*0* 代表*A*模型中非第一个的模型，一个分组中可以有多个模型。

