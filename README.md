 (cd "$(git rev-parse --show-toplevel)" && git apply --3way <<'EOF' 
diff --git a/README.md b/README.md
new file mode 100644
index 0000000000000000000000000000000000000000..03cf7550674c8a86a9b7503e2e15c824fa11a67c
--- /dev/null
+++ b/README.md
@@ -0,0 +1,54 @@
+# Earnings-Call-EPS-Beat
+
+一个基于财报电话会（earnings call transcript）文本特征的 **EPS Beat 概率预测项目**。
+
+## 项目目标（Overview）
+本项目核心目标是：
+- 从财报电话会文本中提取可量化特征（可读性、情绪、文档属性等）；
+- 与季度标签（EPS beat / miss）对齐；
+- 训练并评估预测模型，输出每个公司季度的 beat 概率；
+- 提供可复用的数据产物与 notebook 流程，支持后续迭代与验证。
+
+## 你现在能直接用什么
+当前仓库已经包含了：
+- 处理后的特征宽表与标签文件；
+- 模型训练与 OOS 预测结果；
+- 关键模型文件（imputer/scaler/model）；
+- notebook 分阶段流程（数据获取 → 特征工程 → 建模评估）。
+
+## 目录结构（简版）
+- `data/`
+  - `call_features_wide.csv`：文本特征宽表
+  - `labels/eps_labels.csv`：EPS 标签
+  - `modeling/`：模型、参数、OOS 概率与评估指标
+  - `beat_probability_results.csv`：最终概率结果汇总
+- `notebook/`
+  - 分步骤 notebook（抓取、处理、特征、建模、评估）
+- `quick_health_check.py`
+  - 无第三方依赖的一键健康检查
+- `PROJECT_STATUS.md`
+  - 项目状态快速说明（中文）
+
+## 推荐使用流程
+1. 先跑快速健康检查：
+   ```bash
+   python quick_health_check.py
+   ```
+2. 根据 `notebook/` 中的流程按阶段复现（建议按编号顺序）。
+3. 在 `data/modeling/` 查看模型表现与 OOS 输出。
+4. 基于你关注的股票池扩展 `data/transcripts/` 后重复流程。
+
+## 当前默认健康检查覆盖项
+`quick_health_check.py` 会检查：
+- 关键产物文件是否存在；
+- 核心 CSV 行列规模是否可读；
+- OOS 指标（logloss / brier）是否在经验阈值内。
+
+## 适合继续改进的方向
+- 增加更严格的时间切分与泄漏检查；
+- 做概率校准（calibration）与阈值策略；
+- 引入更多事件特征（指引变动、管理层措辞变化等）；
+- 增加自动化 pipeline（脚本化训练 + 版本化产物）。
+
+## 说明
+该仓库目前更偏研究与实验产物沉淀（notebook + 数据文件），如果你要用于生产环境，建议进一步脚本化、模块化并补齐 CI 检查。
 
EOF
)
