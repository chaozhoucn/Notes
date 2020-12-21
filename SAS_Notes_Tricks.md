清空LOG

> dm 'log; clear;'; 

SAS日期的处理

characters to numeric, such as yyyy-mm

> new_variable = input (old_variable, anydtdte21);
>
> format new_variable date_format;

SAS 删除某一行

> if variable = "" then delete; 
>
> if variable = . then delete; 

使用宏选取某一日期之后的观察值

> %let date01 = "01Jan1990"d;
> if datadate >= &date01;

在SAS中让某一变量中的missing value赋值0或者其他值

> proc stdize out = data02 reponly missing = -9999;
> var date_diff;
> run; 

在SAS中让所有的numeric或者character赋值0或者其他值

> data yourdata;
> set yourdata;
> array change _numeric_;
> do over change;
> if change =. then change = 0; 
> end;
> run ;

在SAS中通过data命令找出重复的观察值并生成两个数据集

> data data02_01 data02_02;
> set data02;
> by gvkey;
> if first.gvkey then output data02_01;
> if not (first.gvkey and last.gvkey) then output data02_02;
> run; 

SAS中的PROC SQL用法

> proc sql options;
> select "columns"
> from "table_name | view_name"
> where "expression"
> group by "columns"
> having "expression"
> order by "columns";
> quit; 

PROC SQL可以直接计算由旧的变量通过计算生成的新变量
PROC SQL也可以直接计算由PROC SQL通过计算新生成的变量再继续计算生成变量
PROC SQL可以直接在SELECT语句中对变量注明格式，比如format = dollar10.2
PROC SQL可以直接对变量进行标签标注，比如label = 'Amount of Sales'
运用CASE...END语句可以对命令进行条件处理，比如

> proc sql;
> select state,
> case
> when sales between 0 and 100 then ‘Low'
> when sales between 100 and 200 then 'Avg'
> when sales between 200 and 500 then 'High' 
> end as salescat
> from ussales;
> quit;

PROC SQL可以在处理过程中同时使用ORDER BY达到和PROC SORT类似的效果

> proc sql;
> select state, sales
> from ussales
> order by state, sales DESC
> quit;

在PROC SQL语句中可以用where用来选取总体观察值中的一部分，比如

> proc sql;
> select *
> from ussales where state in ('OH', 'IN', 'IL');
> select *
> from ussales where state in ('OH', 'IN', 'IL') and sales > 500;
> quit;

但是，where语句不能用于在PROC SQL命令中生成的新的变量的判定

如果要使用where语句判定新的变量，需要在where语句中指定新的变量的计算方式

在PROC SQL中使用CREATE语句创建新的表格，CREATE仅可创建一个新的表格

使用PROC SQL合并表格不需要提前进行排序PROC SORT

> proc sql;
> select *
> from girls, boys
> where girls.state = boys.state;
> quit;

PROC SQL可以三张或多张表格的合并

> proc sql;
> select b.fname, b.lname, claims,
> e.storeno, state
> from benefits b, employee e, febsales febsales
> where b.fname = e.fname and 
> b.lname = e.lname and
> e.storeno = f.storeno and
> claims > 1000;
> quit;

在使用PROC SQL后可以使用UNION命令计算新的变量

> proc sql;
> create table YTDSALES as
> select TRANCODE, STORENO, SALES
> from JANSALES
> union
> select TRANCODE, STORENO, SALES * 0.99
> from FEBSALES;
> quit; 

使用DATA命令合并两个表格

> data data03;
> merge data01 data02 (in = mark01);
> by gvkey;
> run; 
> 	

使用SAS导出DATASET到STATA

> proc export data = data03 replace 
> outfile = "D:\Documents\Research\Data\Stata\taxavoid_inflex_90_18.dta";
> run; 

Winsorize macro

> proc univariate
> data = data10 noprint;
> var
> gaap_etr cash_etr1 cash_etr2 inflex_20y; 
> output out = data11
> pctlpre = 
> gaap_etr_ cash_etr1_ cash_etr2_ inflex_20y_
> pctlpts = 5, 95;
> quit;

> proc sql;
> create table data12 as select
> data10.*, data11.*
> from data10, data11;
> quit;

> %macro winsor(vbl);
> if &vbl>=&vbl._95 then &vbl=&vbl._95;
> if &vbl<=&vbl._5 and &vbl ne . then &vbl=&vbl._5;
> drop &vbl._5 &vbl._95;
> %mend winsor;

> data data12;
> set data12;
> %winsor (gaap_etr); %winsor (cash_etr1); %winsor (cash_etr2); %winsor (inflex_20y);
> run;

使用proc expand命令生成lag, moving average, moving average max and min;
还可以同时使用 moving standard deviation (movstd)命令。

> proc expand data = data02 out = data03 method = none; 
> 	by gvkey;
> 	id fyear;
> 	convert var01 = var01_lag01 /transformout = (lag 1);
> 	convert var01 = var01_lag02 /transformout = (lag 2);
> 	convert var01 = var01_lag03 /transformout = (lag 3);
> 	convert var01 = var01_lag04 /transformout = (lag 4);
> 	convert var01 = var01_lag05 /transformout = (lag 5);
> 	convert var01 = var01_lag06 /transformout = (lag 6);
> 	convert var01 = var01_lag07 /transformout = (lag 7);
> 	convert var01 = var01_lag08 /transformout = (lag 8);
> 	convert var01 = var01_lag09 /transformout = (lag 9);
> 	convert var01 = var01_lag10 /transformout = (lag 10);
> 	convert var01 = var01_lag11 /transformout = (lag 11);
> 	convert var01 = var01_lag12 /transformout = (lag 12);
> 	convert var01 = var01_lag13 /transformout = (lag 13);
> 	convert var01 = var01_lag14 /transformout = (lag 14);
> 	convert var01 = var01_lag15 /transformout = (lag 15);
> 	convert var01 = var01_lag16 /transformout = (lag 16);
> 	convert var01 = var01_lag17 /transformout = (lag 17);
> 	convert var01 = var01_lag18 /transformout = (lag 18);
> 	convert var01 = var01_lag19 /transformout = (lag 19);
> 	convert var01 = var01_movae / transformout = (movae 20);
> 	convert var01 = var01_max / transformout = (movmax 20);
> 	convert var01 = var01_min / transformout = (movmin 20);
> run; 

在使用proc expand的时候会生成很多warnings信息，可以使用proc printto将log储存在硬盘上。

> proc printto log = "D:\Documents\Research\Code\logbackup.log"; run; 

使用proc contents将dataset的变量名称生成到文件

> proc contents data = data05 noprint out = contents ; run;
> data _null_;
>   	set contents;
>   	file 'D:\Documents\Research\Code\Variables_name.txt';
>   	put name;
> run;