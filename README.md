# Earnings-Call-EPS-Beat

> 基于财报电话会文本特征预测公司季度 **EPS Beat** 概率的研究型项目。

这个 `README.md` 就是你 GitHub Project 的首页总览文档，包含项目目标、结构、使用方式与当前产物说明。

---

## 项目概览（Overview）
本项目围绕下面的问题展开：
- 是否可以仅基于 earnings call transcript 的文本信息，提前估计下一期 EPS beat 概率？
- 哪类文本特征（可读性、情绪、措辞风格）对预测更有帮助？
- 在 OOS（out-of-sample）场景下，模型是否保持稳定有效？

当前仓库以“研究/实验产物沉淀”为主，已包含数据、特征、标签、模型与评估结果。

## 仓库结构
- `data/`
  - `call_features_wide.csv`：文本特征宽表
  - `labels/eps_labels.csv`：EPS beat 标签
  - `modeling/`：模型文件、参数、OOS 概率、评估指标
  - `beat_probability_results.csv`：最终概率结果汇总
- `notebook/`
  - 分阶段 notebook（抓取 → 清洗 → 特征工程 → 训练评估）
- `quick_health_check.py`
  - 无第三方依赖的一键健康检查脚本
- `PROJECT_STATUS.md`
  - 中文版“项目状态速览”

## 快速开始（Quick Start）
先执行项目健康检查：

```bash
python quick_health_check.py
```

该命令会检查：
- 关键产物文件是否存在；
- 核心 CSV 的行列规模；
- OOS 指标（`logloss_oos`、`brier_oos`）是否在经验阈值内。

## 推荐复现流程
1. 运行 `quick_health_check.py` 确认基础产物完整。
2. 按 `notebook/` 编号顺序复现实验流程。
3. 在 `data/modeling/` 查看模型输出与指标。
4. 如需扩展标的池，补充 `data/transcripts/` 后重新走流程。

## 当前可改进方向
- 增加更严格的时间切分与数据泄漏检测；
- 做概率校准（calibration）与阈值策略优化；
- 增加事件/管理层语义变化类特征；
- 将 notebook 流程逐步脚本化并接入自动化检查（CI）。

## 说明
该仓库目前偏研究型组织方式（notebook + 数据产物）。如果用于生产环境，建议做模块化重构、配置化训练、版本化产物管理。
