# Factsheet-Wiki
Documentation for the Factsheet Calculations
##### Table of Contents
1. [Introduction](#section1)
2. [Performance Metrics](#section2)
    1. 1 Yr
    2. Since Inception
    3. YTD
    4. CAGR
3. [Cumulative Monthly Performance](#section3)
    1. Line Graph
    2. 3M
    3. 3 Yr
5. [Risk Return Profile](#section4)

## Introduction <a id="section1"></a>
This section is just to lay down the context for all the formulas and code
1. $N$: Represents the total number of months the strategy has been active(?)
2. $R_n$: Represents the **percentage returns** of the strategy for the $nth$ month
3. `monthly_rets`: pd.Series type which represents all the months and its respective returns for each month
## Performance Metrics <a id="section2"></a>
**Description:**
The below metrics are used to evaluate and analyze the performance of the strategy over a specific period of time 
**Diagram:**  
![image](https://github.com/gabrielyong4/Analytics-Project/assets/114644478/cfabcee2-7fee-4b29-94bc-5af895aa99a0)  
**Location within Factsheet**: Page 1, top left hand side
<details>
  <summary> 1 Yr </summary>
    
  ### Description
  Percentage return from the past 12 months  
  ### Formula(words)
  $\ 1 \space Yr = [(1 + R_{N})(1 + R_{N-1})...(1 + R_{N-11})\]-1$  
  ### Formula(code)
  `(monthly_rets.iloc[-12:] + 1).prod() - 1`
  ### Location
  File: `calculation.py`  
  Function: `cal_key_perf(rets)`
</details>

<details>
  <summary> Since Inception </summary>
  
  ### Description
  Percentage return since the inception date
  ### Formula(words)
  $\ Since \space Inception = [(1 + R_1)(1 + R_2)...(1 + R_{N})\]-1$  
  $R_i$: Represents the percentage returns for the ith month
  ### Formula(code)
  `(monthly_rets + 1).prod() - 1`
  ### Location
  File: `calculation.py`  
  Function: `cal_key_perf(rets)`
</details>

<details>
  <summary> YTD </summary>
  
  ### Description
  Percentage return from the start of current year to now
  ### Formula(words)
  $\YTD = [(1 + R_1)(1 + R_2)...(1 + R_{j})\]-1$  
  $R_j$: Represents the percentage returns for the jth month of the current year
  ### Formula(code)
  `monthly_rets.loc[datetime.datetime(monthly_rets.index[-1].year, 1, 1):] + 1).prod() - 1`
  ### Location
  File: `calculation.py`  
  Function: `cal_key_perf(rets)`
</details>

<details>
  <summary> CAGR </summary>
  
  ### Description
  Compound Annual Growth Rate
  ### Formula(words)
  $\CAGR = [(1 + R_1)(1 + R_2)...(1 + R_{N})\]^{12 \over {N}}-1$  
  $R_i$: Represents the percentage returns for the ith month
  ### Formula(code)
  `(monthly_rets + 1).prod()**(12 / len(monthly_rets)) - 1`
  ### Location
  File: `calculation.py`  
  Function: `cal_key_perf(rets)`
</details>

## Cumulative Monthly Performance <a id="section3"></a>
**Description**:  
In this section, the given strategy's monthly performance is compared against certain benchmarks. There will be two main breakdowns:
- Line graph of the monthly performance of the strategy and its benchmarks
![image](https://github.com/gabrielyong4/Analytics-Project/assets/114644478/fad571af-0e03-4c87-a718-068e14ae6efb)
- Table showing the performance metrics(3M, YTD, 1 Yr, 3 Yr, Since January 2017) for the strategy and its benchmarks
![image](https://github.com/gabrielyong4/Analytics-Project/assets/114644478/8236cbd1-dcf2-4464-899a-628988d3cc74) 
**Location within Factsheet**: Page 1, top right side  

<details>
  <summary> Line Graph </summary>
  
  ### Description
  A graph that shows the monthly performance of the fund and its respective benchmarks
  ### Graph Plot Location
  File: `plotting.py`  
  Function: `plot_cum_rets()`  
  ### Calculation Location  
  File: `calculation.py`  
  Function: `cal_key_perf(rets)`
</details>

<details>
  <summary> 3M </summary>
  
  ### Description
  Percentage return for the last 3 months
  ### Formula(words)
  $\ 3M = [(1 + R_{N-2})(1 + R_{N-1})(1 + R_{N})\]-1$
  ### Formula(code)
  `(monthly_rets.iloc[-3:] + 1).prod() - 1`
  ### Calculation Location  
  File: `calculation.py`  
  Function: `cal_key_perf(rets)`
</details>

<details>
  <summary> 3 Yr </summary>
  
  ### Description
  Percentage return from the past 36 months  
  ### Formula(words)
  $\ 1 \space Yr = [(1 + R_{N})(1 + R_{N-1})...(1 + R_{N-35})\]-1$ 
  ### Formula(code)
  `(monthly_rets.iloc[-36:] + 1).prod() - 1`
  ### Location  
  File: `calculation.py`  
  Function: `cal_key_perf(rets)`
</details>

**Note:** 1 Yr and YTD are already defined in the Performance Metrics section

