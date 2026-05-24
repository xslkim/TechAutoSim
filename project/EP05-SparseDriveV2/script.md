>>> 开场 #B01
@enter: fade-up
@exit: fade
@visual: animation

--- visual ---
全屏深色背景 (#0d1117)。画面垂直居中布局，内容占画布 85% 宽度：
[0s] 顶部标签 "CARLA × SparseDriveV2 仿真教程"，字号 28px，颜色 #8b949e。
[0.3s] 主标题 "EP05: SparseDriveV2 架构解析" 淡入，白色 (#e6edf3)，粗体，字号 84px，居中。
[0.8s] accent 色横线从中心向两侧扫出。
[1.2s] 副标题 "Scoring is All You Need"，字号 40px，颜色 #58a6ff，等宽字体。
[1.8s] 画面左下角回忆锚点：上一集结尾的"生成 vs 打分"对比框（缩小版），标注 "上一集留下的问题：怎么让候选池足够密又可计算？→ 本集答案"

--- narration ---
欢迎来到第五集，全系列技术含量最高的一集
上一集结尾我们留了一个问题
打分范式的候选池需要足够密，但 26 万条轨迹怎么高效评分？
这集我们深入拆解 SparseDriveV2 的每一个模块
看看它是怎么做到的


>>> 整体架构概览 #B02
@enter: fade
@exit: fade
@visual: animation

--- visual ---
深色背景 (#0d1117)，内容区域占画布 94% 宽度。
[0s] 顶部居中标题 "整体架构"，字号 56px，粗体，白色，距顶 60px。

[0.5s] 画面中央出现从左到右的流程图，总宽占画布 92%：

模块 1 "6× Surround Cameras"：2×3 排列的小矩形，标注 "Input"
→ 模块 2 "Image Encoder"（宽 150px，圆角 12px，背景 #161b22，边框 #a371f7，内部 "ResNet-34 + FPN" 字号 20px）
→ 模块 3 "Symmetric Sparse Perception"（宽 260px，圆角 12px，背景 #161b22，边框 #58a6ff，内部分两行："Detection & Tracking" / "Online Mapping" 字号 20px）
→ 模块 4 "Scoring-Based Planner"（宽 260px，圆角 12px，背景 #161b22，边框 #3fb950，内部 "Factorized Vocabulary" / "Coarse-to-Fine Scoring" 字号 20px）
→ 模块 5 "Planning Trajectory"（宽 160px，背景 #3fb950，字号 20px，颜色 #0d1117）

各模块依次淡入，间隔 0.4s。

[4s] 流程图下方出现虚线箭头从 Output 回到 Image Encoder，标注 "端到端梯度流 (End-to-End Gradient Flow)" 字号 20px，颜色 #d29922。

--- narration ---
SparseDriveV2 的整体架构分为四个模块
6 个环视相机图像 → Image Encoder 提取特征
→ Symmetric Sparse Perception 做稀疏检测、跟踪和建图
→ Scoring-Based Planner 对候选轨迹打分
整个链路端到端可微


>>> 模型的"眼睛"：前向三相机实拍 #B03
@enter: fade
@exit: fade
@visual: video(./assets/CAM_FRONT.mp4)

--- visual ---
SparseDriveV2 的三路前向相机输入之一：CAM_FRONT。这是 CARLA 仿真中 Ego 车前方视角的原始 RGB 画面。模型在每个 tick 接收 CAM_FRONT、CAM_FRONT_LEFT、CAM_FRONT_RIGHT 三路图像，内部 resize 到 1920×1080 后送入 ResNet-34 backbone。

--- narration ---
先直观感受一下 SparseDriveV2 看到的画面
这是前视相机 CAM_FRONT 的原始输出
加上左前和右前，三路前向相机是模型规划的依据
后向三路相机在 SparseDriveV2 中用于建图辅助
但规划主要依赖前方视野
这些画面每秒更新 10 次，每次都要在 50ms 内完成
从像素到轨迹的完整推理


>>> Image Encoder #B04
@enter: fade-up
@exit: fade
@visual: animation

--- visual ---
深色背景 (#0d1117)，内容区域占画布 88% 宽度。
[0s] 顶部居中标题 "Image Encoder"，字号 56px，粗体，白色，距顶 80px。

[0.5s] 画面中央出现编码器示意图，总宽占画布 78%：

左侧：6 个相机图像（2×3 排列的小矩形，标注 "6×H×W×3"）
→ 梯形 Backbone 示意（左高右矮，表示特征逐层缩小），内部 "ResNet-34"，4 层依次标注 1/4→1/8→1/16→1/32 分辨率
→ FPN 金字塔 → 输出多尺度特征（S 个尺度×N 个视角）

[3s] 底部出现精简参数条（横排 3 个标签，背景 #161b22，圆角 8px，字号 20px）：
  "Backbone: ResNet-34 · 21.8M 参数"  
  "总参数量 ~50M"
  "比 UniAD 的 ResNet-101 轻量 3×"

--- narration ---
Image Encoder 是标准的 Backbone + FPN 结构
SparseDriveV2 使用 ResNet-34，只有 2180 万参数
比 UniAD 的 ResNet-101 轻量三倍
6 个相机各自提特征，FPN 融合多尺度
输出多尺度特征图供感知模块使用
整个模型参数量约 5000 万，非常轻量


>>> Deformable Aggregation：核心采样算子 #B05
@enter: fade
@exit: fade
@visual: animation

--- visual ---
深色背景 (#0d1117)，内容区域占画布 92% 宽度。
[0s] 顶部居中标题 "Deformable Aggregation"，字号 56px，粗体，白色，距顶 55px。副标题 "感知模块的核心算子 — 每个 query 如何从图像中提取信息" 字号 24px，颜色 #58a6ff。

[0.5s] 画面中央呈现本集最重要的动画之一，占画布 85%，高度占 60%：

左侧是 3D 空间场景（宽 55%）：一个蓝色 3D BBox（检测 query 的 anchor）悬浮在 3D 空间中，Ego 车在下方（简化图标）。

[1s] anchor 周围生成 8 个绿色小球（关键采样点），均匀散布在 anchor 前后左右。这些球同时亮起（带发光效果），标注 "Step 1: 生成 K 个 3D Keypoints" 字号 22px。

[2s] 8 条投影线（#58a6ff，2px，虚线）从每个绿色小球出发，射向右侧排列的 6 个相机平面（2×3 排列的矩形，尺寸不等，代表不同视角）。并不是每条线都能到达所有相机 —— 有些点在某些相机视野之外（线中断，标注"视野外"）。

[3s] 命中相机的投影点在相机平面上形成采样像素位置。从这些位置提取特征向量（小色块向量，流向绿色小球），标注 "Step 2: 投影到各相机 → 采样局部特征"。

[3.5s] 所有采样到的特征汇聚成一条流（accent 色，逐渐变粗），流入 query 的 Feature 部分。Feature 部分闪烁，标注 "Step 3: 加权聚合 → 更新 Feature"。

[4.5s] 底部标注 "自定义 CUDA 算子实现 · 每个 query 独立并行采样"，字号 20px，颜色 #3fb950。

--- narration ---
Deformable Aggregation 是整个感知模块的核心
它分三步工作
第一步，每个检测 query 在它的 3D Anchor 周围生成一组关键点
第二步，把这些 3D 关键点投影到各个相机的 2D 图像平面
只有投影落在相机视野内的才有效
第三步，在投影位置采样局部特征，加权聚合回 query
这样每个 query 就能从 6 个视角中精准提取自己的相关信息
整套操作用自定义 CUDA 算子实现，高度并行


>>> 对称稀疏感知：Detection & Tracking #B06
@enter: fade
@exit: fade
@visual: animation

--- visual ---
深色背景 (#0d1117)，内容区域占画布 90% 宽度。
[0s] 顶部居中标题 "Sparse Detection & Tracking"，字号 52px，粗体，白色，距顶 60px。副标题 "Nd 个 Instance Query → 6 层 Decoder → 3D BBox + ID" 字号 24px，颜色 #58a6ff。

[0.5s] 画面中央出现检测流水线，总宽占画布 85%：

左侧：Nd 个 query 竖排（5 条，每条 220×20px，左半 Feature 蓝色，右半 Anchor 绿色），标注 "可学习的 Instance Queries"

→ 中间 6 层 Decoder 堆叠（矩形，宽 280px，高 240px，背景 #161b22，边框 #58a6ff）：
  第 1 层（上方，浅灰 #8b949e 边框）"Non-Temporal" 字号 18px
  ——虚线分隔——
  第 2-6 层 "Temporal" 字号 18px
  每层标注 "Deformable Agg → FFN → Refine" 字号 16px
  层间有小箭头连接，表示 query 逐层精炼

→ 右侧输出区：
  上方 "3D BBox + Class + Velocity" 字号 22px，颜色 #3fb950
  下方 "Persistent Tracking ID" 字号 20px，颜色 #8b949e
  标注 "置信度 > 0.2 → 自动分配持久 ID"，字号 18px

[4s] 底部 Anchor 维度说明条："Anchor Bd = {x, y, z, ln w, ln h, ln l, sin θ, cos θ, vx, vy, vz} — 11维"，字号 22px，等宽字体，颜色 #e6edf3。

--- narration ---
检测模块维护 Nd 个 Instance Query
每个 query 的 anchor 是一个 11 维向量
编码了位置、尺寸、朝向和速度
经过 6 层 Decoder 逐步精炼
第一层无时序，后五层引入历史帧信息
每层核心操作就是刚才讲的 Deformable Aggregation
跟踪非常简洁 —— 置信度超阈值的检测自动获得持久 ID
不需要匈牙利匹配等复杂后处理


>>> 对称稀疏感知：Online Mapping #B07
@enter: fade
@exit: fade
@visual: animation

--- visual ---
深色背景 (#0d1117)，内容区域占画布 88% 宽度。
[0s] 顶部居中标题 "Sparse Online Mapping"，字号 52px，粗体，白色，距顶 70px。

[0.5s] 画面中央出现对称对比图，总宽占画布 85%：

左半 "Detection"，透明度 50%（表示回顾）："Nd Query · BBox Anchor · 6 Decoder Layers" 字号 20px
右半 "Mapping"（全亮）："Nm=100 Query · Polyline Anchor (20 点) · 6 Decoder Layers" 字号 20px

中间竖线分隔，上方 "完全对称的架构" 字号 26px，颜色 #f0883e。

[2s] 下方 50px 出现建图结果俯视示意（宽 60%，高 180px，背景 #0d1117，边框 1px #30363d）：
  三种折线在道路场景中展示：
  蓝色 "Lane Divider" (#58a6ff)
  绿色 "Road Boundary" (#3fb950)
  黄色 "Pedestrian Crossing" (#d29922)

[4s] 底部标注 "一套 Decoder 架构，两种实体类型。对称设计 = 代码复用 + 概念统一"，字号 22px，颜色 #8b949e。

--- narration ---
建图模块和检测模块是完全对称的
同样的 6 层 Decoder、同样的 Deformable Aggregation
区别只在 query 定义
检测用 11 维 BBox anchor，建图用 20 点 Polyline anchor
100 个 Map Query 对应车道线、道路边界和人行横道
一套架构处理两种实体，这个设计非常优雅


>>> Factorized Vocabulary：262K 候选的由来 #B08
@enter: fade
@exit: fade
@visual: animation

--- visual ---
深色背景 (#0d1117)，内容区域占画布 94% 宽度。
[0s] 顶部居中标题 "Factorized Vocabulary"，字号 56px，粗体，白色，距顶 55px。副标题 "轨迹 = 路径 × 速度，独立分解让规模变得可计算" 字号 26px，颜色 #3fb950。

[0.5s] 这是本集最重要的视觉动画。画面中央出现二维矩阵示意，总宽占画布 88%：

上方单独标注 "传统方案: ~8K 候选" 字号 22px，颜色 #8b949e。一个小矩形代表 8K 候选池。

中间向下箭头，标注 "SparseDriveV2:"，字号 22px，颜色 #58a6ff。

下方核心区域：

一个大的二维矩阵框架（宽 700px，高 380px，背景 #0d1117，边框 1px #30363d），标注坐标系：
  横轴 "1024 Geometric Paths (空间采样 @1m 间隔)" 字号 20px，颜色 #58a6ff
  纵轴 "256 Velocity Profiles (时间采样 @0.5s 间隔)" 字号 20px，颜色 #3fb950

横轴最左侧，展示几条代表性路径曲线（彩色，不同曲率和方向），从直的到急转弯。标注 "Path = 几何形状 · 决定'走哪条线'"。

纵轴最左侧，展示几条代表性速度曲线（彩色，不同斜率），从缓慢加速到急加速。标注 "Velocity = 速度曲线 · 决定'走多快'"。

[2s] 横轴和纵轴的交汇区域：矩阵的一个单元格高亮（闪烁），标注 "1 条轨迹 = 1 个 Path × 1 个 Velocity"。

[3s] 关键动画：矩阵中所有 1024×256 个格子从左下角开始依次点亮（涟漪扩散效果，#58a6ff 发光），形成完整网格。伴随一个"爆炸展开"的效果，标注在矩阵右下角弹出：
"1024 × 256 = 262,144 条候选轨迹" 字号 36px，粗体，颜色 #f0883e
"比传统方案密 32×" 字号 22px，颜色 #3fb950

[4.5s] 矩阵下方出现关键说明："分解后的计算量 = O(1024 + 256) = O(1280)，而非 O(262,144)"，字号 24px，颜色 #e6edf3，背景 #161b22，圆角 8px。

--- narration ---
这是 SparseDriveV2 最关键的设计
它把轨迹分解成两个独立维度
Geometric Path 决定走哪条线，1024 条
Velocity Profile 决定走多快，256 种
两者笛卡尔积 1024 乘以 256，得到 26 万条候选
比传统方案密集 32 倍
关键在于这个分解让计算量变成了加法而非乘法
O(1280) 而不是 O(262K)
这就是"足够密"变得"可计算"的秘密


>>> Coarse-to-Fine Scoring：高效筛选 #B09
@enter: fade-up
@exit: fade
@visual: animation

--- visual ---
深色背景 (#0d1117)，内容区域占画布 92% 宽度。
[0s] 顶部居中标题 "Coarse-to-Fine Scoring"，字号 52px，粗体，白色，距顶 55px。副标题 "从 26 万到最优轨迹的两阶段筛选" 字号 26px，颜色 #58a6ff。

[0.5s] 画面中央出现两阶段筛选动画，总宽占画布 90%：

阶段 1 "粗筛 (Coarse Stage)"，持续到 [3.5s]：
  背景是继承 B08 的 262K 矩阵（缩小版，宽 500px，高 260px）。
  
  [1s] 横轴 Path 维度被独立扫描：一个轻量 MLP 图标沿横轴滑动，逐行打分。Top-K 行高亮为蓝色（#58a6ff），标注 "Top-K Paths 选中"。
  
  [1.8s] 纵轴 Velocity 维度被独立扫描：MLP 图标沿纵轴滑动打分。Top-K 列高亮为绿色（#3fb950），标注 "Top-K Velocities 选中"。
  
  [2.5s] 高亮的行和列交叉，矩阵中出现 K×K 个交叉格子，同时高亮（蓝绿混色 = 青色），其余格子变暗。标注 "交叉区域 = K² 条组合轨迹 → 进入精选"。

→ 过渡箭头 →

阶段 2 "精选 (Fine Stage)"，从 [3.5s] 开始：
  右侧大矩形（宽 45%，高 300px，圆角 16px，背景 #161b22，边框 2px solid #3fb950）：
  标题 "Fine Scoring" 字号 28px，颜色 #3fb950
  内部展示 K² 条轨迹（以卡片形式排列），卡片数量约 36-100 张（取决于 K 值）。
  
  [4s] "Trajectory Re-Conditioning" 标注出现：所有卡片被送入一个网络，进行路径和速度的联合时空推理。
  
  [4.5s] 卡片依次被评分，分数数字弹出。最优卡片高亮为金色（#d29922），放大弹出到画面中央。标注 "最优轨迹 ✓"

[5.5s] 底部总结条："262,144 → 粗筛 Top-K² (~100) → 精排 → 1 条最优轨迹"，字号 26px，颜色 #e6edf3。

--- narration ---
26 万条不可能全部精细评分，用两阶段策略
粗筛阶段，两个轻量 MLP 分别对 1024 条路径和 256 种速度独立打分
各选 Top-K，计算量是 O(1280) 不是 O(262K)
精选阶段，Top-K 路径和速度两两组合成 K² 条完整轨迹
通过 Trajectory Re-Conditioning 做时空联合推理
逐条精细评分，选出最高分轨迹
262K → 粗筛到约 100 条 → 精排到 1 条
整个过程高效、稳定、可微


>>> Spatial-Temporal Interactions #B10
@enter: fade
@exit: fade
@visual: animation

--- visual ---
深色背景 (#0d1117)，内容区域占画布 88% 宽度。
[0s] 顶部居中标题 "Spatial-Temporal Interactions"，字号 48px，粗体，白色，距顶 65px。副标题 "Ego 也是一个 Agent" 字号 26px，颜色 #3fb950。

[0.5s] 画面中央出现三种交互类型，纵向排列，间距 28px，总宽占画布 82%：

交互 1 [0.5s] "Agent-Temporal Cross-Attention" (#58a6ff)：
  图标：Agent 的现在帧和过去 3 帧用虚线连接
  说明 "每个 Agent 关注自己 H=3 帧历史" 字号 24px

交互 2 [1.3s] "Agent-Agent Self-Attention" (#3fb950)：
  图标：3 个 Agent 互相连线
  说明 "所有 Agent（含 Ego）之间交互" 字号 24px

交互 3 [2.1s] "Agent-Map Cross-Attention" (#f0883e)：
  图标：Agent 和 Map 折线之间连线
  说明 "Agent 与地图元素交互" 字号 24px

[3.5s] 底部高亮核心设计："Ego Vehicle 被当作普通 Agent 实例参与所有交互。规划和预测本质是同一个任务的不同实例。"，字号 24px，颜色 #3fb950，背景 #161b22，圆角 8px。

--- narration ---
感知和规划之间通过三种 Attention 连接
Agent-Temporal 关注自己的历史，Agent-Agent 各车交互，Agent-Map 与地图交互
最关键的设计是 Ego Vehicle 被当作一个普通 Agent
用同样的机制参与所有交互
规划和预测本质上是同一个任务


>>> 模型驾驶实测 #B11
@enter: fade
@exit: fade
@visual: video(./assets/model_driving_topdown.mp4)

--- visual ---
SparseDriveV2 在 CARLA 中的闭环驾驶实测，鸟瞰视角。Ego 车（蓝色）在右车道行驶，NPC（红色）从左侧切入。SparseDriveV2 检测到切入车辆后，通过 Coarse-to-Fine Scoring 选出减速让行的轨迹，Pure Pursuit 执行控制。完整展示了从 6 相机 → 感知 → 262K 候选打分 → 最优轨迹 → 控制的端到端链路。

--- narration ---
来看 SparseDriveV2 在 CARLA 中的实际驾驶表现
注意 NPC 从左侧切入时
模型的 6 相机输入检测到这一变化
感知模块更新了 NPC 的位置和速度
Scoring-Based Planner 在 26 万候选中选出减速让行的轨迹
Pure Pursuit 执行刹车
整个链路在 50ms 内完成，车平稳减速
这就是从像素到控制的完整端到端


>>> Scaling Law 与性能 #B12
@enter: fade
@exit: fade
@visual: animation

--- visual ---
深色背景 (#0d1117)，内容区域占画布 90% 宽度。
[0s] 顶部居中标题 "Scaling Law & 性能"，字号 52px，粗体，白色，距顶 60px。

[0.5s] 画面分为左右两栏，总宽占画布 88%，间距 40px：

左栏 "密度 Scaling"，宽 45%：
  一个折线图（背景 #161b22，圆角 8px，内边距 16px）：
  X 轴 "密度 1× → 32×"，Y 轴 "PDMS 88→92"
  折线持续上升，无饱和趋势
  标注 "候选越密，性能越好 · 未见饱和" 字号 20px，颜色 #3fb950

右栏 "关键性能数字"，宽 45%：
  纵向排列的指标卡片，行间距 20px：
  卡片 1 "NAVSIM PDMS: 92.0" 字号 24px，颜色 #3fb950
  卡片 2 "NAVSIM EPDMS: 90.1 (领先 4.6)" 字号 24px，颜色 #3fb950
  卡片 3 "Bench2Drive DS: 89.15" 字号 24px，颜色 #3fb950
  卡片 4 "Bench2Drive SR: 70.00%" 字号 24px，颜色 #3fb950

[4s] 底部精简对比条："vs UniAD: 训练 144h→20h · 推理 1.8→9 FPS · Backbone R101→R34"

--- narration ---
SparseDriveV2 发现轨迹密度和性能之间存在 Scaling Law
候选从 1× 密到 32×，性能一直涨，没有饱和
在 NAVSIM 开环评测中 PDMS 92.0、EPDMS 90.1
Bench2Drive 闭环 DS 89.15、SR 70%，都是目前最好
对比 UniAD，训练快 7 倍，推理快 5 倍，backbone 更轻
Scoring + Sparse 范式的效率优势是全方位的
