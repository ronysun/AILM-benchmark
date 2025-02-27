# AILM-benchmark

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)

一个开源的综合性大语言模型（LLM）基准测试工具包，提供标准化的评估脚本、可视化工具和文档指南。

## 📌 核心功能

- **多框架支持**
  - 兼容 Hugging Face Transformers / OpenAI API / Anthropic 等主流接口
  - 支持单机多卡分布式推理
  
- **标准化测试集**
  - 内置 20+ 常见NLP基准任务（包括GLUE、SuperGLUE、HELM等）
  - 支持自定义数据集导入
  
- **多维评估指标**
  - 准确性：精确率/召回率/F1
  - 效率：Tokens per second/内存占用
  - 成本估算：API调用成本模拟器
  
- **可视化报告**
  - 自动生成交互式评估仪表盘
  - 多模型对比雷达图
  - 资源消耗热力图

## 🚀 快速开始

### 安装依赖

```bash
git clone https://github.com/ronysun/AILM-benckmark.git
cd AILM-benchmark
pip install -r requirements.txt
```

### 基础使用示例

```python
from benchmark import LLMEvaluator

# 初始化评估器
evaluator = LLMEvaluator(
    model_name="gpt-3.5-turbo",
    device="cuda:0",  # 或 "cpu"
    precision="fp16"
)

# 运行标准测试套件
results = evaluator.run_standard_suite(
    tasks=["text_classification", "summarization"],
    batch_size=32,
    max_length=512
)

# 生成可视化报告
evaluator.generate_report(
    output_format="html",
    compare_with=["llama-2-7b", "mistral-7b"]
)
```

## 📊 预置测试任务

| 任务类别       | 包含数据集                     | 评估指标                     |
|----------------|--------------------------------|------------------------------|
| 文本分类       | IMDB, AG News                  | Accuracy, F1                 |
| 问答系统       | SQuAD v2, HotpotQA             | EM, F1                       |
| 文本生成       | CNN/DailyMail                  | ROUGE, BLEU                  |
| 推理任务       | GSM8K, MATH                    | Accuracy                     |
| 代码生成       | HumanEval, MBPP                | Pass@k                       |

## 🔧 高级功能

### 自定义测试模板

```yaml
# custom_benchmark.yaml
task_config:
  name: "legal_ner"
  description: "法律文本命名实体识别"
  dataset:
    path: "./data/legal_ner.jsonl"
    format: "jsonlines"
  metrics:
    - name: "f1"
      args:
        average: "macro"
  constraints:
    max_input_length: 2048
    min_samples: 1000
```

### 分布式基准测试
```bash
python run_distributed.py \
  --model meta-llama/Llama-2-13b-hf \
  --tasks all \
  --gpus 4 \
  --batch_sizes 16 32 64 \
  --output_dir ./results
```

## 📈 结果可视化示例
![Benchmark Dashboard](docs/images/dashboard_preview.png)

## 🤝 贡献指南

欢迎通过以下方式参与贡献：
1. 提交新的测试数据集
2. 添加对新模型架构的支持
3. 改进评估指标计算方法
4. 优化性能监控模块

请先阅读[贡献指南](CONTRIBUTING.md)并签署贡献者协议。

## 📜 许可证

本项目采用 [MIT License](LICENSE)

## 📬 联系方式

如有问题或建议，请通过以下方式联系：
- GitHub Issues
- Email: ronysun@qq.com

---
