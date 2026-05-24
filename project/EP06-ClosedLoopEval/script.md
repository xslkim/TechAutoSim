>>> 开场 #B01
@enter: fade-up
@exit: fade
@visual: animation

--- visual ---
全屏深色背景 (#0d1117)。画面垂直居中布局，内容占画布 85% 宽度：
[0s] 顶部标签 "CARLA × SparseDriveV2 仿真教程"，字号 28px，颜色 #8b949e。
[0.3s] 主标题 "EP06: 闭环评测实战" 淡入，白色 (#e6edf3)，粗体，字号 96px，居中。
[0.8s] accent 色横线从中心向两侧扫出。
[1.2s] 副标题 "从训练好的模型到 CARLA 考场，完整闭环 Pipeline"，字号 34px，颜色 #8b949e。
[1.8s] 画面中央出现系列知识回顾条：从左到右依次排列 "CARLA 环境 ✓ → 传感器 ✓ → tick 循环 ✓ → SparseDriveV2 ✓"，每个标签有绿色对号。最后一个标签 "闭环评测 ← 本集" 闪烁，accent 色。

--- narration ---
欢迎来到全系列最后一集
五集下来，我们建好了 CARLA 环境
装好了传感器，跑通了 tick 循环
深入理解了 SparseDriveV2 的每个模块
现在是最终考验：把训练好的模型放到 CARLA 考场里
跑 Bench2Drive 闭环评测，看它到底能不能安全开车


>>> 开环 vs 闭环 #B02
@enter: fade
@exit: fade
@visual: animation

--- visual ---
深色背景 (#0d1117)，内容区域占画布 90% 宽度。
[0s] 顶部居中标题 "开环 vs 闭环评测"，字号 56px，粗体，白色，距顶 70px。

[0.5s] 下方出现左右两栏对比，总宽占画布 88%，间距 48px：

左栏 "Open-Loop"，宽度 45%，标题 #f0883e：
  示意图：固定轨迹线和预测轨迹线并排，标注 "L2 Error"
  要点字号 22px："回放录制数据 · Agent 决策不影响环境 · 只看轨迹偏差"
  代表基准：nuScenes / NAVSIM

右栏 "Closed-Loop"，宽度 45%，标题 #3fb950：
  示意图：循环箭头 "感知→规划→控制→环境响应→感知"
  要点："Agent 操作改变环境 · 碰撞真实发生 · 评估安全+任务完成"
  代表基准：CARLA Leaderboard / Bench2Drive

两栏依次淡入：[0.5s] 左 → [2s] 右。
[4s] 底部标注 "SparseDriveV2 两种评测都做，但闭环才是真考试"，字号 24px，颜色 #58a6ff。

--- narration ---
先区分两种评测
开环是回放数据，模型做预测但结果不影响环境
看的是 L2 轨迹偏差
闭环则完全不同，Agent 做的每个决策都在仿真里真实执行
碰撞、违规都会真实发生
SparseDriveV2 是少数两种评测都做的方案


>>> Bench2Drive：考试协议 #B03
@enter: fade-up
@exit: fade
@visual: animation

--- visual ---
深色背景 (#0d1117)，内容区域占画布 88% 宽度。
[0s] 顶部居中标题 "Bench2Drive — 基于 CARLA 的闭环考试"，字号 52px，粗体，白色，距顶 60px。

[0.5s] 画面中央出现考试流程全景图，总宽占画布 88%：

从左到右五个阶段（每个是圆角矩形，宽 160px，高 80px，背景 #161b22，边框 2px）：

阶段 1 "Checkpoint 加载" (#58a6ff 边框)：
  图标：文件 + 下载箭头
  文字 "SparseDriveV2 权重" 字号 20px

→ 箭头 →

阶段 2 "连接 CARLA" (#3fb950 边框)：
  图标：Server + Client
  文字 "同步模式启动" 字号 20px

→ 箭头 →

阶段 3 "加载 Route" (#f0883e 边框)：
  图标：地图 + 路径线
  文字 "220 条测试路线" 字号 20px
  下方 "44 种交互场景" 字号 16px

→ 箭头 →

阶段 4 "Agent 驾驶" (#a371f7 边框)：
  图标：Ego 车 + 轨迹
  文字 "tick 循环中推理" 字号 20px
  下方 "每 50ms 一次决策" 字号 16px

→ 箭头 →

阶段 5 "评分出分" (#d29922 边框)：
  图标：计分板
  文字 "DS / SR / Multi-Ability" 字号 20px

各阶段依次淡入，间隔 0.4s。

--- narration ---
Bench2Drive 是建立在 CARLA 上的标准化闭环考试
流程分五步
加载训练好的 SparseDriveV2 checkpoint
连接 CARLA Server 并开启同步模式
加载测试路线，一共 220 条，覆盖 44 种交互场景
Agent 自动驾驶，在每 50ms 的 tick 间隔内完成推理和控制
最后汇总所有路线的结果，得出三个核心分数


>>> 闭环评测流水线 #B04
@enter: fade
@exit: fade
@visual: animation

--- visual ---
深色背景 (#0d1117)，内容区域占画布 94% 宽度。
[0s] 顶部居中标题 "闭环评测流水线"，字号 52px，粗体，白色，距顶 55px。副标题 "每帧都在这条流水线上运转" 字号 24px，颜色 #58a6ff。

[0.5s] 画面主体是一条从左到右的流水线，总宽占画布 92%，每个阶段依次亮起：

阶段 1 "world.tick()" (宽 140px，背景 #161b22，边框 #58a6ff)：仿真推进一帧 →

阶段 2 "6 Camera Capture" (宽 160px，边框 #3fb950)：6 个相机同步采集图像 →

阶段 3 "SparseDriveV2 Forward" (宽 200px，边框 #a371f7)：感知 + 建图 + 规划 → 输出轨迹 →

阶段 4 "apply_control()" (宽 150px，边框 #d29922)：油门/转向/刹车 →

阶段 5 "Infraction Check" (宽 180px，边框 #f0883e)：每一帧检测违规——
  下方展开三个小检测器图标：
  "Collision?" (红色) / "Red Light?" (红色) / "Lane Invasion?" (黄色)
  每个检测器在检测到违规时闪烁红色

[3.5s] 流水线进入阶段 6 "Log Accumulation" (宽 160px，边框 #30363d)：
  每条路线结束后，所有 infractions 汇总
  一个 infractions log 面板弹出，展示违规记录

[4.5s] 底部出现标注："每条路线独立记录 · 220 条路线汇总 → Driving Score"，字号 22px，颜色 #8b949e。

--- narration ---
来看闭环评测的完整流水线
每帧从 world.tick 开始，6 个相机同步采集
SparseDriveV2 做一次完整推理，输出规划轨迹
apply_control 发送油门、转向和刹车
同时，每帧都在检查违规
碰撞、闯红灯、压线、偏离路线
每次违规都被记录到 infractions log
220 条路线全部跑完后，汇总出 Driving Score


>>> 失败案例：违规的代价 #B05
@enter: fade-up
@exit: fade
@visual: animation

--- visual ---
深色背景 (#0d1117)，内容区域占画布 92% 宽度。
[0s] 顶部居中标题 "每次违规都扣分"，字号 52px，粗体，白色，距顶 55px。

[0.5s] 画面中央出现四个失败场景卡片（2×2 网格），总宽占画布 88%，间距 24px：
每个卡片宽 44%，高 200px，圆角 16px，背景 #161b22，边框 2px solid #30363d，内边距 20px：

卡片 1 "碰撞前车" [0.5s]：
  场景图标：Ego 车追尾前车，碰撞点用红色爆炸图标 (#f85149)
  penalty badge 弹出（红色大圆形，内部 "−40%"，字号 40px，粗体）
  说明 "Collision Penalty · 最重扣分" 字号 20px，颜色 #f85149

卡片 2 "闯红灯" [1.3s]：
  场景图标：Ego 车在红灯亮时通过路口
  penalty badge "−20%"
  说明 "Red Light Violation" 字号 20px

卡片 3 "压线/偏离" [2.1s]：
  场景图标：Ego 车压在车道线上
  penalty badge "−10%"
  说明 "Lane Invasion / Off-Road" 字号 20px

卡片 4 "超时" [2.9s]：
  场景图标：Ego 车停在路中不动，计时器走到零
  penalty badge "TIMEOUT"
  说明 "Route Timeout → 该路线 0 分" 字号 20px，颜色 #f85149

[4s] 四个卡片中央出现汇总动画：所有 penalty badge 飞入一个公式区，拼成：
  "Infraction Score = 1.0 − sum(penalties)" 字号 28px，颜色 #f0883e
  下方 "DS = Route Completion × Infraction Score" 字号 32px，颜色 #e6edf3

--- narration ---
闭环评测中，每次违规都要付出代价
**碰撞行人或车辆**是最严重的，扣分最重
**闯红灯**次之
**压线或偏离道路**再次
**超时未完成路线**，整条路线直接零分
所有路线的违规记录汇总成 Infraction Score
乘以 Route Completion 就是最终的 **Driving Score**
这个公式体现了闭环评测的核心 —— 既要开得远，又要开得安全


>>> 训练 Pipeline #B06
@enter: fade
@exit: fade
@visual: animation

--- visual ---
深色背景 (#0d1117)，内容区域占画布 88% 宽度。
[0s] 顶部居中标题 "训练 Pipeline"，字号 52px，粗体，白色，距顶 70px。

[0.5s] 画面中央出现两阶段训练流程，总宽占画布 85%：

阶段 1 矩形（宽 42%，圆角 16px，背景 #161b22，边框 2px solid #58a6ff）：
  标题 "Stage 1: Perception Pre-training" 字号 22px
  内部精简参数："100 epochs · Batch 8 · LR 4e-4" 字号 20px
  标注 "只训感知，冻结规划" 字号 18px，颜色 #8b949e

→ 箭头 →

阶段 2 矩形（同尺寸，边框 #3fb950）：
  标题 "Stage 2: Joint End-to-End" 字号 22px
  参数 "10 epochs · Batch 128 · LR 1e-4" 字号 20px
  标注 "全模块联合训练，梯度从规划回传感知" 字号 18px

[3.5s] 底部硬件条："8 × NVIDIA L20 GPU · 对比 UniAD: A100 × 144h → L20 × ~10h"，字号 22px，颜色 #e6edf3。

--- narration ---
训练分两阶段进行
第一阶段只训练感知模块 100 epoch，让检测和建图充分收敛
第二阶段联合训练 10 epoch，梯度从规划回传到感知
8 张 L20 GPU 完成，对比 UniAD 在 A100 上训练 144 小时
效率提升超过一个数量级


>>> Loss Function #B07
@enter: fade
@exit: fade
@visual: animation

--- visual ---
深色背景 (#0d1117)，内容区域占画布 88% 宽度。
[0s] 顶部居中标题 "损失函数"，字号 52px，粗体，白色，距顶 80px。

[0.5s] 画面中央出现总公式，宽占画布 70%，背景 #161b22，圆角 12px，内边距 20px：
"L = L_det + L_map + L_motion + L_plan + L_depth" 字号 32px，等宽字体，颜色 #e6edf3

[1.5s] 公式下方出现五个损失项的词云式排列（非列表，而是散布在公式周围）：
  L_det (#58a6ff) "检测：Focal + L1"
  L_map (#3fb950) "建图：分类 + 回归"
  L_motion (#f0883e) "预测：Winner-Takes-All"
  L_plan (#a371f7) "规划：Path + Velocity + Trajectory"
  L_depth (#d29922) "深度：辅助监督"

各项依次淡入，间距 0.2s。

[3s] 底部注释："Winner-Takes-All — 只有最接近 GT 的 mode 参与 loss 计算。多任务联合训练 = 端到端的核心优势。"，字号 22px，颜色 #8b949e。

--- narration ---
总损失由五个分量组成
检测、建图、运动预测、规划和一个辅助的深度监督
运动预测和规划采用 Winner-Takes-All 策略
只有最接近 Ground Truth 的那个 mode 参与优化
这种多任务联合训练正是端到端优于模块化方案的根本原因


>>> 闭环评测结果 #B08
@enter: fade-up
@exit: fade
@visual: animation

--- visual ---
深色背景 (#0d1117)，内容区域占画布 92% 宽度。
[0s] 顶部居中标题 "闭环评测结果"，字号 52px，粗体，白色，距顶 55px。

[0.5s] 画面中央不是表格，而是一场"路线完成动画"：

一个简化的俯视地图（宽 70%，高 280px，背景 #0d1117，边框 1px #30363d），上面有一条从起点到终点的路线。

[1s] Ego 车从起点出发，沿路线行驶（动画）。
[2s] 行驶到一半，出现一个场景：前方有车切入（场景标签弹出）。Ego 平滑减速让行（绿色 ✓）。
[3s] 继续行驶，接近终点。
[3.5s] Ego 车到达终点，画面弹出三个分数（依次展开）：

"Route Completion: 95%" (进度条，绿色 #3fb950 填充 95%) → 
  "×" →
"Infraction Score: 0.94" (轻微扣分，因为有一次压线) →
  "=" →
"Driving Score = 89.15" (大字弹出，粗体，颜色 #58a6ff)

[5s] 底部出现精简对比数据（单行标签）：
  "SparseDriveV2: DS 89.15 · SR 70.00%  vs  DriveSuprim: DS 83.02 · SR 60.00%"
  字号 22px，颜色 #e6edf3

--- narration ---
我们跟着一条路线来理解结果
Ego 车从起点出发，在 CARLA 中自动驾驶
途中遇到切入、超车、让行等场景
SparseDriveV2 做出正确决策，安全通过
到达终点后，Route Completion 乘以 Infraction Score
得到 Driving Score 89.15
对比第二名 DriveSuprim 只有 83.02
成功率领先 10 个百分点
这是在 CARLA 里真实驾驶得出的成绩


>>> 全面对比 #B09
@enter: fade
@exit: fade
@visual: animation

--- visual ---
深色背景 (#0d1117)，内容区域占画布 90% 宽度。
[0s] 顶部居中标题 "从 UniAD 到 SparseDriveV2"，字号 52px，粗体，白色，距顶 55px。

[0.5s] 画面中央出现精简对比表，总宽占画布 85%，背景 #161b22，圆角 12px：
表头行背景 #1a2332，字号 20px，颜色 #8b949e：
"" | "UniAD (2023)" | "SparseDrive v1 (2024)" | "SparseDriveV2 (2026)"

数据行字号 22px，行高 40px：
"表示" | "Dense BEV" | "Sparse" | "Sparse"
"规划" | "回归 1 条" | "生成 6 条" | "打分 262K 条"
"Backbone" | "R-101" | "R-50/101" | "R-34"
"训练" | "144h A100" | "20h 4090" | "~10h L20"
"推理" | "1.8 FPS" | "9.0 FPS" | "实时"
"评测" | "开环" | "开环" | "开环 + 闭环"
"闭环 DS" | "—" | "—" | "89.15"

SparseDriveV2 列数值用 #3fb950 高亮。"开环 + 闭环" 和 "89.15" 用粗体。

[4s] 表格下方出现总结文字："从 Dense 到 Sparse，从生成到打分，从开环到闭环 — 三步跨越"，字号 24px，颜色 #e6edf3。

--- narration ---
来做最后一次全面对比
从 UniAD 到 SparseDriveV2
表示方式从 Dense BEV 走向全 Sparse
规划方式从单条回归到 26 万打分
Backbone 从 ResNet-101 缩小到 ResNet-34
训练从 A100 上 144 小时降到 L20 上约 10 小时
最重要的是 SparseDriveV2 是唯一做闭环的方案
在 CARLA 上用真实驾驶验证了自己


>>> 系列总结与展望 #B10
@enter: fade-up
@exit: fade
@visual: animation

--- visual ---
全屏深色背景 (#0d1117)。画面垂直居中布局，内容占画布 88% 宽度。
[0s] 顶部标题 "系列回顾 · 六年旅程"，字号 52px，粗体，白色，距顶 60px。

[0.5s] 画面中央出现水平时间线 + 路径图：

一条宽水平线（4px，颜色 #30363d），代表六集的旅程。线上排列 6 个节点（圆形，直径 32px，accent 色）：

节点 1 [0.5s] "01" | "CARLA 架构 — Ego 车创建 · 最小实验 15 行代码"
节点 2 [1s] "02" | "传感器系统 — 6 相机数据流 · GT 训练/推理区分"
节点 3 [1.5s] "03" | "仿真引擎 — 同步数据闭环 · tick→inference→control"
节点 4 [2s] "04" | "范式演进 — Dense→Vectorized→Sparse · Scoring 动机"
节点 5 [2.5s] "05" | "SparseDriveV2 — Factorized Vocab · Coarse-to-Fine"
节点 6 [3s] "06" | "闭环评测 — 流水线 · Penalty · DS/SR 出分"

每节点依次亮起，对应的 icon 浮现（车→相机→环→对比图→打分矩阵→奖杯）。

[4s] 整条时间线变成 accent 色 (#58a6ff)，Ego 车图标从节点 1 行驶到节点 6。

[4.5s] 下方 40px 出现展望区域（背景 #161b22，圆角 12px，内边距 20px，宽度 75%）：
  标题 "从仿真到真实" 字号 26px，颜色 #58a6ff
  "World Model + 闭环仿真 → 更真实的训练环境" 字号 22px
  "Vision-Language Model + Driving → 自然语言指令驾驶" 字号 22px

[5.5s] 底部 "感谢观看 · 代码与论文见 SparseDriveV2 GitHub"，字号 24px，颜色 #8b949e。

--- narration ---
六集教程到这里全部结束了
我们从 CARLA 的 Client-Server 架构开始
给 Ego 车装上传感器，跑通 tick 同步闭环
理解端到端范式从不做 Dense BEV 到 Sparse Scoring 的演进
深入拆解了 SparseDriveV2 的每个模块
最后在 CARLA 上完成闭环评测验证
未来的方向是 World Model 和 VLM 驱动的自动驾驶
感谢观看，希望这个系列让你真正理解了
CARLA 提供世界，传感器提供输入
SparseDriveV2 输出轨迹，Bench2Drive 负责验证
