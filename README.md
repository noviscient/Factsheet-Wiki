# Factsheet-Wiki
Documentation for the Factsheet Calculations
##### Table of Contents
1. [Introduction](#section1)
2. [Performance Metrics](#section2)
    1. [1 Yr](#section2.1)
    2. [Since Inception](#section2.2)
    3. [YTD](#section2.3)
    4. [CAGR](#section2.4)
3. [Cumulative Monthly Performance](#section3)
    1. [Line Graph](#section3.1)
    2. [3M](#section3.2)
    3. [3 Yr](#section3.3)
5. [Risk Return Profile](#section4)
    1. [Annualized Returns](#section4.1)
    2. [Annualized Volatility](#section4.2)
6. [Return Statistics (Annualized)](#section5)
    1. [6 Month ROR](#section5.1)
    2. [Winning Month](#section5.2)
    3. [Average Winning Month](#section5.3)
    4. [Average Losing Month](#section5.4)
8. [Risk Statistics (Annualized)](#section6)
    1. [Downside Volatility](#section6.1)
    2. [Maximum Drawdown](#section6.2)
    3. [Value at Risk](#section6.3)
    4. [Expected Shortfall](#section6.4)
    5. [Beta (Market Index)](#section6.5)
    6. [Correlation (Market Index)](#section6.6)
    7. [Tail Correlation (Market Index)](#section6.7)
    8. [Sharpe Ratio](#section6.8)
    9. [Calmar Ratio](#section6.9)
10. [Historical Performance](#section7)
11. [Return Report](#section8)
    1. [Period](#section8.1)
    2. [Worst](#section8.2)
    3. [Average](#section8.3)
    4. [Median](#section8.4)
    5. [Last](#section8.5)
12. [Distribution of Monthly Returns](#section9)
13. [Maximum Drawdown and Recovery](#section10)
    1. [Depth ($)](#section10.1)
    2. [Length (Months)](#section10.2)
    3. [Recovery (Months)](#section10.3)
    4. [Start Date](#section10.4)
    5. [End Date](#section10.5)
14. [Daily Drawdown](#section11)


## Introduction <a id="section1"></a>
This section details the definition, formulas and code used for each metric in the factsheet. 
1. $N$: The total number of months the strategy has been active
2. $R_n$: The percentage returns of the strategy for the $nth$ month
3. `monthly_rets`: pd.Series type which represents all the months and its respective returns for each month
## Performance Metrics <a id="section2"></a>
**Description:**
The below metrics are used to evaluate and analyze the performance of the strategy over a specific period of time  
**Diagram:**  
![image](https://github.com/gabrielyong4/Analytics-Project/assets/114644478/cfabcee2-7fee-4b29-94bc-5af895aa99a0)  
**Location within Factsheet**: Page 1, top left hand side
<details>
  <summary>
      <a id="section2.1"> 1 Yr </a>
  </summary>
    
  ### Description
  Percentage return from the past 12 months  
  ### Formula(words)
  $\ \text{1 Yr} = [(1 + R_{N})(1 + R_{N-1})...(1 + R_{N-11})]-1 $  
  ### Formula(code)
  `(monthly_rets.iloc[-12:] + 1).prod() - 1`
  ### Location
  File: `calculation.py`  
  Function: `cal_key_perf(rets)`
</details>

<details>
  <summary> 
      <a id="section2.2"> Since Inception </a>
  </summary>
  
  ### Description
  Percentage return since the inception date
  ### Formula(words)
  $\ Since \space Inception = [(1 + R_1)(1 + R_2)...(1 + R_{N})]-1$  
  $R_i$: The percentage returns for the ith month
  ### Formula(code)
  `(monthly_rets + 1).prod() - 1`
  ### Location
  File: `calculation.py`  
  Function: `cal_key_perf(rets)`
</details>

<details>
  <summary>
      <a id="section2.3"> YTD </a>
  </summary>
  
  ### Description
  Percentage return from the start of current year to now
  ### Formula(words)
  $\ YTD = [(1 + R_1)(1 + R_2)...(1 + R_{j})]-1 $  
  $R_j$: The percentage returns for the j$^{th}$ month of the current year
  ### Formula(code)
  `monthly_rets.loc[datetime.datetime(monthly_rets.index[-1].year, 1, 1):] + 1).prod() - 1`
  ### Location
  File: `calculation.py`  
  Function: `cal_key_perf(rets)`
</details>

<details>
  <summary>
      <a id="section2.4"> CAGR </a>
  </summary>
  
  ### Description
  Compound Annual Growth Rate
  ### Formula(words)
  $\ CAGR = [(1 + R_1)(1 + R_2)...(1 + R_{N})]^{12 \over {N}}-1 $  
  $R_i$: The percentage returns for the ith month
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
  <summary> 
      <a id="section3.1"> Line Graph </a>
  </summary>
  
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
  <summary>
      <a id="section3.2"> 3M </a>
  </summary>
  
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
  <summary>
      <a id="section3.3"> 3 Yr </a>
  </summary>
  
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

**Note:** [1 Yr](#section2.1), [YTD](#section2.3) and [Since January 2017(Since Inception)](#section2.2) are already defined in the earlier sections. 

## Risk Return Profile <a id="section4"></a>
**Description**:  
In this section, the strategy and its respective benchmarks annualized return and annualized volatility will be reflected on graph
![image](https://github.com/noviscient/Factsheet-Wiki/assets/114644478/f287af28-c961-4896-a6a4-b4302b9c8d42)  
**Location within Factsheet**: Page 1, top left hand side

<details>
  <summary>
      <a id="section4.1"> Annualized Return </a>
  </summary>
  
  ### Description
  A measure of how much an investment has increased on average each year, during a specific time period. The y-axis of the graph
  ### Formula(words)
  $\ Annualized \space Return = \bar{R} * 252 $  
  $\bar{R}$: The mean of the daily returns
  ### Formula(code)
  `rr_mu = rets_for_rr.mean() * YEARLY_LENGTH`  
  `YEARLY_LENGTH`: Number of trading days per year, 252  
  `rets_for_rr`: pandas.DataFrame of the daily returns of the strategy and its respective benchmarks
  ### Location  
  File: `plotting.py`  
  Function: `plot_risk_return_profile(self)`
</details>

<details>
  <summary>
      <a id="section4.2"> Annualized Volatility </a>
  </summary>
  
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
  <summary>
      <a id="section5.1"> 6 Month ROR </a>
  </summary>
  
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
  <summary>
      <a id="section5.2"> Winning Month </a>
  </summary>
  
  ### Description
  Proportion of positive returns (returns > 0) in the strategy
  ### Formula(words)
  $\ Winning \space Month = \frac{x}{N}$  
  $x$: Total number of positive returns in the strategy
  ### Formula(code)
  `rets_stats['Winning Month'] = (self.stgy_mrets > 0).mean()`  
  `self.stgy_mrets`: Panda.Series of the monthly percentage returns for the strategy
  ### Location  
  File: `calculation.py`  
  Function: `cal_return_stats(self)`
</details>

<details>
  <summary>
      <a id="section5.3"> Average Winning Month </a>
  </summary>
  
  ### Description
  Average of the strategy's positive returns (returns > 0)
  ### Formula(words)
  $\ Average \space Winning \space Month = \frac{R_1 + R_2 + ... + R_W}{W}  $  
  $R_w$: The positive returns for month $w$
  ### Formula(code)
  `rets_stats['Average Winning Month'] = self.stgy_mrets[self.stgy_mrets > 0].mean()`  
  ### Location  
  File: `calculation.py`  
  Function: `cal_return_stats(self)`
</details>

<details>
  <summary>
      <a id="section5.4"> Average Losing Month </a>
  </summary>
  
  ### Description
  Average of the strategy's negative returns (returns < 0)
  ### Formula(words)
  $\ Average \space Losing \space Month = \frac{R_1 + R_2 + ... + R_W}{W} $   
  $R_w$: The negative returns for month $w$
  ### Formula(code)
  `rets_stats['Average Losing Month'] = self.stgy_mrets[self.stgy_mrets < 0].mean()`  
  ### Location  
  File: `calculation.py`  
  Function: `cal_return_stats(self)`
</details>

**Note:** [CAGR](#section2.4), [1 Year ROR (1 Yr)](#section2.1), [Year To Date ROR (YTD)](#section2.3), [Total Return (Since Inception)](#section2.2), [3 Month ROR (3M)](#section3.2) and the [3 year ROR (3 Yr)](#section3.3) are already defined in the above sections 


## Risk Statistics (Annualized) <a id="section6"></a>
**Description**:  
In this section, the metrics are used to evaluate the risks from the chosen strategy  
![image](https://github.com/noviscient/Factsheet-Wiki/assets/114644478/5e3adf8a-d5e3-412f-99b5-31d4f18537de)  
**Location within Factsheet:**  Page 1, Next to the Return Statistics section

<details>
  <summary>
      <a id="section6.1"> Downside Volatility </a>
  </summary>
  
  ### Description
  Measure of downside risk that focuses on returns that fall below the risk-free benchmark. The risk-free benchmark will depend on the geography where the strategy is denominated and the market traded. For US and Global strategies we will be using the 13 week Treasury Bill rate. 
  ### Formula(words) 
  $$\ Annualised \space Downside \space Volatility = \sqrt{\frac{\sum\limits_{t=1}^{n} [min(R_{st} - R_{ft}, 0)]^2}{n}} - \sqrt{No. \space of \space Trading \space Days \space per \space year}$$
  $n$: Total Number of Returns  
  $min(X,Y)$: Minimum out of the 2 parameters. For the numerator we only want the negative excess returns  
  $R_{st}$: Strategy/Product Returns at time t  
  $R_{ft}$: Risk-free Benchmark Returns at time t  
  $No. \space of \space Trading \space Days \space per \space year$: 252
  ### Formula(code)
  `risk_stats["Downside Volatility"] = ((excess_rets[excess_rets < 0]**2).sum() /len(excess_rets))**0.5 * scale**0.5`  
  ### Location  
  File: `calculation.py`  
  Function: `cal_risk_stats(self)`
</details>

<details>
  <summary>
      <a id="section6.2"> Maximum Drawdown </a>
  </summary>
  
  ### Description
  A measure of the strategy's largest drop in returns from peak to a trough (lowest point), before the strategy starts to recover.  
  ### Formula(words)
  1. Compute the cumulative returns series, $C$:
     $$\ C = [C_1, C_2, \ldots , C_T] $$  
     where the C_t, the cumulative return at each time point $t$, is calculated by:
     $$\ C_t = \prod\limits_{i=0}^{t} (1 + R_i) $$
     where $t$ The date of the returns series.
  2. Calculate the drawdown series, $D$:
     $$\ D = [D_1, D_2, \ldots , D_T] $$  
     where the D_t, the drawdown at each time period $t$, is calculated by 
     $$\ D_t = \frac{C_t}{{\max\limits_{i=0}^{t}(C_i)}} - 1 $$
     where $\max\limits_{i=0}^{t}(C_i)$ is the maximum cumulative return observed up to time $t$
  3. Find the absolute maximum drawdown:
     $$\ \text{Max Drawdown} = \left| \min(D) \right| $$
     where $\ \text{Max Drawdown} $ The absolute value of the lowest drawdown observed in the specified time period and $D$ The whole drawdown time series
  ### Formula(code)
  ```python
  def cal_underwater(rets):
    cum_rets = (rets + 1).cumprod()
    underwater = cum_rets / np.maximum.accumulate(cum_rets) - 1
    return underwater
  ...
  class Calculation:
      ...
      def cal_risk_stats(self):
          ...
          risk_stats['Maximum Drawdown'] = abs(cal_underwater(stgy_rets).min())
          ...
  ```
  ### Location  
  File: `calculation.py`  
  Function: `cal_underwater(rets), cal_risk_stats(self)`
</details>

<details>
  <summary>
      <a id="section6.3"> Value at Risk (Value at Risk) </a>
  </summary>
  
  ### Description
  Measures the extent of possible financial losses within the strategy/product over a specific time frame given a certain significance level (alpha)
  ### Formula(words)
  $\ \text{Value at Risk} = Q(\alpha, \text{rets}) $  
  $\ \alpha$: The significance level  
  $rets$: Represents all the returns in the strategy  
  $Q$: Finds the quantile based on the significance level and the returns in the strategy
  ### Formula(code)
  ```python
  def cal_var(rets, alpha=0.05):
    rets = rets[~np.isnan(rets)]
    var = np.quantile(rets, alpha)
    return var
  ...
  class Calculation:
      ...
      def cal_risk_stats(self):
          ...
          risk_stats['Value at Risk'] = -cal_var(self.stgy_mrets)
          ...
  ``` 
  ### Location  
  File: `calculation.py`  
  Function: `cal_risk_stats(self)`, `cal_var(rets, alpha=0.05)`
</details>

<details>
  <summary>
      <a id="section6.4"> Expected Shortfall </a>
  </summary>
  
  ### Description
  Measures the weighted average of the "extreme" losses in the tail of the distribution of possible returns, beyond the VaR cutoff point and given a certain significance level (alpha)
  ### Formula(words)
  Given $\ \alpha < 0.05$,
  $$\ \text{ES} = \frac{1}{N_<} \sum\limits_{i=1}^{N<} x_i $$  
  $N_<$: The number of returns lesser than the $\ \alpha$ quantile  
  $x_i$: Represents each return in the set
  ### Formula(code)
  ```python
  def cal_empirical_es(rets, alpha=0.05):
    rets = rets[~np.isnan(rets)]
    if alpha >= 0.5: # if the user inputs losses
        es = rets[rets >= np.quantile(rets, alpha)].mean()
    else: # if the user inputs returns
        es = rets[rets <= np.quantile(rets, alpha)].mean()
    return es
  ...
  class Calculation:
      ...
      def cal_risk_stats(self):
          ...
          risk_stats['Expected Shortfall'] = -cal_empirical_es(self.stgy_mrets)
          ...
  ``` 
  ### Location  
  File: `calculation.py`  
  Function: `cal_risk_stats(self)`, `cal_empirical_es(rets, alpha=0.05)`
</details>

<details>
  <summary>
      <a id="section6.5"> Beta (Market Index) </a>
  </summary>
  
  ### Description
  Measures the strategy's volatility in relation to the overall market. The market will depend on the geography where the strategy is denominated and the market traded.
  ### Formula(words)
  $\ R_i = \beta{R_m} + \epsilon $   
  $R_m$: Represents market returns  
  $R_i$: Represents strategy returns  
  $\ \beta $: Our objective  
  $\ \epsilon $: Error term or residuals, captures the unexplained part of stock returns
  ### Formula(code)
  ```python
  def cal_risk_stats(self):
      ...
      risk_stats['Beta (Market Index)'] = OLS(
        stgy_rets.values,
        add_constant(
            rets_all[self.market_rets.name].values)).fit().params[1]
      ...
  ```  
  Above code finds the Beta, which corresponds to the coefficient of the market returns (`results.params[1]`)
  ### Location  
  File: `calculation.py`  
  Function: `cal_risk_stats(self)`
</details>

<details>
  <summary>
      <a id="section6.6"> Correlation (Market Index) </a>
  </summary>
  
  ### Description
  A measure that determines how the strategy will move in relation to the market. The market will depend on the geography where the strategy is denominated and the market traded
  ### Formula(words)
  $\ correlation = \frac{{\sum ((x - \bar{x})(y - \bar{y}))}}{{\sqrt{{\sum ((x - \bar{x})^2)}} \cdot \sqrt{{\sum ((y - \bar{y})^2)}}}} $   
  $x$: represents one set of stock returns  
  $y$: The other set of stock returns  
  $\bar{x}$: The mean (average) of the x values.  
  #\bar{y}$: The mean (average) of the y values.  
  ### Formula(code)
  `risk_stats['Correlation (Market Index)'] = rets_all[[
            self.stgy_rets.name, self.market_rets.name
        ]].corr().iloc[0, 1]`  
  ### Location  
  File: `calculation.py`  
  Function: `cal_risk_stats(self)`
</details>

<details>
  <summary>
      <a id="section6.7"> Tail Correlation (Market Index) </a>
  </summary>
  
  ### Description
  Refers to the correlation between the extreme events or outliers of the strategy and the market. The market will depend on the geography where the strategy is denominated and the market traded
  ### Formula(words)
  1. Standardise the returns for series $i$ at each time $t$, Z_{i, t} where i is the `strat` or `mkt`:
  $$\ Z_{i, t} = \frac{R_{i,t}}{\sigma_i} $$  
  $R_{i, t}$: The returns of series $i$ at time $t$  
  $\ \sigma_i $: The standard deviation of series $i$  
  2. Find the weighted average portfolio return series at each time $t$, $Z_{p, t}$:  
  $$\ Z_{p, t} = Z_{strat, t}(w) + Z_{mkt, t}(1-w) $$  
  $w$: The weight assigned to the strategy
  3. Find the mean of all the return series, $\ \mu_i $ where i is either `strat`, `mkt`, `portfolio (p)`:
  $$\ \mu_i = \frac{\sum\limits_{t=1}^{N_i}R_{i,t}}{N_i} $$
  $ N_i $: Total number of returns for series $i$  
  4. Find the expected shortfall of all the return series, $ES_i$ where i is either `strat`, `mkt`, `portfolio (p)`:  
  Use the equation in the [Expected Shortfall](#section6.4) section on each series
  5. Find the Tail Correlation: 
  $$\ \text{Tail Correlation} = \frac{(ES_{p} - \mu_{p})^2 - w^2(ES_{strat} - \mu_{strat})^2 - (1-w)^2(ES_{mkt} - \mu_{mkt})^2}{2w(1-w)(ES_{strat} - \mu_{strat})(ES_{mkt} - \mu_{mkt})} $$
  ### Formula(code)
```python
def cal_rm_corr(rets, w=0.5, func=cal_empirical_es, **args):
    rets = rets[~np.isnan(rets).any(axis=1)]
    rets = rets / rets.std(axis=0)
    rets_1, rets_2 = rets[:, 0], rets[:, 1]
    rets_p = rets_1 * w + rets_2 * (1 - w)
    mu = [r.mean() for r in [rets_1, rets_2, rets_p]]
    rm = [func(r, **args) for r in [rets_1, rets_2, rets_p]]
    corr = ((rm[2] - mu[2])**2 - w**2 * (rm[0] - mu[0])**2 - (1 - w)**2 * (rm[1] - mu[1])**2) \
        / (2 * w * (1 - w) * (rm[0] - mu[0]) * (rm[1] - mu[1]))
    return corr
  ...
  class Calculation:
      ...
      def cal_risk_stats(self):
          ...
          risk_stats['Tail Correlation (Market Index)'] = cal_rm_corr(
              rets_all[[self.stgy_rets.name, self.market_rets.name]].values)
          ...
``` 
  ### Location  
  File: `calculation.py`  
  Function: `cal_risk_stats(self)`, `def cal_rm_corr(rets, w=0.5, func=cal_empirical_es, **args)`
</details>

<details>
  <summary>
      <a id="section6.8"> Sharpe Ratio </a>
  </summary>
  
  ### Description
  Measure of an investment's risk-adjusted performance, calculated by comparing its return to that of a risk-free benchmark. The risk-free benchmark will depend on the geography where the strategy is denominated and the market traded. For US and Global strategies we will be using the 13 week Treasury Bill rate.

  ### Formula(words)
  1. Find the excess returns at each time $t$, $R_{excess, t}$:  
  $$\ R_{excess, t} = R_{strat, t} - R_{f,t} $$  
  $R_{strat, t}$: The strategy returns at time $t$  
  $R_{f, t}$: The risk-free benchmark returns at time $t$  

  2. Find the Sharpe Ratio:  
  $$\ \text{Sharpe Ratio} = \frac{E(R_{excess})}{\sigma_{excess}} * \sqrt{\text{YEARLY LENGTH}} $$  
  $E(R_{excess})$: The mean of the excess returns  
  $\sigma_{strat}$: The standard deviation of the excess returns  
  $YEARLY LENGTH$: 272, Total number of trading days per year  

  ### Formula(code)
  `risk_stats['Sharpe Ratio'] = excess_rets.mean() / excess_rets.std() * np.sqrt(scale)`

  ### Location  
  File: `calculation.py`  
  Function: `cal_risk_stats(self)`
</details>

<details>
  <summary>
      <a id="section6.9"> Calmar Ratio </a>
  </summary>
  
  ### Description
  Measure of risk-adjusted returns for investment funds such as hedge funds.  
  Note: Calmar Ratio focuses on worst-case scenario through the maximum drawdown while the Sharpe Ratio considers overall volatility  

  ### Formula(words)
  1. Find the excess returns at each time $t$, $R_{excess, t}$:
  $$\ R_{excess, t} = R_{strat, t} - R_{f,t} $$  
  $R_{strat, t}$: The strategy returns at time $t$  
  $R_{f, t}$: The risk-free benchmark returns at time $t$  

  2. Find the Maximum Drawdown, $\ \text{Maximum Drawdown} $:  
  Calculate [Maximum Drawdown](#section6.2) from the above section.  

  3. Find the Calmar Ratio:  
  $$\ \text{Calmar Ratio} = \frac{E(R_{excess})}{\text{Maximum Drawdown}} * \text{YEARLY LENGTH} $$  
  $E(R_{excess})$: The mean of the excess returns  
  $YEARLY LENGTH$: 272, Total number of trading days per year  

  ### Formula(code)
  `risk_stats['Calmar Ratio'] = excess_rets.mean() / risk_stats['Maximum Drawdown'] * scale`  

  ### Location  
  File: `calculation.py`  
  Function: `cal_risk_stats(self)`
</details>

**Note:** [Volatility](#section4.2) is in the above section.  

## Historical Performance (Up to 5 Years) <a id="section7"></a>
**Description**:  
The past performance of the strategy  
![image](https://github.com/noviscient/Factsheet-Wiki/assets/114644478/742c88ed-172f-48ef-b767-771b9817d539)  
**Location within Factsheet:**  Page 1, Bottom of the page  

### Formula(words)
Converting the daily returns into monthly returns for each month $m$, $R_m$:
$$\ R_m = [(D_1 + 1)(D_2 + 1)...(D_I + 1)] - 1 $$
$D_i$: The return on day $i$ in month $m$
$I$: The total number of days in that month $m$
### Formula(code)
Plotting of the graph code
```python
def format_table(self, version):
  ...
  # Historical Performance
  rets = self.data.stgy_mrets
  df = (rets + 1).groupby(
      [rets.index.year.rename('year'),
        rets.index.month.rename('month')]).prod() - 1
  ...
```

### Location  
  File: `plotting.py`  
  Function: `format_table(self)`

## Return Report <a id="section8"></a>
**Description**:  
The past performance of the strategy based on the rolling period the returns have been calculated on. It will also describe the returns by displaying the best, worst, average, median and last returns for each different period.  

The metrics will be analysed using the column names as references.  
![image](https://github.com/noviscient/Factsheet-Wiki/assets/114644478/5ca953c4-3aa6-46ac-a91a-29e875cedb76)  
**Location within Factsheet:**  Page 2, top left of the page  

<details>
  <summary>
      <a id="section8.1"> Period </a>
  </summary>
  
  ### Description
  This column provides the rolling window calculation size for the monthly returns.   
  ### Formula(words)
  1. Find the rolling calculation size:
  To do this we find the total number of months present in the period. For example:   
  $\ \text{Window Size (6 Months)} = 6 $  
  $\ \text{Window Size (3 Years)} = 3 \times 12 = 36 $

  2. Calculate the compounded return for each month $m$, $R_m$:
  $$\ R_m = (\prod\limits_{m-window}^{T = m}{R_i + 1}) - 1 $$  

  where the first month $m$ will be equal to the window size. For example, for the `3 Years` Period, the first return calculated will be the rolling period return for the 36th month, $R_{36}$, which uses the previous 36 months to calculate the $R_{36}$ compounded return. This process will keep repeating until there is less than 36 months of data available to do the calculations. 


  ### Formula(code)
  ```python
  def cal_return_report(self):
    ...
    rets_report = OrderedDict()
    rets_report['1 Month'] = f((self.stgy_mrets +
                                1).rolling(1).apply(np.prod, raw=False) -
                                1)
    # more Period calculations
    rets_report['5 Years'] = f((self.stgy_mrets +
                                1).rolling(60).apply(np.prod, raw=False) -
                                1)
    ...
  ```

  ### Location  
  File: `calculation.py`  
  Function: `cal_return_report(self)`
</details>

<details>
  <summary>
      <a id="section8.2"> Best </a>
  </summary>
  
  ### Description
  This column provides the maximum return from the respective rolling period return series. 
  ### Formula(words)
  Let $R = {r_1, r_2, \ldots, r_n}$ represent the return series. We seek to determine $\max(R)$, which The maximum value within the series.

  ### Formula(code)
  ```python
  def cal_return_report(self):
    def f(rets):
      return pd.Series({
          'Best': rets.max(),
          ...
      })
  ```

  ### Location  
  File: `calculation.py`  
  Function: `cal_return_report(self)`
</details>

<details>
  <summary>
      <a id="section8.2"> Worst </a>
  </summary>
  
  ### Description
  This column provides the lowest return from the respective rolling period return series. 
  ### Formula(words)
  Let $R = {r_1, r_2, \ldots, r_n}$ represent the return series. We seek to determine $\min(R)$, which The minimum value within the series.

  ### Formula(code)
  ```python
  def cal_return_report(self):
    def f(rets):
      return pd.Series({
          ...
          'Worst': rets.min(),
          ...
      })
  ```

  ### Location  
  File: `calculation.py`  
  Function: `cal_return_report(self)`
</details>

<details>
  <summary>
      <a id="section8.3"> Average </a>
  </summary>
  
  ### Description
  This column calculates the average return from the respective rolling period return series. 
  ### Formula(words)
  Let $R = {r_1, r_2, \ldots, r_n}$ represent the return series (following the rolling window calculation). We seek to determine:  
  $\ \bar{R} = \frac{\sum\limits_{i=1}^{len(R)}R_i}{len(R)} $  

  ### Formula(code)
  ```python
  def cal_return_report(self):
    def f(rets):
      return pd.Series({
          ...
          'Average': rets.mean(),
          ...
      })
  ```

  ### Location  
  File: `calculation.py`  
  Function: `cal_return_report(self)`
</details>

<details>
  <summary>
      <a id="section8.4"> Median </a>
  </summary>
  
  ### Description
  This column calculates the median return, 50th percentile, from the respective rolling period return series. 
  ### Formula(words)
  Let $R = {r_1, r_2, \ldots, r_n}$ represent the return series. We seek to determine the median, denoted by $\text{median}(R)$, which The middle value when the series is arranged in ascending or descending order.

  ### Formula(code)
  ```python
  def cal_return_report(self):
    def f(rets):
      return pd.Series({
          ...
          'Median': rets.median(),
          ...
      })
  ```

  ### Location  
  File: `calculation.py`  
  Function: `cal_return_report(self)`
</details>

<details>
  <summary>
      <a id="section8.5"> Last </a>
  </summary>
  
  ### Description
  This column calculates the latest return from the respective rolling period return series. 
  ### Formula(words)
  Let $R = {r_1, r_2, \ldots, r_n}$ represent the return series. We seek to determine the latest return, denoted by $R_n$, which The latest/last value in the series.

  ### Formula(code)
  ```python
  def cal_return_report(self):
    def f(rets):
      return pd.Series({
          ...
          'Last': rets.iloc[-1]
      })
  ```

  ### Location  
  File: `calculation.py`  
  Function: `cal_return_report(self)`
</details>

## Distribution of Monthly Returns <a id="section9"></a>
**Description**:  

**Location:**  Page 2, Top right hand side

## Maximum Drawdown and Recovery <a id="section10"></a>
**Description**:  
A table that displays the statistics for the top 5 maximum drawdown depth values which represent the downturns in the strategy. The section also describe other drawdown values such as the `Length (Months)`, `Recovery (Months)`, `Start date` and `End date` of the drawdown.  
<img width="351" alt="image" src="https://github.com/noviscient/Factsheet-Wiki/assets/114644478/91878dab-ebdc-4b43-a4f9-0077263239a7">  

**Location:**  Page 2, Below the Return Report section

<details>
  <summary>
      <a id="section10.1"> Depth (%) </a>
  </summary>
  
  ### Description
  Measures the magnitude of the loss experienced during the drawdown period. 
  ### Formula(words)
  The formula used is the same as the one in the [Maximum Drawdown](#section6.2) however the difference is in the last step where instead of finding the absolute value, we find the actual value:  
  $$\ \text{Depth} = \min_{t}(D) $$
  where $Depth$ The actual value of the lowest drawdown observed. Then we can convert it to percentage by multipling $Depth$ by 100.  

  ### Formula(code)
  ```python
  def cal_drawdown_report(self):
    def get_max_dd_report(underwater):
        depth = underwater.min()
        ...
        return depth, peak, valley, recovery
    ...
    underwater = cal_underwater(self.stgy_rets)
    for i in range(5):
      try:
        depth, peak, valley, recovery = get_max_dd_report(
            underwater.values)
      ...
      dd_report['Depth (%)'] = depth * 100
      ...
  ```

  ### Location  
  File: `calculation.py`  
  Function: `cal_drawdown_report(self)`
</details>

<details>
  <summary>
      <a id="section10.2"> Length (Months) </a>
  </summary>
  
  ### Description
  The length of time, in months, from the peak to the respective valley for each drawdown event. The estimated length of time will be rounded up.
  ### Formula(words)
  $\ \text{Length (Months)} = \lceil \text{Valley Date} - \text{Peak Date} \rceil $  
  $\ \lceil x \rceil $: Rounding up the $x$ value  
  $\ \text{Valley Date} $: The date the strategy reaches its maximum drawdown during each drawdown period  
  $\ \text{Peak Date} $: The date when the strategy reached its highest value before experiencing its largest decline until the $\ \text{Valley Date} $
  ### Formula(code)
  ```python
  def cal_drawdown_report(self):
    def get_max_dd_report(underwater):
      depth = underwater.min()
      ...
      return depth, peak, valley, recovery
    ...
    def f(d1, d2):
            return np.ceil((d1.year - d2.year) * 12 + (d1.month - d2.month) +
                           (d1.day - d2.day) / 32)
    underwater = cal_underwater(self.stgy_rets)
    for i in range(5):
      try:
        # print(f'Underwater {i}:{underwater}')
        depth, peak, valley, recovery = get_max_dd_report(
        underwater.values)
      except IndexError:
        break
      ...
      start_date, valley_date = underwater.index[peak], underwater.index[valley]
      ...
      dd_report['Length (Months)'] = f(valley_date, start_date)
      ...
  ```

  ### Location  
  File: `calculation.py`  
  Function: `cal_drawdown_report(self)`
</details>

<details>
  <summary>
      <a id="section10.3"> Recovery (Months) </a>
  </summary>
  
  ### Description
  Refers to the duration it takes for the strategy to fully recover from a drawdown and reach a new peak value (when the drawdown becomes 0). The estimated length of time will be rounded up.
  ### Formula(words)
  Given that for that drawdown event, the strategy reaches a new peak value (drawdown becomes 0),  
  $\ \text{Recovery (Months)} = \lceil \text{Recovery Date} - \text{Valley Date} \rceil $  
  $\ \lceil x \rceil $: Rounding up the $x$ value  
  $\ \text{Valley Date} $: The date the strategy reaches its maximum drawdown during each drawdown period  
  $\ \text{Recovery Date} $: The date when the strategy reached its highest value after the date the strategy experienced its maximum drawdown
  ### Formula(code)
  ```python
  def cal_drawdown_report(self):
    def get_max_dd_report(underwater):
      depth = underwater.min()
      ...
      return depth, peak, valley, recovery
    ...
    def f(d1, d2):
            return np.ceil((d1.year - d2.year) * 12 + (d1.month - d2.month) +
                           (d1.day - d2.day) / 32)
    underwater = cal_underwater(self.stgy_rets)
    for i in range(5):
      try:
        # print(f'Underwater {i}:{underwater}')
        depth, peak, valley, recovery = get_max_dd_report(
        underwater.values)
      except IndexError:
        break
      ...
      if not pd.isnull(recovery):
        end_date = underwater.index[recovery]
        rec = f(end_date, valley_date)
      else:
        end_date = np.nan
        rec = np.nan
      dd_report['Recovery (Months)'] = rec
      ...
  ```

  ### Location  
  File: `calculation.py`  
  Function: `cal_drawdown_report(self)`
</details>

<details>
  <summary>
      <a id="section10.4"> Start Date </a>
  </summary>
  
  ### Description
  Refers to the beginning of the drawdown period. The date when the strategy reaches its peak value before declining to the maximum drawdown value. 
  ### Formula(words)
  For the respective drawdown events,  
  $\ \text{Start Date} = \text{Peak Date} $
  ### Formula(code)
  ```python
  def cal_drawdown_report(self):
    def get_max_dd_report(underwater):
      depth = underwater.min()
      ...
      return depth, peak, valley, recovery
    ...
    underwater = cal_underwater(self.stgy_rets)
    for i in range(5):
      try:
        # print(f'Underwater {i}:{underwater}')
        depth, peak, valley, recovery = get_max_dd_report(
        underwater.values)
      except IndexError:
        break
      ...
      start_date, valley_date = underwater.index[peak], underwater.index[valley]
      ...
      dd_report['Start date'] = start_date
      ...
  ```

  ### Location  
  File: `calculation.py`  
  Function: `cal_drawdown_report(self)`
</details>

<details>
  <summary>
      <a id="section10.5"> End Date </a>
  </summary>
  
  ### Description
  Refers to the end of the drawdown period. The date when the strategy reaches its valley value. 
  ### Formula(words)
  For the respective drawdown events,  
  $\ \text{End Date} = \text{Valley Date} $
  ### Formula(code)
  ```python
  def cal_drawdown_report(self):
    def get_max_dd_report(underwater):
      depth = underwater.min()
      ...
      return depth, peak, valley, recovery
    ...
    underwater = cal_underwater(self.stgy_rets)
    for i in range(5):
      try:
        # print(f'Underwater {i}:{underwater}')
        depth, peak, valley, recovery = get_max_dd_report(
        underwater.values)
      except IndexError:
        break
      ...
      start_date, valley_date = underwater.index[peak], underwater.index[valley]
      ...
      dd_report['End date'] = valley_date
      ...
  ```

  ### Location  
  File: `calculation.py`  
  Function: `cal_drawdown_report(self)`
</details>
