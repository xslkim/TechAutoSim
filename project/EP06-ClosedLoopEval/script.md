>>> 开场 #B01
@enter: fade-up
@exit: fade
@visual: image

--- visual ---
一张 16:9 横构图的扁平化教程封面图。深色背景 #0d1117。

主体居中布局：
- 顶部标签 "CARLA × SparseDriveV2 仿真教程"，灰色 #8b949e 小字。
- 主标题 "EP06: 闭环评测实战"，白色 #e6edf3 粗体大字号。
- 主标题下方亮蓝色 #58a6ff 短横线。
- 副标题 "从训练好的模型到 CARLA 考场，完整闭环 Pipeline"，灰色 #8b949e 中等字号。

画面中央偏下是一行知识回顾标签条（横向排列，5 个胶囊形圆角小卡片，每个深色 #161b22 背景、圆角 8 px、内边距大），用细右指箭头连接：
"CARLA 环境 ✓" → "传感器 ✓" → "tick 循环 ✓" → "SparseDriveV2 ✓" → "闭环评测"

前 4 个标签左侧带绿色 #3fb950 ✓ 图标；最后一个 "闭环评测" 标签用亮蓝色 #58a6ff 边框 + 实心填充，文字白色粗体，旁边一行小字 "← 本集"，亮蓝色。

整体风格极简、留白克制、对齐严格。

--- narration ---
欢迎来到全系列最后一集
五集下来
我们建好了 CARLA 环境
装好了传感器
跑通了 tick 循环
深入理解了 SparseDriveV2 的每个模块
现在是最终考验
把训练好的模型放到 CARLA 考场里
跑 Bench2Drive 闭环评测
看它到底能不能安全开车


>>> 开环 vs 闭环 #B02
@enter: fade
@exit: fade
@visual: image

--- visual ---
一张 16:9 横构图的左右对比图，扁平化技术风格。深色背景 #0d1117。

顶部居中标题 "开环 vs 闭环评测"，白色 #e6edf3 粗体大字。

画面分左右两栏，总宽占画布 88%，间距充足。

左栏 "Open-Loop"（橙色 #f0883e 标题、2 px 同色边框、圆角 16 px、深色背景 #161b22、内边距大）：
- 顶部示意图：两条并列轨迹线——一条 GT 真实轨迹（实线）和一条模型预测轨迹（虚线），中间标注 "L2 Error"。
- 下方要点（中等字号 #e6edf3）：
  - 回放录制数据
  - Agent 决策不影响环境
  - 只看轨迹偏差
- 底部一行小字 "代表基准：nuScenes / NAVSIM"，灰色 #8b949e。

右栏 "Closed-Loop"（绿色 #3fb950 标题与边框）：
- 顶部示意图：一个圆形循环箭头流程图（缩小版），节点 "感知 → 规划 → 控制 → 环境响应 → 感知"。
- 下方要点：
  - Agent 操作改变环境
  - 碰撞真实发生
  - 评估安全 + 任务完成
- 底部小字 "代表基准：CARLA Leaderboard / Bench2Drive"。

画面底部居中一行亮蓝色 #58a6ff 中等字号粗体：
"SparseDriveV2 两种评测都做，但闭环才是真考试"

整体风格强对比、对称、文字清晰。

--- narration ---
先区分两种评测
开环是回放数据
模型做预测但结果不影响环境
看的是 L2 轨迹偏差
闭环则完全不同
Agent 做的每个决策都在仿真里真实执行
碰撞、违规都会真实发生
SparseDriveV2 是少数两种评测都做的方案


>>> Bench2Drive：考试协议 #B03
@enter: fade-up
@exit: fade
@visual: image

--- visual ---
一张 16:9 横构图的五阶段流程图，扁平化技术风格。深色背景 #0d1117。

顶部居中标题 "Bench2Drive — 基于 CARLA 的闭环考试"，白色 #e6edf3 粗体大字。

画面中央从左到右是五个阶段卡片，总宽占画布 88%，每张卡片圆角 12 px、深色背景 #161b22、2 px 不同色边框、内边距大，用右指细箭头连接：

