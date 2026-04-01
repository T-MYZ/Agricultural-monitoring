# 植株健康评分人工校验说明

## 1）本轮目标
本轮只做人工校验与修正：
- 校验并修改 `classification`
- 校验并修改 `grade`

本轮不修改检测框、不改图片文件名。

## 2）校验会用到的文件
- 主要编辑表格：`plant_health_scores.csv`
- 裁剪图目录：`crops`

## 3）允许填写的取值
### classification（标签必须保持英文）
只能使用以下英文标签：
- `target_plant`（目标植株）
- `partial_leaf_or_incomplete`（叶片局部/植株不完整）
- `weed_or_nontarget`（杂草或非目标）
- `invalid_background`（无效背景）

### grade
只能使用以下值：
- `A`
- `B`
- `C`
- `D`
- `Q0`

### grade 含义
- `A`：优秀/健康。叶色正常且均匀，叶片完整，长势好，基本无明显胁迫症状。
- `B`：良好/轻微问题。整体健康，可能有轻微黄化、轻度破损或轻微长势下降。
- `C`：一般/中度问题。存在较明显异常（黄化、破损、萎蔫、长势弱等），建议重点关注。
- `D`：较差/重度问题。症状明显，建议优先干预处理。
- `Q0`：不参与健康分档。用于无效样本（如 `invalid_background`、`weed_or_nontarget`，或严重模糊/遮挡导致不可判定）。

## 4）各列修改规则
在 `plant_health_scores.csv` 中：
- 必改列（如发现问题）：`classification`、`grade`
- 绝对不要改：`image_name`

如需补充说明，可新增：
- `review_note`（可选，写简短备注）

## 5）快速判定建议
- 图中大部分是土壤/地膜/背景，或严重模糊无法判断：`invalid_background` + `Q0`
- 只截到一部分叶片、植株明显不完整：`partial_leaf_or_incomplete` + `Q0`
- 明显细长杂草或非瓜苗目标：`weed_or_nontarget` + `Q0`
- 明确是目标瓜苗植株：`target_plant`，再按健康状态给 `A/B/C/D`

## 6）团队协作流程
1. 按 `image_name` 前缀分段分工（例如 `1_*~7_*`、`8_*~14_*`）。
2. 每位成员在群里面的共享excel表中修改自己负责的行。
