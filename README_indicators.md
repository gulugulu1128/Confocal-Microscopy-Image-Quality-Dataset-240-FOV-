# 显微图像客观指标标签


## 数据概况

- 图像数：2640
- FOV组数：240
- 不可读图像数：37

## Z轴先验分

以各FOV的 `Best` 图像作为组内参考，令 `d=|z-z_best|`。本项目历史表格中可恢复的分档为：

- d=0：100分
- d=1：90分
- d=2：82分
- d=3：74分
- d=4：62分
- d>=5：50分

这里的距离是图像序列步数，不是文件名中Z坐标的直接差值，也不是微米距离。表中的 `z_distance` 表示相隔层数，`z_offset` 保留原始Z坐标差；若要换算为微米，必须另行提供真实Z步长。

## 六项客观指标

- Signal：自动前景区域平均灰度。
- SNR：前景平均信号除以背景标准差。
- Sharpness：前景区域拉普拉斯响应方差。
- Contrast：`(前景均值-背景均值)/背景标准差`，实际对应CNR形式。
- Saturation：灰度不低于254的像素比例。
- Background：自动背景区域平均灰度。

前景阈值为 `max(P50+3*背景标准差, P50+5)`。六项指标先在同一FOV的11张图像内转为0-100效用分；Signal、SNR、Sharpness和Contrast越高越好，Saturation和Background越低越好。若组内某指标完全相同，其效用统一设为50，避免人为制造差异。

客观综合分为六项效用分的加权平均，当前权重为：

- `signal`: 1
- `snr`: 1
- `sharpness`: 1
- `contrast`: 1
- `saturation`: 1
- `background`: 1

候选融合分计算为：

`combined_score = 0.70 * z_prior_score + 0.30 * objective_score`