1. "Checkpoint 加载"，亮蓝色 #58a6ff 边框；卡片内一个文件 + 下载箭头图标，下方 "SparseDriveV2 权重"。
2. "连接 CARLA"，绿色 #3fb950 边框；图标 Server + Client，下方 "同步模式启动"。
3. "加载 Route"，橙色 #f0883e 边框；图标地图 + 路径线，下方 "220 条测试路线"，小字 "44 种交互场景"。
4. "Agent 驾驶"，紫色 #a371f7 边框；图标 Ego 车 + 轨迹，下方 "tick 循环中推理"，小字 "每 50 ms 一次决策"。
5. "评分出分"，金色 #d29922 边框；图标计分板，下方 "DS / SR / Multi-Ability"。

整体风格干净、对齐严格、每个卡片标签清晰可读。

--- narration ---
Bench2Drive 是建立在 CARLA 上的标准化闭环考试
流程分五步
加载训练好的 SparseDriveV2 checkpoint
连接 CARLA Server 并开启同步模式
加载测试路线
共 220 条，覆盖 44 种交互场景
Agent 自动驾驶
每 50 ms 完成一次推理和控制
最后汇总所有路线的结果
得出三个核心分数


>>> 闭环评测流水线 #B04
@enter: fade
@exit: fade
@visual: image

--- visual ---
一张 16:9 横构图的水平流水线图，扁平化技术风格。深色背景 #0d1117。

顶部居中标题 "闭环评测流水线"，白色 #e6edf3 粗体大字；副标题 "每帧都在这条流水线上运转"，亮蓝色 #58a6ff。

画面中央是一条从左到右的横向流水线，总宽占画布 92%，六个阶段矩形（圆角 12 px、深色背景 #161b22、2 px 不同色边框）用右指箭头连接：

1. "world.tick()"，亮蓝色 #58a6ff 边框；下方小字 "仿真推进一帧"。
2. "6 Camera Capture"，绿色 #3fb950 边框；下方 "6 相机同步采集"。
3. "SparseDriveV2 Forward"，紫色 #a371f7 边框；下方 "感知 + 建图 + 规划 → 轨迹"。
4. "apply_control()"，金色 #d29922 边框；下方 "油门 / 转向 / 刹车"。
5. "Infraction Check"，橙色 #f0883e 边框；卡片内部三个小检测器图标（一行排列）：
   - Collision?（红色圆点）
   - Red Light?（红色圆点）
   - Lane Invasion?（金色圆点）
6. "Log Accumulation"，灰色 #30363d 边框；下方 "每路线独立记录"。

画面底部居中一行小字（灰色 #8b949e 中等字号）：
"220 条路线汇总 → Driving Score"

整体风格干净、流水线对齐严格、文字按字面准确渲染。

--- narration ---
来看闭环评测的完整流水线
每帧从 world.tick 开始
6 个相机同步采集
SparseDriveV2 做一次完整推理
输出规划轨迹
apply_control 发送油门、转向和刹车
同时每帧都在检查违规
碰撞、闯红灯、压线、偏离路线
每次违规都被记录
220 条路线全部跑完后
汇总出 Driving Score


>>> 成功案例：Cut-In 安全通过 #B05
@enter: fade-up
@exit: fade
@visual: video(./assets/pass_cutin_topdown.mp4)

--- visual ---
（本块使用本地视频 ./assets/pass_cutin_topdown.mp4，无需生成图片）

SparseDriveV2 在 Cut-In 场景中的成功驾驶，鸟瞰视角。
蓝色 Ego 车在右车道行驶，红色 NPC 从左侧追上后切入。
SparseDriveV2 检测到切入车辆，选出减速轨迹，Ego 平稳减速让行。
本次运行无碰撞、无压线、无闯红灯——Driving Score 全保留。

--- narration ---
EP05 我们已经看过模型怎么应付 cut-in
现在站在考官视角再看一遍
注意蓝色 Ego 车的反应
SparseDriveV2 检测到红色 NPC 靠近
在 26 万候选中选出减速让行的轨迹
Ego 平稳刹车，保持安全距离
整个过程：无碰撞、无压线、无闯红灯
**Driving Score 全保留**


