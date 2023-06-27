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
10. Historical Performance

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
  <summary>
      <a id="section2.1"> 1 Yr </a>
  </summary>
    
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
  <summary> 
      <a id="section2.2"> Since Inception </a>
  </summary>
  
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
  <summary>
      <a id="section2.3"> YTD </a>
  </summary>
  
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
  <summary>
      <a id="section2.4"> CAGR </a>
  </summary>
  
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
  $R_w$: Represents the positive returns for month $w$
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
  $R_w$: Represents the negative returns for month $w$
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
  A measure of an asset's largest price drop from peak to a trough
  ### Formula(words)
  1. Compute the cumulative returns series:
     $$\ C_t = \prod\limits_{i=0}^{t} (1 + R_i) $$
     where $t$ represents the date of the returns series.
  2. Calculate the drawdown series:
     $$\ D_t = \frac{C_t}{{\max\limits_{i=0}^{t}(C_i)}} - 1 $$
     where $D_t$ represents the drawdown at time $t$ and $\max\limits_{i=0}^{t}(C_i)$ is the maximum cumulative returns observed up to time $t$
  3. Find the absolute maximum drawdown:
     $$\ \text{Max Drawdown} = \left| \min_{t}(D_t) \right| $$
     where $\\text{Max Drawdown}$ represents the absolute value of the lowest drawdown observed. 
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
  $\ \alpha$: Represents the significance level  
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
  $N_<$: Represents the number of returns lesser than the $\ \alpha$ quantile  
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
  $y$: represents the other set of stock returns  
  $\bar{x}$: represents the mean (average) of the x values.  
  #\bar{y}$: represents the mean (average) of the y values.  
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
  $R_{i, t}$: represents the returns of series $i$ at time $t$  
  $\ \sigma_i $: represents the standard deviation of series $i$  
  2. Find the weighted average portfolio return series at each time $t$, $Z_{p, t}$:  
  $$\ Z_{p, t} = Z_{strat, t}(w) + Z_{mkt, t}(1-w) $$  
  $w$: represents the weight assigned to the strategy
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
  $R_{strat, t}$: represents the strategy returns at time $t$  
  $R_{f, t}$: represents the risk-free benchmark returns at time $t$  

  2. Find the Sharpe Ratio:  
  $$\ \text{Sharpe Ratio} = \frac{E(R_{excess})}{\sigma_{excess}} * \sqrt{\text{YEARLY LENGTH}} $$  
  $E(R_{excess})$: represents the mean of the excess returns  
  $\sigma_{strat}$: represents the standard deviation of the excess returns  
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
  $R_{strat, t}$: represents the strategy returns at time $t$  
  $R_{f, t}$: represents the risk-free benchmark returns at time $t$  

  2. Find the Maximum Drawdown, $\ \text{Maximum Drawdown} $:  
  Calculate [Maximum Drawdown](#section6.2) from the above section.  

  3. Find the Calmar Ratio:  
  $$\ \text{Calmar Ratio} = \frac{E(R_{excess})}{\text{Maximum Drawdown}} * \text{YEARLY LENGTH} $$  
  $E(R_{excess})$: represents the mean of the excess returns  
  $YEARLY LENGTH$: 272, Total number of trading days per year  

  ### Formula(code)
  `risk_stats['Calmar Ratio'] = excess_rets.mean() / risk_stats['Maximum Drawdown'] * scale`  

  ### Location  
  File: `calculation.py`  
  Function: `cal_risk_stats(self)`
</details>

**Note:** [Volatility](#section4.2) is in the above section.
