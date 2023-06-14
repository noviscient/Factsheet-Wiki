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
    1. Annualized Returns
    2. Annualized Volatility
6. [Return Statistics (Annualized)](#section5)
7. [Risk Statistics (Annualized)](#section6)
8. Historical Performance

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

**Note:** 1 Yr, YTD and Since January 2017(Since Inception) are already defined in the Performance Metrics section

## Risk Return Profile <a id="section4"></a>
**Description**:  
In this section, the strategy and its respective benchmarks annualized return and annualized volatility will be reflected on graph
![image](https://github.com/noviscient/Factsheet-Wiki/assets/114644478/f287af28-c961-4896-a6a4-b4302b9c8d42)  
**Location within Factsheet**: Page 1, top left hand side

<details>
  <summary> Annualized Return </summary>
  
  ### Description
  A measure of how much an investment has increased on average each year, during a specific time period. The y-axis of the graph
  ### Formula(words)
  $\ Annualized \space Return = \bar{R} * 252 $  
  $\bar{R}$: Represents the mean of the daily returns
  ### Formula(code)
  `rr_mu = rets_for_rr.mean() * YEARLY_LENGTH`  
  `YEARLY_LENGTH`: Number of trading days per year, 252  
  `rets_for_rr`: pandas.DataFrame of the daily returns of the strategy and its respective benchmarks
  ### Location  
  File: `plotting.py`  
  Function: `plot_risk_return_profile(self)`
</details>

<details>
  <summary> Annualized Volatility </summary>
  
  ### Description
  A measure of the dispersion of returns of a financial instrument over a given period, expressed in terms of an annualized standard deviation. The y-axis of the graph
  ### Formula(words)
  $\ Annualized \space Volatility = \sigma * \sqrt{252} $  
  $\sigma$: Standard deviation of the daily returns
  ### Formula(code)
  `rr_std = rets_for_rr.std() * np.sqrt(YEARLY_LENGTH)`  
  ### Location  
  File: `plotting.py`  
  Function: `plot_risk_return_profile(self)`
</details>

## Return Statistics (Annualized) <a id="section5"></a>
**Description**:  
In this section, the metrics are used to evaluate the returns from the chosen strategy
![image](https://github.com/noviscient/Factsheet-Wiki/assets/114644478/959cc2c9-e3e9-44d5-8c75-f5d13542ca07)  
**Location:**  Page 1, Below the Cumulative Monthly Performance Table

<details>
  <summary> 6 Month ROR </summary>
  
  ### Description
  Percentage return for the last 6 months
  ### Formula(words)
  $\ 6 \space Month \space ROR = [(1 + R_{N})(1 + R_{N-1})...(1 + R_{N-5})\]-1$ 
  ### Formula(code)
  `rets_stats['6 Month ROR'] = (self.stgy_mrets.iloc[-6:] + 1).prod() - 1`  
  ### Location  
  File: `calculation.py`  
  Function: `cal_return_stats(self)`
</details>

<details>
  <summary> Winning Month </summary>
  
  ### Description
  Average of the percentage returns for months where the trading strategy generated positive returns (returns > 0)
  ### Formula(words)
  $\ Winning \space Month = \frac{R_1 + R_2 + ... + R_W}{W} $  
  w: Each w represents a month where the trading strategy generated positive returns
  ### Formula(code)
  `rets_stats['Winning Month'] = (self.stgy_mrets > 0).mean()`  
  ### Location  
  File: `calculation.py`  
  Function: `cal_return_stats(self)`
</details>

<details>
  <summary> Average Winning Month </summary>
  
  ### Description
  
  ### Formula(words)
  $\  $  
  ### Formula(code)
  `rr_mu = rets_for_rr.mean() * YEARLY_LENGTH`  
  ### Location  
  File: `plotting.py`  
  Function: `plot_risk_return_profile(self)`
</details>

<details>
  <summary> Average Losing Month </summary>
  
  ### Description
  
  ### Formula(words)
  $\  $  
  ### Formula(code)
  `rr_mu = rets_for_rr.mean() * YEARLY_LENGTH`  
  ### Location  
  File: `plotting.py`  
  Function: `plot_risk_return_profile(self)`
</details>

**Note:** CAGR, 1 Year ROR (1 Yr), Year To Date ROR (YTD), Total Return(Since Inception) are already defined in the Performance Metrics section. 3 Month ROR (3M) and the 3 year ROR (3 Yr) are already defined in the Cumulative Monthly Performance section.


## Risk Statistics (Annualized) <a id="section6"></a>