>>> 违规与扣分公式 #B06
@enter: fade
@exit: fade
@visual: image

--- visual ---
一张 16:9 横构图的违规系数公式图，扁平化技术风格。深色背景 #0d1117。

顶部居中标题 "违规与扣分公式"，白色 #e6edf3 粗体大字；副标题 "每种违规对应一个乘法系数，累乘成 Infraction Score"，灰色 #8b949e。

画面中央上半部是四个违规系数卡片（横向 2×2 网格，总宽占画布 80%，每张圆角 16 px、深色背景 #161b22、2 px 边框、内边距大）：

卡片 1 "碰撞行人"（红色 #f85149 边框）：
- 顶部一个简约碰撞图标（叠加的两个色块 + 红色 ⚡）
- 中间一个超大粗体红色系数 "× 0.50"
- 下方小字 "最严重"
- 底部 "Bench2Drive penalty factor"

卡片 2 "碰撞车辆"（红色 #f85149 边框）：
- 系数 "× 0.60"
- 下方小字 "次严重"

卡片 3 "闯红灯"（金色 #d29922 边框）：
- 系数 "× 0.70"

卡片 4 "压线 / Off-Road"（金色 #d29922 边框）：
- 系数 "× 0.95"（按时长累乘）
- 下方小字 "每段时间窗累乘"

画面下半部居中是一个公式区（深色背景 #161b22 圆角 12 px、内边距大、等宽字体）：

行 1 大字（白色 #e6edf3 中等字号）：
"Infraction Score = ∏ penalty_factor_i"

行 2 大字（亮蓝色 #58a6ff 粗体中字号）：
"DS = Route Completion × Infraction Score"

公式区下方一行小字（金色 #d29922 中等字号）：
"超时不在乘法里——超时直接判该路线为零分"

整体风格干净、数字按字面准确渲染（系数必须为 0.50 / 0.60 / 0.70 / 0.95，不要写成百分数）。

--- narration ---
闭环评测中
每种违规对应一个**乘法系数**
碰撞行人最严重 ×0.5
碰撞车辆 ×0.6
闯红灯 ×0.7
压线和偏离按时间窗累乘 ×0.95
所有违规系数累乘得到 Infraction Score
再乘以路线完成率
就是最终的 Driving Score
超时不计入乘法
超时直接判该路线零分
这套公式体现了闭环评测的核心
既要开得远，又要开得安全


>>> 失败案例一：ALG 域差（弯道） #B07
@enter: fade
@exit: fade
@visual: video(./assets/fail_changelane_topdown.mp4)

--- visual ---
（本块使用本地视频 ./assets/fail_changelane_topdown.mp4，无需生成图片）

SparseDriveV2 在 Town04 弯道 ChangeLane 场景中的失败案例，鸟瞰视角。
Ego 车（蓝色）进入弯道后，模型输出近零横向轨迹（域差：训练数据以直道为主），
导致 Ego 偏离道路。AutoSim verify_batch 自动诊断：steer_abs_max ≈ 0、
nonzero_steer_ticks = 0/250、off-road 81%。
**这不是工程 bug，而是 ALG 算法局限。**

--- narration ---
来看两类失败
**第一类：算法域差**
这是 Town04 的弯道路段
Ego 进入弯道后
SparseDriveV2 输出了近乎直线的轨迹
因为模型在 nuScenes 和 NAVSIM 数据上训练
这两个数据集都以直道场景为主
模型在 CARLA 的弯道几何上表现不佳
自动诊断脚本显示：steer 全程为 0，81% 的 tick 已 off-road
这不是工程错误
而是算法域差
解决需要针对 CARLA 弯道做轻量微调


>>> 失败案例二：SCN 场景几何（cut_in_right） #B08
@enter: fade
@exit: fade
@visual: image

--- visual ---
一张 16:9 横构图的双场景对比示意图，扁平化技术风格。深色背景 #0d1117。

