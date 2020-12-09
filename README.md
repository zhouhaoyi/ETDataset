# Electricity Transformer Dataset (ETDataset)

In this Github repo, we provide several datasets could be used for the long sequence time-series problem. All datasets have been preprocessed and they were stored as .csv files.  The dataset ranges from 2016/07 to 2018/07, and we will update to 2019 soon).

*Dataset list*

- [x] **ETT-small**: The data of 2 Electricity Transformers at 2 stations, including load, oil temperature.
- [ ] **ETT-large**: The data of 39 Electricity Transformers at 39 stations, including load, oil temperature.
- [ ] **ETT-Full**: The data of 69 Transformer station at 39 stations, including load, oil temperature, location, climate, demand.

If you use this dataset please cite:

```
@inproceedings{haoyi-etal-2021,
  author    = {Haoyi Zhou and
               Shanghang Zhang and
               Jieqi Peng and
               Shuai Zhang and
               Jianxin Li and
               Hui Xiong and
               Wancai Zhang},
  title     = {Informer: Beyond Efficient Transformer for Long Sequence Time-Series Forecasting},
  booktitle = {The Thirty-Fifth {AAAI} Conference on Artificial Intelligence, {AAAI}
               2021},
  pages     = {online},
  publisher = {{AAAI} Press},
  year      = {2021},
}
```

## Why *Oil Temperature* is involved in this dataset?

The electric power distribution problem is the distribution of electricity to different areas depends on its sequential usage. But predicting the following demand of a specific area is difficult, as it varies with weekdays, holidays, seasons, weather, temperatures, etc. However, no existing method can perform a long-term prediction based on super long-term real-world data with high precision. Any false prophecy may damage the electrical transformer. So currently, without an efficient method to predict future electric usage, managers have to make decisions based on the empirical number, which is much higher than the real-world demands. It causes unnecessary waste of electric and equipment depreciation. One of the most efficient strategies is to predict how the electrical transformers' oil temperature is safe and avoid unnecessary waste. 
As a result, to address this problem, our team and Beijing Guowang Fuda Science & Technology Development Company built a real-world platform and collected 2-year data. We work on it to predict the electrical transformers' oil temperature and investigate the extreme load capacity.

## ETT-small:

We donated two years of data, in which each data point recorded every 15 minutes, from two regions of a province of China, named ETT-small$_1$ and ETT-small$_2$, respectively. Each dataset contains 2 year * 365 days * 24 hours * 4 times = 70,080 data point. Each data point consists of 7 features, including the predictive value "oil temperature", and 6 different types of external power load features.

<img src="https://raw.githubusercontent.com/zhouhaoyi/ETDataset/main/img/appendix_auto_correlation.png" height = "200" alt="" align=center />
<center>*Figure 1. The overall view of the "oil temperature" variable in the dataset.*</center>

<img src="https://raw.githubusercontent.com/zhouhaoyi/ETDataset/main/img/appendix_dataset_year.png" height = "200" alt="" align=center />
<center>*Figure 2. The autocorrelation graph of the dataset.*</center>

Specifically, the dataset combines short-term periodical patterns, long-term periodical patterns, long-term trends, and many irregular patterns. We firstly give an overall view in Figure 1 and it shows evident seasonal trends. To better examine the existence of long-term and short-term repetitive patterns, we plot the autorcorrelation graph for all the variables of the ETT-small$_1$ dataset in Figure 2. The blue line in the above is the target 'oil temperature', and it maintains some short-term local continuity. However, the other variables (power load) shows short-term daily pattern (in every 24 hours) and long-term week pattern(in every 7 days).
