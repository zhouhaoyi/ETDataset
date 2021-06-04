# 电力变压器数据集 (ETDataset)

在这个仓库中，我们提供了涉及电力变压器的多个数据集，用于支撑”长时间序列”相关的研究。所有的数据都经过了预处理，并且以`.csv`的格式存储。这些数据的时间跨度为2016年7月到2018年7月。

*数据列表*

- [x] **ETT-small**：含有2个电力变压器（来自2个站点）的数据，包括负载、油温。
- [ ] **ETT-large**：含有39个电力变压器（来自39个站点）的数据，包括负载、油温。
- [ ] **ETT-full**：含有69个电力变压器（来自39个站点）的数据，包括负载、油温、位置、气候、需求。

如果您使用该数据集，请引用该工作 `Informer@AAAI2021`[\[paper\]](https://arxiv.org/abs/2012.07436)[\[code\]](https://github.com/zhouhaoyi/Informer2020)[\[video\]](https://slideslive.com/38948878):

```
@inproceedings{haoyietal-informer-2021,
  author    = {Haoyi Zhou and
               Shanghang Zhang and
               Jieqi Peng and
               Shuai Zhang and
               Jianxin Li and
               Hui Xiong and
               Wancai Zhang},
  title     = {Informer: Beyond Efficient Transformer for Long Sequence Time-Series Forecasting},
  booktitle = {The Thirty-Fifth {AAAI} Conference on Artificial Intelligence, {AAAI} 2021, Virtual Conference},
  volume    = {35},
  number    = {12},
  pages     = {11106--11115},
  year      = {2021},
}
```

## 为什么引入 *油温数据* 到该数据集中？

电力分配问是电网根据顺序变化的需求管理电力分配到不同用户区域。但要预测特定用户区域的未来需求是困难的，因为它随工作日、假日、季节、天气、温度等的不同因素变化而变化。现有预测方法不能适用于长期真实世界数据的高精度长期预测，并且任何错误的预测都可能产生严重的后果。因此当前没有一种有效的方法来预测未来的用电量，管理人员就不得不根据经验值做出决策，而经验值的阈值通常远高于实际需求。保守的策略导致不必要的电力和设备折旧浪费。值得注意的是，变压器的油温可以有效反映电力变压器的工况。我们提出最有效的策略之一，是预测变压器的油温同时设法避免不必要的浪费。
为了解决这个问题，我们的团队与北京国网富达科技发展公司建立了一个平台并收集了2年的数据。我们用它来预测电力变压器的油温并研究电力变压器极限负载能力。

## ETT-small:

我们提供了两年的数据，每个数据点每分钟记录一次（用 *m* 标记），它们分别来自中国同一个省的两个不同地区，分别名为ETT-small-m1和ETT-small-m2。每个数据集包含2年 * 365天 * 24小时 * 4 = 70,080数据点。 此外，我们还提供一个小时级别粒度的数据集变体使用（用 *h* 标记），即ETT-small-h1和ETT-small-h2。 每个数据点均包含8维特征，包括数据点的记录日期、预测值“油温”以及6个不同类型的外部负载值。

<p align="center">
<img src="./img/appendix_dataset_year.png" height = "200" alt="" align=center />
<img src="./img/appendix_auto_correlation.png" height = "200" alt="" align=center />
<br><br>
<b>图 1.</b>"油温"特征在ETT-small数据集中的总览&nbsp;&nbsp;&nbsp;&nbsp;<b>图 2.</b>全部变量的自回归图形展示
</p>


具体来说，数据集中包含短周期模式，长周期模式，长期趋势和大量不规则模式。我们在图1给出了数据的总览，图中数据显示出了明显的季节趋势。为了更好地表示数据中长期和短期重复模式的存在，我们在图2中绘制了ETT-small-h1数据集中所有变量的自相关图，其中最上面的蓝色曲线是目标变量“油温”，它保持了一些短期的局部连续性，而其他的变量（各类负载）则显示出了短期的日模式（每24小时）和长期的周模式（每7天）。

数据集是使用`.csv`形式进行存储的，在图3中我们给出了一个数据的样例。其中第一行（8列）是数据头，包括了 "HUFL", "HULL", "MUFL", "MULL", "LUFL", "LULL" 和 "OT"，每一列的详细意义展示在表1中。

<p align="center">
<img src="./img/ETT%20data%20demo.png" height = "168" alt="" align=center />
<br><br>
<b>图 3.</b> ETT 数据样例.
</p>


|    Field    |         date          |              HUFL              |               HULL                |                MUFL                |                MULL                 |              LUFL               |               LULL               |                OT                |
| :---------: | :-------------------: | :----------------------------: | :-------------------------------: | :--------------------------------: | :---------------------------------: | :-----------------------------: | :------------------------------: | :------------------------------: |
| Description | The recorded **date** | **H**igh **U**se**F**ul **L**oad | **H**igh **U**se**L**ess **L**oad | **M**iddle **U**se**F**ul **L**oad | **M**iddle **U**se**L**ess **L**oad | **L**ow **U**se**F**ul **L**oad | **L**ow **U**se**L**ess **L**oad | **O**il **T**emperature (target) |

<p align="center"><b>表 1.</b> 数据中各列的含义.</p>