顶部居中标题 "失败案例二：SCN 场景几何"，白色 #e6edf3 粗体大字；副标题 "cut_in_right：NPC 始终未真切入 Ego 车道"，金色 #d29922。

画面分左右两栏，总宽占画布 88%，间距充足。

左栏 "期望中的 cut_in_right"（橙色 #f0883e 边框、圆角 16 px、深色背景 #161b22）：
- 一段双车道俯视图：右车道 Ego（蓝色色块），左车道 NPC（红色色块）从 Ego 后方追上后向 Ego 车道**斜切汇入**（红色路径用粗箭头明显跨过车道线）。
- 下方标签 "理想剧本：NPC 真切入"，中等字号白色。

右栏 "实际发生的（Bench2Drive Town04 弯道）"（红色 #f85149 边框）：
- 同样的双车道俯视图，但弯道弯曲。NPC 路径与 Ego 路径**全程平行**（红色路径与 Ego 路径几乎平行，未跨车道线），最近距离仍保持 ≈5 m。
- 下方标签 "实际：NPC 走平行 waypoint，始终未跨车道线"，中等字号白色。

画面下方居中一行诊断证据卡片（深色背景 #161b22 圆角 12 px、内边距大、等宽字体 monospace、白色 #e6edf3）：

verify_batch.py 自动诊断：
- npc_in_lane_ticks = 0          ← NPC 从未进入 Ego 车道
- min_lat_offset = 2.9 m → 12 m   ← 横向间距单调增大
- ego brake_max = 1.00            ← 模型有刹车，但是因为旁边有车，不是因为 cut-in

底部一行金色 #d29922 中等字号粗体：
"诊断分类：SCN（场景几何问题，不属 ENG 也不属 ALG）"

整体风格干净、双栏对比清晰、文字按字面准确渲染。

--- narration ---
**第二类：场景几何局限**
cut_in_right 这条 case 看上去 Ego 减速了
但仔细看 NPC 的轨迹
它从未真正切入 Ego 车道
而是沿弯道走了一条平行路径
横向距离从 2.9 米单调增大到 12 米
自动诊断脚本把这归为 **SCN**——场景几何问题
不是工程 bug
也不是算法局限
而是 bench2drive 行为树在这段弯道上
本来就没设计 NPC 切入 Ego 车道
诚实展示边界，比掩盖问题更重要


>>> 训练 Pipeline #B09
@enter: fade
@exit: fade
@visual: image

--- visual ---
一张 16:9 横构图的两阶段训练流程图，扁平化技术风格。深色背景 #0d1117。

顶部居中标题 "训练 Pipeline"，白色 #e6edf3 粗体大字。

画面中央两个并排大卡片，总宽占画布 85%，中间一个右指大箭头（亮蓝色 #58a6ff）。

卡片 1 "Stage 1: Perception Pre-training"（圆角 16 px、深色背景 #161b22、2 px 亮蓝色 #58a6ff 边框、内边距大）：
- 标题白色粗体中字。
- 中部参数列表（等宽字体）：
  - 100 epochs
  - Batch 8
  - LR 4e-4
- 下方标签 "只训感知，冻结规划"，灰色 #8b949e。

卡片 2 "Stage 2: Joint End-to-End"（2 px 绿色 #3fb950 边框）：
- 参数：
  - 10 epochs
  - Batch 128
  - LR 1e-4
- 标签 "全模块联合，梯度从规划回传感知"。

画面底部居中一个胶囊形信息条，深色背景 #161b22 圆角 8 px、白色 #e6edf3 中等字号：
"8 × NVIDIA L20 · 总时长 ~10h · 对比 UniAD A100 × 144h"

整体风格干净、对齐严格、文字按字面准确渲染。

--- narration ---
训练分两阶段进行
第一阶段
只训练感知模块 100 个 epoch
让检测和建图充分收敛
第二阶段
联合训练 10 个 epoch
梯度从规划回传到感知
8 张 L20 GPU
总时长约 10 小时
对比 UniAD 在 A100 上 144 小时
效率提升超过一个数量级


>>> Loss Function #B10
@enter: fade
@exit: fade
@visual: image

