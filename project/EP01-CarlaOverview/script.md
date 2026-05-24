>>> 开场 #B01
@enter: fade-up
@exit: fade
@visual: animation

--- visual ---
全屏深色背景 (#0d1117)。画面垂直居中布局，内容占画布 85% 宽度。
[0s] 顶部出现系列标签 "CARLA × SparseDriveV2 仿真教程"，字号 28px，颜色 #8b949e，字母间距 4px。
[0.3s] 主标题 "EP01: CARLA 仿真器全景" 淡入，白色 (#e6edf3)，粗体，字号 96px，居中，标签下方 40px。
[0.8s] 主标题正下方 20px 处出现一条 4px 粗的 accent 色 (#58a6ff) 横线，从中心向两侧扫出，最终宽度 400px。
[1.2s] 横线下方 40px 出现副标题 "我们要在 CARLA 里跑一个端到端自动驾驶 Agent"，字号 34px，颜色 #8b949e。
[2s] 画面右下角淡入一辆简化 Ego 车图标（俯视视角，白色线条勾勒，20×36px），旁边标注 "Ego Vehicle" 字号 18px，颜色 #58a6ff。这辆车将作为贯穿全系列的视觉锚点。

--- narration ---
大家好，欢迎来到 **CARLA × SparseDriveV2** 仿真教程系列
这个系列的最终目标是
在 CARLA 仿真器里跑通一个 SparseDriveV2 自动驾驶 Agent
并用 Bench2Drive 闭环考试来验证它能不能安全开车
这是第一集，我们从 CARLA 的基础架构开始


>>> 为什么需要仿真 #B02
@enter: fade-up
@exit: fade
@visual: animation

--- visual ---
深色背景 (#0d1117)，内容区域占画布 90% 宽度，垂直居中。
[0s] 顶部居中标题 "为什么需要仿真？"，字号 64px，粗体，白色 (#e6edf3)，距顶 80px。
[0.5s] 标题下方 60px 出现左右两栏对比布局，总宽占画布 88%，两栏间距 48px：
左栏标题 "真实路测"，字号 36px，颜色 #f85149（红色），下方依次淡入三个条目（间隔 0.4s），每条目前有红色圆点：
  - "成本极高：一辆测试车百万级投入" 字号 28px
  - "安全风险：无法测试极端场景" 字号 28px
  - "不可复现：每次路况都不同" 字号 28px
右栏标题 "仿真测试"，字号 36px，颜色 #3fb950（绿色），下方依次淡入三个条目（间隔 0.4s），每条目前有绿色圆点：
  - "零成本：无限虚拟里程" 字号 28px
  - "零风险：随意制造危险场景" 字号 28px
  - "可复现：完全确定性回放" 字号 28px
[4s] 两栏之间的分隔线（竖线，2px，颜色 #30363d）从上向下生长。
画面右下角淡入 Ego 车图标（白色线条，小尺寸），它将在后续每集出现，代表"我们要搭的车"。

--- narration ---
为什么自动驾驶研发离不开仿真？
真实路测成本极高，一辆测试车就是百万级投入
而且很多极端场景，比如行人突然冲出
在现实中根本无法安全地、可重复地测试
仿真器零成本、零风险，每次实验条件完全一致
这正是我们这个系列要做的事
用仿真器训练和验证自动驾驶算法


>>> CARLA 是什么 #B03
@enter: fade
@exit: fade
@visual: animation

--- visual ---
深色背景 (#0d1117)，内容区域占画布 88% 宽度。
[0s] 顶部居中标题 "CARLA — Car Learning to Act"，字号 64px，粗体，白色 (#e6edf3)，距顶 80px。
[0.5s] 标题下方 16px 出现副标题 "开源 · 高保真 · 城市驾驶仿真器"，字号 32px，颜色 #58a6ff。
[1s] 下方 60px 出现时间线布局，水平排列，总宽占画布 85%：
  一条水平线（2px，颜色 #30363d），线上有三个关键节点（精简为最具代表性的里程碑）：
  节点 1: "2017" / "CoRL 论文发表 · 开源"，淡入于 [1s]
  节点 2: "2019" / "Leaderboard 上线 · 标准化评测"，淡入于 [2s]
  节点 3: "2024" / "UE5 迁移 · 进入次世代"，淡入于 [3s]
每个节点是一个圆点（12px，accent 色）+ 上方年份（字号 28px 粗体）+ 下方事件（字号 22px #8b949e）。
[4s] 时间线下方 60px 出现一行标签横排，间距 24px，每个标签圆角 8px，背景 #161b22，内边距 12px 24px：
  "Unreal Engine" / "OpenDRIVE" / "Python API" / "传感器仿真" / "Traffic Manager"
  标签文字字号 24px，颜色 #e6edf3。

--- narration ---
**CARLA** 全称 Car Learning to Act
2017 年由巴塞罗那计算机视觉中心和 Intel Labs 联合推出
是目前学术界最主流的开源自动驾驶仿真器
它基于 **Unreal Engine** 构建，2024 年已迁移到 UE5
提供高保真渲染、物理仿真和完整的 Python API
我们的 SparseDriveV2 Agent 就是在这个世界里开车


>>> Client-Server 架构 #B04
@enter: fade-up
@exit: fade
@visual: animation

--- visual ---
深色背景 (#0d1117)，内容区域占画布 90% 宽度。
[0s] 顶部居中标题 "Client-Server 架构"，字号 64px，粗体，白色，距顶 80px。
[0.5s] 画面中央出现架构图，分为左右两大块，总宽占画布 85%：

左侧大方块 "Server (Unreal Engine)"，宽 420px，高 320px，圆角 16px，背景 #161b22，边框 2px solid #58a6ff：
  内部分三层，每层间距 12px，内边距 24px：
  - 顶层：图标 + "渲染引擎" 字号 28px
  - 中层：图标 + "物理模拟" 字号 28px
  - 底层：图标 + "场景管理" 字号 28px

右侧纵向排列两个方块：
  上方 "SparseDriveV2 Agent"，宽 360px 高 140px，圆角 16px，背景 #161b22，边框 2px solid #3fb950：
    内部：图标 + "6 相机输入 → 轨迹输出" 字号 26px
    底部标注 "我们的主角" 字号 20px，颜色 #3fb950
  下方 "数据记录 / 可视化"，宽 360px 高 100px，圆角 16px，背景 #161b22，边框 1px solid #30363d

两大块之间用两条带箭头的连线连接（颜色 #58a6ff，线宽 2px）：
  上方连线标注 "RPC (指令：spawn / tick / control)" 字号 20px
  下方连线标注 "TCP Stream (传感器数据：6 相机图像)" 字号 20px

各元素依次淡入：[0.5s] Server → [1.5s] 连线 → [2.5s] Agent → [3s] 数据记录

--- narration ---
CARLA 采用经典的 **Client-Server** 架构
Server 端运行 Unreal Engine，负责渲染和物理模拟
Client 端就是我们要跑的自动驾驶算法
两者之间有两条通信通道
**RPC** 通道发送同步指令，比如生成车辆、发送控制
**TCP Streaming** 通道持续接收传感器数据
在我们的场景里，就是 6 个相机的实时图像流


>>> 核心概念：World 与 Blueprint #B05
@enter: fade
@exit: fade
@visual: animation

--- visual ---
深色背景 (#0d1117)，内容区域占画布 88% 宽度。
[0s] 顶部居中标题 "核心概念"，字号 64px，粗体，白色，距顶 80px。
[0.5s] 下方出现两个卡片横向排列，间距 48px，总宽占画布 85%：

左卡片 "World"，宽度占 45%，高 360px，圆角 16px，背景 #161b22，边框 1px solid #30363d，内边距 32px：
  标题 "carla.World" 字号 40px，粗体，颜色 #58a6ff，等宽字体
  下方 24px 分隔线（1px，#30363d）
  下方列表，字号 26px，颜色 #e6edf3，行间距 36px：
  - "获取地图 get_map()"
  - "生成 Actor spawn_actor()"
  - "设置天气 set_weather()"
  - "管理仿真 apply_settings()"

右卡片 "Blueprint Library"，宽度占 45%，高 360px，同样样式：
  标题 "BlueprintLibrary" 字号 40px，粗体，颜色 #58a6ff，等宽字体
  下方 24px 分隔线
  下方列表，字号 26px，行间距 36px：
  - "vehicle.tesla.model3"
  - "sensor.camera.rgb"
  - "walker.pedestrian.0001"
  - "filter('vehicle.*')"

两个卡片依次淡入：[0.5s] 左卡片 → [1.5s] 右卡片。
[3s] 两卡片之间出现一个向右箭头，颜色 #58a6ff，标注 "选模板 → 生成实体" 字号 24px。

--- narration ---
CARLA 的核心入口是 **World** 对象
它代表整个仿真世界
提供生成车辆、获取地图、设置天气等所有操作
要创建任何东西，需要先从 **Blueprint Library** 选模板
每种车辆、传感器、行人都有唯一的 ID
选好 Blueprint 之后，调用 spawn 方法就能在仿真世界里生成实体


>>> Actor 体系 #B06
@enter: fade-up
@exit: fade
@visual: animation

--- visual ---
深色背景 (#0d1117)，内容区域占画布 90% 宽度。
[0s] 顶部居中标题 "Actor 体系"，字号 64px，粗体，白色，距顶 80px。
[0.5s] 下方出现树形层级图，居中，总宽占画布 80%：
根节点 "Actor" 圆角矩形，背景 #58a6ff，文字白色，字号 36px，宽 200px 高 56px。

根节点下方三条分支线（2px，#30363d）连接三个子节点（[1s] 依次淡入，间隔 0.3s）：

子节点 1 "Vehicle"，背景 #161b22，边框 2px solid #f0883e，字号 30px，宽 260px 高 48px
  下方子项（字号 24px，颜色 #8b949e，行间距 28px）：
  "Ego Vehicle (hero 标签)  ← 我们的主车"
  "NPC 车辆"
  "apply_control() / set_autopilot()"

子节点 2 "Sensor"，背景 #161b22，边框 2px solid #3fb950，字号 30px
  下方子项：
  "attach_to 父 Actor"
  "listen(callback) 接收数据"
  "Camera / LiDAR / RADAR / IMU..."

子节点 3 "Walker"，背景 #161b22，边框 2px solid #a371f7，字号 30px
  下方子项：
  "行人 + AI Controller"
  "骨骼控制 (WalkerBoneControl)"
  "自主导航到随机位置"

[4s] 底部出现补充说明条："Traffic Light / Traffic Sign — 地图自动生成，不可手动 spawn"，字号 22px，颜色 #8b949e，背景 #161b22，圆角 8px，内边距 12px 24px。

--- narration ---
CARLA 中所有实体统称 **Actor**，分为三大类
**Vehicle** 是最核心的，其中标记为 hero 的叫 Ego Vehicle
这就是我们要用 SparseDriveV2 控制的主车
**Sensor** 必须附着在 Actor 上，通过 listen 回调接收数据
**Walker** 是行人，可以自主行走
这个 Actor 体系就是构建整个仿真场景的基础


>>> 地图系统 #B07
@enter: fade
@exit: fade
@visual: animation

--- visual ---
深色背景 (#0d1117)，内容区域占画布 88% 宽度。
[0s] 顶部居中标题 "地图系统"，字号 64px，粗体，白色，距顶 70px。
[0.5s] 画面中央出现 3 张代表性地图卡片，横向排列，总宽占画布 80%，间距 40px：
  卡片 1 "Town03"，宽 33%，高 200px，圆角 16px，背景 #161b22，边框 1px solid #30363d，内边距 24px：
    标题字号 32px，颜色 #58a6ff，粗体
    下方 "最复杂的标准城市 · 环岛 · 隧道 · 高低差" 字号 22px，颜色 #8b949e
    底部小字 "Bench2Drive 常用地图" 字号 18px，颜色 #3fb950
  卡片 2 "Town05"，同尺寸：
    标题字号 32px，颜色 #58a6ff
    下方 "方格路网 · 多车道交叉口" 字号 22px，颜色 #8b949e
  卡片 3 "Town12"，同尺寸：
    标题字号 32px，颜色 #58a6ff
    下方 "超大地图 10×10km · 高速 + 城区" 字号 22px，颜色 #8b949e
三张卡片依次淡入，间隔 0.3s。
[3.5s] 卡片下方 40px 出现地图构成公式："3D 模型 (Unreal)  +  OpenDRIVE (.xodr 道路定义)"，字号 26px，颜色 #e6edf3，背景 #161b22，圆角 8px，内边距 12px 24px，居中。元素间用 accent 色 "+" 连接。
[4.5s] 下方补充一句："CARLA 内置 10+ 张地图，覆盖小镇到超大城市"，字号 22px，颜色 #8b949e。

--- narration ---
CARLA 内置了十多张不同风格的地图
从复杂城市 Town03 的环岛和隧道
到 10×10 公里的超大地图 Town12
Bench2Drive 的闭环考试就是在这些地图上进行的
每张地图由 3D 模型和 OpenDRIVE 道路定义两部分组成
地图选择决定了 Agent 要面对什么样的驾驶场景


>>> 最小 CARLA 实验 #B08
@enter: fade-up
@exit: fade
@visual: animation

--- visual ---
深色背景 (#0d1117)，内容区域占画布 90% 宽度。
[0s] 顶部居中标题 "最小 CARLA 实验"，字号 56px，粗体，白色，距顶 60px。副标题 "从零到车在仿真里跑起来" 字号 28px，颜色 #58a6ff。

[0.5s] 画面分为左右两栏，总宽占画布 92%，间距 32px：

左栏 "Python 代码"，宽度 52%：
  代码块，背景 #161b22，圆角 12px，内边距 20px，等宽字体，字号 24px，语法高亮：
  ```python
  import carla
  # 1. 连接 Server
  client = carla.Client('localhost', 2000)
  world = client.get_world()
  # 2. 设置同步模式
  settings = world.get_settings()
  settings.synchronous_mode = True
  settings.fixed_delta_seconds = 0.05
  world.apply_settings(settings)
  # 3. 生成 Ego Vehicle
  bp = world.get_blueprint_library()
  ego_bp = bp.find('vehicle.tesla.model3')
  spawn = world.get_map().get_spawn_points()[0]
  ego = world.spawn_actor(ego_bp, spawn)
  # 4. 主循环
  while True:
      world.tick()
      ego.apply_control(
          carla.VehicleControl(throttle=0.5))
  ```
  关键字色 #ff7b72，字符串色 #a5d6ff，注释色 #8b949e。
  代码分四段，每段对应一个注释编号，依次高亮（间隔 0.8s）。

右栏 "仿真画面"，宽度 42%：
  对应左侧代码段的四个阶段，分别展示 CARLA 渲染效果（用文字描述示意，宽度占满右栏，每阶段高 80px，背景 #0d1117，边框 1px #30363d，圆角 8px，内边距 12px）：
  [0.5s] 阶段 1："① 连接成功 → CARLA 窗口出现在屏幕上"，字号 20px，颜色 #3fb950
  [1.3s] 阶段 2："② 同步模式激活 → 仿真等待 tick 指令"，字号 20px，颜色 #3fb950
  [2.1s] 阶段 3："③ Ego Vehicle 出现在地图上，俯视视角看到一辆车停在路面上"，字号 20px，颜色 #3fb950
  [2.9s] 阶段 4："④ server tick → Ego 车开始向前行驶"，字号 20px，颜色 #3fb950
  [3.7s] 阶段 4 补充：右下角显示 Ego 车图标在俯视地图上缓速移动的示意动画

[5s] 底部出现关键信息条："这 15 行代码就是所有 CARLA 实验的骨架。后面每集都在不断完善这个循环。"，字号 24px，颜色 #e6edf3，背景 #58a6ff，圆角 8px，内边距 12px 24px，文字颜色 #0d1117。

--- narration ---
来看一个最小 CARLA 实验的完整代码
只有 15 行
连接 Server，设置同步模式，选一辆 Tesla Model 3 作为 Ego Vehicle
然后进入主循环，每次 tick 走一步，给一点油门让车前进
这 15 行代码就是所有 CARLA 实验的骨架
后面每集我们都在不断完善这个循环
最后这个循环里会跑 SparseDriveV2 的完整推理


>>> 本集总结 #B09
@enter: fade-up
@exit: fade
@visual: animation

--- visual ---
全屏深色背景 (#0d1117)。画面垂直居中布局，内容占画布 85% 宽度。
[0s] 顶部标题 "EP01 小结 · 下一步"，字号 56px，粗体，白色，距顶 100px。
[0.5s] 下方 50px 出现四个关键要点，纵向排列，行间距 44px，每行左侧有 accent 色竖条（4px 宽，28px 高）：
  "CARLA = Unreal Engine 仿真器，Client-Server 架构" 字号 30px
  "Actor 体系：Vehicle（Ego 主车）/ Sensor / Walker" 字号 30px
  "15 行代码 = 最小实验骨架" 字号 30px
  "我们的主线：在 CARLA 里跑 SparseDriveV2 → Bench2Drive 考试" 字号 30px，颜色 #58a6ff
依次从左侧滑入（间隔 0.3s）。
[3.5s] 要点下方出现 Ego 车图标（白色线条）+ 向右箭头 + 相机图标（#58a6ff），标注 "下一步：给车装上传感器"。
[4.5s] 底部出现下集预告："下一集：CARLA 传感器与数据采集 — 给 Ego 装上六只眼睛"，字号 28px，颜色 #58a6ff。

--- narration ---
来回顾这一集
CARLA 是开源的 Unreal Engine 仿真器，采用 Client-Server 架构
所有实体都是 Actor，Ego Vehicle 是我们的主车
15 行代码就能让一辆车在仿真里跑起来
记住我们的主线 —— 要在 CARLA 里跑 SparseDriveV2
用 Bench2Drive 考试验证
下一集，我们给这辆 Ego 车装上传感器
看看 CARLA 如何模拟自动驾驶的感知硬件
