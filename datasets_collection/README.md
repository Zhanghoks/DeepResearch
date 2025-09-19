# DeepResearch 数据集集合说明文档

## 概述

本目录包含了 DeepResearch 项目中所有子项目的数据集文件，按子项目分类整理。这些数据集主要用于训练、评估和测试各种 Web Agent 模型的能力。

## 目录结构

```
datasets_collection/
├── WebWatcher/          # 网页视觉理解基准数据
├── WebDancer/           # 多步交互轨迹数据
├── WebShaper/           # 网页结构化数据
├── WebSailor/           # 网页研究问答数据
├── inference/           # 推理评测样例数据
└── README.md           # 本说明文档
```

## 数据集详细说明

### 1. WebWatcher - 网页视觉理解基准

**位置**: `WebWatcher/`

**文件列表**:
- `bc_vl_level1.jsonl` (199条记录)
- `bc_vl_level2.jsonl` (200条记录)

**用途**: 评估模型在网页截图上的视觉理解和问答能力

**数据格式**:
```json
{
  "question": "问题文本",
  "image_path": "image/level1/level1_1.jpg",
  "answers": ["答案1", "答案2"],
  "domain": "领域标签"
}
```

**字段说明**:
- `question`: 基于网页截图的问答问题
- `image_path`: 图片文件的相对路径
- `answers`: 可接受的答案列表（支持多个正确答案）
- `domain`: 问题所属领域（如 Engineering, Art, Music, Politics 等）

**来源**: WebWatcher 项目的视觉基准测试数据，用于评估多模态网页理解能力

**特点**:
- 涵盖多个领域的问题
- 包含复杂的视觉推理任务
- 支持多答案评估

### 2. WebDancer - 多步交互轨迹数据

**位置**: `WebDancer/`

**文件列表**:
- `sample_qa.jsonl` (200条记录) - 问答样例
- `sample_traj.jsonl` (200条记录) - 交互轨迹数据

**用途**: 训练和评估多步推理、工具调用和网页交互能力

**数据格式**:

**sample_qa.jsonl**:
```json
{
  "question": "问题文本",
  "answer": "标准答案",
  "tag": "题型标签"
}
```

**sample_traj.jsonl**:
```json
{
  "type": "chatml",
  "task": "agent/multiturn_search",
  "messages": [
    {
      "role": "system",
      "content": "系统提示"
    },
    {
      "role": "user", 
      "content": "用户问题"
    },
    {
      "role": "assistant",
      "content": "助手回复（包含工具调用）"
    }
  ],
  "functions": [...],
  "tool_calls": [...],
  "answer": [...],
  "tag": "e2hqa"
}
```

**字段说明**:
- `type`: 数据格式类型
- `task`: 任务类型
- `messages`: 对话历史，包含系统提示、用户问题和助手回复
- `functions`: 可用工具定义
- `tool_calls`: 工具调用记录
- `answer`: 最终答案
- `tag`: 数据标签（e2hqa, crawlqa 等）

**来源**: WebDancer 项目的多步推理和工具调用训练数据

**特点**:
- 包含完整的对话轨迹
- 支持工具调用和搜索
- 涵盖多种问答类型

### 3. WebShaper - 网页结构化数据

**位置**: `WebShaper/`

**文件列表**:
- `webshaper.500.jsonl` (500条记录)

**用途**: 网页信息抽取和结构化任务

**数据格式**:
```json
{
  "id": "唯一标识符",
  "question": "复杂问题文本",
  "answer": "答案",
  "formalization": [
    ["变量1", "关系", "变量2"],
    ["变量2", "属性", "值"]
  ],
  "urls": ["相关URL列表"]
}
```

**字段说明**:
- `id`: 数据项唯一标识符
- `question`: 复杂的结构化问题
- `answer`: 标准答案
- `formalization`: 问题的形式化表示，用于结构化理解
- `urls`: 相关的网页URL列表

**来源**: WebShaper 项目的网页信息结构化处理数据

**特点**:
- 包含复杂的关系推理
- 支持结构化信息抽取
- 提供形式化表示

### 4. WebSailor - 网页研究问答数据

**位置**: `WebSailor/`

**文件列表**:
- `sailorfog-QA.jsonl` (19条记录) - 主要数据集
- `example.jsonl` (1条记录) - 示例数据

**用途**: 网页研究和信息检索能力评估

**数据格式**:
```json
{
  "question": "复杂的研究问题",
  "answer": "详细答案"
}
```

**字段说明**:
- `question`: 需要深度网页研究才能回答的复杂问题
- `answer`: 基于网页搜索和验证的详细答案

**来源**: WebSailor 项目的网页研究能力测试数据

**特点**:
- 问题复杂度高，需要多步推理
- 答案详细且准确
- 涵盖多个知识领域

### 5. Inference - 推理评测样例

**位置**: `inference/`

**文件列表**:
- `example.jsonl` (1条记录) - 基础推理样例
- `example_with_file.jsonl` (1条记录) - 文件处理样例

**用途**: 快速测试和验证推理能力

**数据格式**:

**example.jsonl**:
```json
{
  "question": "基础问题",
  "answer": ""
}
```

**example_with_file.jsonl**:
```json
{
  "question": "(Uploaded 1 file: ['hello.txt'])\n\n带文件的问题",
  "answer": ""
}
```

**字段说明**:
- `question`: 测试问题，可能包含文件上传信息
- `answer`: 标准答案（可能为空，用于生成任务）

**来源**: 推理模块的测试和验证数据

**特点**:
- 数据量小，用于快速测试
- 支持文件处理能力测试
- 适合回归测试

## 数据统计总览

| 子项目 | 文件数 | 总记录数 | 主要用途 |
|--------|--------|----------|----------|
| WebWatcher | 2 | 399 | 视觉理解基准 |
| WebDancer | 2 | 400 | 多步交互训练 |
| WebShaper | 1 | 500 | 结构化信息抽取 |
| WebSailor | 2 | 20 | 网页研究问答 |
| Inference | 2 | 2 | 推理能力测试 |
| **总计** | **9** | **1,321** | **多模态Web Agent** |

## 使用建议

### 1. 数据加载
所有数据文件均为 JSONL 格式，每行一个 JSON 对象。可以使用以下方式加载：

```python
import json

def load_jsonl(file_path):
    data = []
    with open(file_path, 'r', encoding='utf-8') as f:
        for line in f:
            data.append(json.loads(line.strip()))
    return data
```

### 2. 评估指标
- **WebWatcher**: 视觉问答准确率、多答案匹配
- **WebDancer**: 工具调用成功率、多步推理准确率
- **WebShaper**: 结构化信息抽取准确率、关系识别准确率
- **WebSailor**: 复杂问答准确率、信息检索质量
- **Inference**: 基础推理能力、文件处理能力

### 3. 注意事项
- 视觉数据需要确保图片文件路径正确
- 轨迹数据包含完整的对话历史，适合序列到序列训练
- 结构化数据包含形式化表示，可用于关系抽取任务
- 所有数据均支持中文和英文混合使用

## 更新日志

- **2025-01-XX**: 初始版本，整理所有子项目数据
- 数据来源：DeepResearch 项目各子模块
- 维护者：DeepResearch 团队

## 联系方式

如有问题或建议，请联系 DeepResearch 项目团队。