--- visual ---
一张 16:9 横构图的损失函数公式图，扁平化技术风格。深色背景 #0d1117。

顶部居中标题 "损失函数"，白色 #e6edf3 粗体大字。

画面上半部居中一个大公式块（深色背景 #161b22 圆角 12 px、内边距大、等宽字体 monospace、白色 #e6edf3 中等字号粗体）：

"L = L_det + L_map + L_motion + L_plan + L_depth"

公式块下方一行间距处，是 5 个并列小卡片（横向排列，总宽占画布 88%，每张圆角 12 px、深色背景 #161b22、2 px 不同色边框、内边距适中）：

卡片 1 "L_det"，亮蓝色 #58a6ff 边框；下方 "检测：Focal + L1"
卡片 2 "L_map"，绿色 #3fb950 边框；下方 "建图：分类 + 回归"
卡片 3 "L_motion"，橙色 #f0883e 边框；下方 "预测：Winner-Takes-All"
卡片 4 "L_plan"，紫色 #a371f7 边框；下方 "规划：Path + Velocity + Trajectory"
卡片 5 "L_depth"，金色 #d29922 边框；下方 "深度：辅助监督"

画面底部居中一行小字（灰色 #8b949e 中等字号）：
"Winner-Takes-All：只有最接近 GT 的 mode 参与 loss 计算"

整体风格干净、对齐严格、公式按字面准确渲染（下划线、加号都不能错）。

--- narration ---
总损失由五个分量组成
检测、建图、运动预测、规划
还有一个辅助的深度监督
运动预测和规划采用 Winner-Takes-All
只有最接近 GT 的 mode 参与优化
这种多任务联合训练
正是端到端优于模块化方案的根本原因


>>> 闭环评测结果 #B11
@enter: fade-up
@exit: fade
@visual: image

--- visual ---
一张 16:9 横构图的评分公式可视化图，扁平化技术风格。深色背景 #0d1117。

顶部居中标题 "闭环评测结果"，白色 #e6edf3 粗体大字。

画面上半部（占画布高 50%）是一个简化俯视地图：一条从起点（绿色 ✓ 标志）到终点（金色旗帜）的弯曲路线，路线上有一辆蓝色 Ego 车位于终点位置。途中路线上有一个标签 "cut-in 场景" 和一个 "✓ 安全通过" 绿色文字标注。

画面下半部（占画布高 45%）是一个三段公式动画的静态最终态——三个分数块从左到右展开，每块圆角 16 px、内边距大：

块 1 "Route Completion"：白色背景圆角矩形（深色 #0d1117 文字）"95%"，下方一个细进度条 95% 填充绿色 #3fb950。

→ 大字号亮蓝色 "×"。

块 2 "Infraction Score"：橙色 #f0883e 边框、深色背景 #161b22；中间大字 "0.94"（白色粗体）；下方小字 "（一次轻微压线 ×0.95）"。

→ 大字 "="。

块 3 "Driving Score = 89.15"（亮蓝色 #58a6ff 实心填充、深色 #0d1117 粗体超大字号）。

画面底部居中一行精简对比（白色 #e6edf3 中等字号）：
"SparseDriveV2: DS 89.15 · SR 70.00%   |   DriveSuprim: DS 83.02 · SR 60.00%"

整体风格干净、公式可读、数字按字面准确渲染。

--- narration ---
我们跟着一条路线看结果
Ego 车从起点出发
在 CARLA 中自动驾驶
途中遇到切入、超车、让行等场景
SparseDriveV2 做出正确决策，安全通过
到达终点后
Route Completion 95%
乘以 Infraction Score 0.94
得到 Driving Score 89.15
对比第二名 DriveSuprim 只有 83.02
成功率领先 10 个百分点
这是在 CARLA 真实驾驶得出的成绩


>>> 全面对比 #B12
@enter: fade
@exit: fade
@visual: image

--- visual ---
一张 16:9 横构图的对比表，扁平化技术风格。深色背景 #0d1117。

顶部居中标题 "从 UniAD 到 SparseDriveV2"，白色 #e6edf3 粗体大字。

