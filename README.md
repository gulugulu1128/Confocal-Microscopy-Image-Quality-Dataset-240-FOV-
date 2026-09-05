# dataset 240-FOV 显微图像数据集

## 数据集概述
- **数据集名称**: dataset_240FOV
- **视野数量**: 240个 (FOV)
- **图像总数**: 2640张

## 目录结构
```
dataset_240FOV/
├── all.csv                   # 全量数据标签（2640条）
├── train.csv                 # 训练集标签
├── val.csv                   # 验证集标签
├── test.csv                  # 测试集标签
├── train/images/             # 训练集图像（176个视野组）
├── val/images/               # 验证集图像
└── test/images/              # 测试集图像
```

## 标签字段说明
- `image_id`: 图像唯一标识符
- `image_path`: 图像完整路径
- `relative_image_path`: 相对路径
- `group_new_id`: 视野组ID (FOV-level grouping)
- `group_id`: 原始视野组ID
- `source_partner`: 数据来源合作者 (Partner A/B/C)
- `dataset`: 数据集名称
- `folder`, `x`, `y`: 空间坐标信息
- `image_no`: 焦面编号
- `z`: Z-stack深度位置
- `is_expert_best`: 是否为专家最佳焦面
- `reference_score`: 参考焦面评分
- `reference_level`: 参考焦面等级 (差/中/良/优)
- `quality_score`: 综合质量评分
- `quality_level`: 综合质量等级
- `label_source`: 标签来源
- `source_note`: 来源备注

## 数据划分
- **训练集**: 约70%数据
- **验证集**: 约15%数据
- **测试集**: 约15%数据
- 按视野组(FOV)划分，确保不同视野组不会同时出现在训练集和测试集中

## 数据来源
原始数据来源：`expert_best_standard/` 目录下的 partner_A/B/C 三个子目录

## 使用建议
1. 训练模型时，通过 `train.csv` 读取图像和标签
2. 图像路径在 CSV 中为绝对路径，也可直接通过相对路径定位
3. 如需批量处理，可使用 `group_new_id` 按视野组进行汇总统计
