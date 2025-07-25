# 信用卡交易反欺诈模型 (Credit Card Fraud Detection)

本项目是一个专注于解决**金融领域核心挑战——极度不平衡数据下欺诈检测**的机器学习项目。利用Kaggle上经典的信用卡交易数据集，本项目完整地实现了从数据预处理、不平衡学习、多模型对比到专业评估的全流程。

**项目亮点:**
*   **技术栈**: `Python`, `Pandas`, `Scikit-learn`, `Imbalanced-learn (SMOTE)`, `Matplotlib`
*   **核心挑战**: 数据集极度不平衡，欺诈样本仅占总体的 **0.172%**。
*   **关键成果**: 通过SMOTE与逻辑回归的结合，模型实现了 **88% 的欺诈召回率(Recall)** 和 **0.743 的AUPRC**，展现了强大的风险识别能力。

---

## 1. 项目流程与核心方法

### 1.1 数据预处理与EDA
*   对原始数据中的`Time`和`Amount`特征进行**标准化(Standardization)**，以消除量纲差异，为模型训练做好准备。
*   通过KDE可视化分析，初步探索了欺诈交易与正常交易在交易金额与时间分布上的模式差异。

### 1.2 不平衡学习 (Imbalanced Learning)
*   **核心策略**: 识别到直接使用不平衡数据训练会导致模型失效（倾向于预测多数类）。因此，采用业界主流的**SMOTE (Synthetic Minority Over-sampling Technique)** 算法对**训练集**进行过采样。
*   **效果**: SMOTE通过合成新的少数类（欺诈）样本，成功将训练集构建为正负样本比例1:1的平衡数据集，为模型学习欺诈特征提供了充分的信息。

### 1.3 多模型对比与评估
*   **基线模型 (有监督)**: 在SMOTE处理后的平衡数据上，训练了一个**逻辑回归(Logistic Regression)**模型。
*   **对比模型 (无监督)**: 为探索不同方法论，直接在原始不平衡数据上训练了一个**孤立森林(Isolation Forest)**异常检测模型。
*   **评估指标**: 摒弃在不平衡场景下具有误导性的Accuracy，采用 **Precision-Recall Curve (PR曲线)** 和 **AUPRC (PR曲线下面积)** 作为核心评估指标。

## 2. 结论与洞察

<img width="954" height="669" alt="Image" src="https://github.com/user-attachments/assets/43ac6e51-30e6-488b-800a-08b95dba3713" />


*   **性能对比**: 实验结果清晰地表明，**SMOTE + 逻辑回归 (AUPRC=0.743)** 的性能**显著优于**孤立森林 (AUPRC=0.199)。
*   **核心洞察**: 本项目有力地证明，在信用卡反欺诈这类场景中，通过**采样技术有效解决数据不平衡问题，并应用有监督的分类模型**，是比无监督异常检测更可靠、更高效的技术路径。
*   **业务价值**: 最终模型实现了**88%的高召回率**，这意味着它能成功识别绝大多数的欺诈行为，可作为高效的**一线欺诈预警系统**，极大地降低银行的资金损失和声誉风险。

## 3. 如何运行
1.  克隆本仓库。
2.  确保已安装`Python 3.x`及`pip`。
3.  在项目根目录下运行 `pip install -r requirements.txt` (你需要创建一个包含`pandas`, `scikit-learn`, `matplotlib`, `seaborn`, `imblearn`的`requirements.txt`文件)。
4.  使用Jupyter Notebook打开 `.ipynb` 文件并运行所有单元格。

## 数据来源 (Data Source)

本项目使用的数据集来自Kaggle竞赛 "Credit Card Fraud Detection"。由于文件大小限制，数据集未包含在本仓库中。您可以从以下链接下载原始数据：

[https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud/data](https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud/data)