画面中央是一个 4 列 × 8 行的对比表（含表头），总宽占画布 85%、深色背景 #161b22、圆角 12 px、内边距大。

表头行（背景略亮 #1a2332，文字灰色 #8b949e 中等字号）：
| | UniAD (2023) | SparseDrive v1 (2024) | SparseDriveV2 (2026) |

数据行（白色 #e6edf3 中等字号，行高充足）：
| 表示       | Dense BEV  | Sparse        | Sparse                 |
| 规划       | 回归 1 条   | 生成 6 条      | 打分 262K 条            |
| Backbone   | R-101      | R-50/101      | R-34                   |
| 训练       | 144h A100  | 20h 4090      | ~10h L20               |
| 推理       | 1.8 FPS    | 9.0 FPS       | 实时                    |
| 评测       | 开环       | 开环          | 开环 + 闭环             |
| 闭环 DS    | —          | —             | 89.15                  |

最右一列（SparseDriveV2）的所有数值用绿色 #3fb950 高亮；"开环 + 闭环" 和 "89.15" 加粗。

画面底部居中一行总结（白色 #e6edf3 中等字号粗体）：
"从 Dense 到 Sparse，从生成到打分，从开环到闭环 —— 三步跨越"

整体风格干净、表格对齐严格、所有数字与文字按字面准确渲染。

--- narration ---
来做最后一次全面对比
从 UniAD 到 SparseDriveV2
表示方式从 Dense BEV 走向全 Sparse
规划方式从单条回归到 26 万打分
Backbone 从 ResNet-101 缩小到 ResNet-34
训练从 A100 上 144 小时
降到 L20 上约 10 小时
最重要的是
SparseDriveV2 是唯一做闭环的方案
在 CARLA 上用真实驾驶验证了自己


>>> 系列总结与展望 #B13
@enter: fade-up
@exit: fade
@visual: image

--- visual ---
一张 16:9 横构图的系列回顾图，扁平化技术风格。深色背景 #0d1117。

顶部居中标题 "系列回顾 · 六集旅程"，白色 #e6edf3 粗体大字。

画面中央偏上是一条横向时间线（亮蓝色 #58a6ff 4 px 实线），线上等距 6 个圆形节点（直径 32 px、实心亮蓝色 #58a6ff、白色数字 01–06）。

每个节点上方一行集名小字，下方一行要点（中等字号 #e6edf3）：

01 - CARLA 架构        ｜ Ego 车创建 · 最小实验 ~25 行代码
02 - 传感器系统        ｜ 6 相机数据流 · GT 训练/推理区分
03 - 仿真引擎          ｜ 同步数据闭环 · tick→inference→control
04 - 范式演进          ｜ Dense → Vectorized → Sparse · Scoring 动机
05 - SparseDriveV2     ｜ Factorized Vocab · Coarse-to-Fine
06 - 闭环评测          ｜ 流水线 · Penalty · DS/SR 出分

时间线最右端有一辆简约 Ego 车线条图标（白色），表示"已抵达终点"。

时间线下方居中一个展望卡片（深色背景 #161b22 圆角 12 px、内边距大、宽度 75%）：
- 标题 "从仿真到真实"，亮蓝色 #58a6ff 中等字号粗体
- 两行展望（白色 #e6edf3）：
  - World Model + 闭环仿真 → 更真实的训练环境
  - Vision-Language Model + Driving → 自然语言指令驾驶

画面底部居中一行小字（灰色 #8b949e 中等字号）：
"感谢观看 · 代码与论文见 SparseDriveV2 GitHub"

整体风格干净、时间线对齐严格、文字清晰。

--- narration ---
六集教程到这里全部结束
从 CARLA 的 Client-Server 架构开始
给 Ego 车装上传感器
跑通 tick 同步闭环
理解端到端范式的演进
深入拆解 SparseDriveV2 的每个模块
最后在 CARLA 上完成闭环评测验证
未来的方向是
World Model 和 VLM 驱动的自动驾驶
感谢观看
希望这个系列让你真正理解了
CARLA 提供世界
传感器提供输入
SparseDriveV2 输出轨迹
Bench2Drive 负责验证
