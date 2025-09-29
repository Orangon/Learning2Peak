# 国产AI编程模型

在[Claude封禁中国](https://www.anthropic.com/news/updating-restrictions-of-sales-to-unsupported-regions)之后，国产厂商纷纷出手。
Claude Code（以下简称CC）作为一个命令行工具，本身是不受模型限制的，只不过默认是Claude系列模型。其实可以通过配置替换为其他兼容CC的模型。
如今Claude的国产平替模型有：
1. 开源明星：DeepSeek V3.1
2. 宝刀未老：Kimi K2
3. 难他天：GLM-4.5
智谱甚至开放了GLM包月套餐，20元/200元。
K2需要先付费50才能解锁CC所需要的并发次数。

Kimi也做了半价促销活动。
智谱做了更激进的订阅套餐。

## 时间轴

### 2025年9月29日
DeepSeek-V3.2-Exp 模型发布。

这是一个实验性（Experimental）的版本。作为迈向新一代架构的中间步骤，V3.2-Exp 在 V3.1-Terminus 的基础上引入了 DeepSeek Sparse Attention（一种稀疏注意力机制），针对长文本的训练和推理效率进行了探索性的优化和验证。

新模型输出效果几乎不变，但是成本大幅降低，官方 API 价格也相应下调，现在开发者调用 DeepSeek API 的成本将降低 50% 以上。

现在，对于每百万tokens，输入（缓存命中）由0.5元降为0.2元；输出（缓存未命中）由4元降为2元；输出由12元降为3元。

|           | 原价   | 现价   |
| --------- | ---- | ---- |
| 输入（缓存命中）  | 0.5元 | 0.2元 |
| 输出（缓存未命中） | 4元   | 2元   |
| 输出        | 12元  | 3元   |


### 2025年9月22日
DeepSeek-V3.1 现已更新至 DeepSeek-V3.1-Terminus （终极版）

此次更新在保持模型原有能力的基础上，针对用户反馈的问题进行了改进，包括：
- **语言一致性**：缓解了中英文混杂、偶发异常字符等情况；
- **Agent 能力**：进一步优化了 Code Agent 与 Search Agent 的表现。

这下应该缓解了“极”字的幻觉现象。
[相关链接](https://mp.weixin.qq.com/s/DGf1DjjIt_gnm5Ajkp98hA)