# 三种区域 CutMix 还原预测可视化

右键运行 `RUN_CUTMIX_THREE_REGION_VISUALIZE.py`。不训练，自动选择已完成的 5% RCFM
完整方法中验证 Dice 最高的 EMA 教师权重。正在训练且没有 final_metrics.json 的诊断实验不会被选择。

每个测试病例使用原有固定切片规则：真值前景切片序列中的 Q25、Q50、Q75。程序用测试
真值选择不同患者中三张切片前景重叠最大的配对，因此仅属于 oracle 定性诊断。

每个切片文件夹输出四张主要图片：

- `00_original_prediction.png`：未混合切片的原始预测；
- `01_whole_foreground_restored_prediction.png`：掩码包含双方全部前景；
- `02_local_region_restored_prediction.png`：原有约 40 像素外接范围的局部不规则区域；
- `03_foreground_internal_restored_prediction.png`：双方共同前景内部的小型不规则区域，直径在窄范围变化。

还原不使用真值补预测。对于病例 A，区域外取“以 A 为主体”的混合输入预测，交换区域取
另一张混合输入中属于 A 内容的预测；病例 B 同理。输出保持 256x256 网络空间，不叠加 MRI、
不加文字白边。颜色为背景黑、RV 红、Myo 绿、LV 蓝。审计用黑白掩码位于每个切片的
`masks` 子目录；病例名、配对病例和切片号记录在文件夹及 `manifest.json`。

结果保存到新的时间戳目录：
`visualizations/ACDC_5percent_three_region_cutmix_restored_时间/`
旧结果不会覆盖。
