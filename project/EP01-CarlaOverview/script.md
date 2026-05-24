>>> 开场 #B01
@enter: fade-up
@exit: fade
@visual: image

--- visual ---
一张 16:9 横构图的扁平化技术风格教程封面图。深色背景纯色 #0d1117，无渐变无噪点。

主体居中布局：
- 顶部偏上一行小字标签 "CARLA × SparseDriveV2 仿真教程"，灰色 #8b949e，无衬线字体，字母间距宽松。
- 标签下方约一行间距处是主标题 "EP01: CARLA 仿真器全景"，白色 #e6edf3，粗体无衬线字体，超大字号（视觉上占画布宽度约 60%），居中。
- 主标题正下方有一条短横线，亮蓝色 #58a6ff，2 px 厚，长度约 240 px，居中。
- 横线下方一行副标题 "我们要在 CARLA 里跑一个端到端自动驾驶 Agent"，中等字号，灰色 #8b949e，居中。

画面右下角是一个小型简约 Ego 车俯视图标，仅用细白线条勾勒（不要写实），下方一行小字标注 "Ego Vehicle"，亮蓝色 #58a6ff。

整体风格：极简、科技感、留白克制、内容占画布 80% 区域、左右上下安全边距均匀。无任何阴影、光晕或装饰元素。文字渲染必须清晰可读，所有引号、冒号、× 符号按字面呈现。

--- narration ---
大家好，欢迎来到 **CARLA × SparseDriveV2** 系列
这个系列的最终目标是
在 CARLA 里跑通一个 SparseDriveV2 自动驾驶 Agent
并用 Bench2Drive 闭环考试验证它能不能安全开车
这是第一集，我们从 CARLA 的基础架构开始


>>> 为什么需要仿真 #B02
@enter: fade-up
@exit: fade
@visual: image

--- visual ---
一张 16:9 横构图的对比信息图，扁平化技术风格。深色背景 #0d1117。

顶部居中标题 "为什么需要仿真？"，白色 #e6edf3 粗体，大字号。

下方是左右两栏对比卡片，两栏总宽占画布 88%，中间用一条灰色细竖线 #30363d 分隔。

左栏标题 "真实路测"，红色 #f85149 粗体；下方三个条目竖排，每条前面有一个红色小圆点：
- 成本极高：一辆测试车百万级投入
- 安全风险：无法测试极端场景
- 不可复现：每次路况都不同

右栏标题 "仿真测试"，绿色 #3fb950 粗体；下方三个条目竖排，每条前面有一个绿色小圆点：
- 零成本：无限虚拟里程
- 零风险：随意制造危险场景
- 完全确定性：每次实验条件一致

条目正文字号一致、灰白色 #c9d1d9，行间距充足。

画面右下角小尺寸 Ego 车线条图标，作为系列视觉锚点。

风格：极简扁平化，文字清晰，无渐变无装饰。

--- narration ---
为什么自动驾驶研发离不开仿真
真实路测成本极高
一辆测试车就是百万级投入
很多极端场景，比如行人突然冲出
在现实里根本无法安全地重复测试
仿真器零成本、零风险
每次实验条件完全一致
这就是仿真要解决的问题


>>> CARLA 是什么 #B03
@enter: fade
@exit: fade
@visual: image

--- visual ---
一张 16:9 横构图的时间线信息图，扁平化技术风格。深色背景 #0d1117。

顶部居中主标题 "CARLA — Car Learning to Act"，白色 #e6edf3 粗体，大字号。
标题下方一行副标题 "开源 · 高保真 · 城市驾驶仿真器"，亮蓝色 #58a6ff，中等字号。

画面中央是一条横向时间线：一条灰色 #30363d 水平细线，线上有三个等距节点，每个节点是一个亮蓝色 #58a6ff 小圆点（直径约 12 px）。

节点从左到右依次标注（每个节点上方写年份粗体白色大字，下方写事件中等字号 #8b949e）：
- 2017｜CoRL 论文发表 · 开源
- 2020｜Autonomous Driving Leaderboard 上线
- 2024｜向 UE5 迁移（CARLA 2.0 分支启动）

时间线下方约一行间距处是一行水平排列的圆角标签胶囊，每个胶囊背景 #161b22，圆角 8 px，内边距充足，文字 #e6edf3 中等字号：
"Unreal Engine"｜"OpenDRIVE"｜"Python API"｜"传感器仿真"｜"Traffic Manager"

总体内容占画布 85% 宽度，居中。无装饰，所有文字按字面准确渲染。

--- narration ---
**CARLA** 全称 Car Learning to Act
2017 年由巴塞罗那计算机视觉中心和 Intel Labs 联合推出
是目前学术界最主流的开源自动驾驶仿真器
它基于 Unreal Engine 构建
2024 年起向 UE5 迁移
提供高保真渲染、物理模拟和完整的 Python API
我们的 SparseDriveV2 Agent 就是在这个世界里开车


>>> Client-Server 架构 #B04
@enter: fade-up
@exit: fade
@visual: image

--- visual ---
一张 16:9 横构图的架构示意图，扁平化技术风格、轴测略带俯视的等距构图（isometric flat）。深色背景 #0d1117。

顶部居中标题 "Client-Server 架构"，白色 #e6edf3 粗体大字。

画面主体是左右两个大方块用两条带箭头的连线连接，整体宽度占画布 85%。

左侧大方块 "Server (Unreal Engine)"，约占画布宽 30%，圆角 16 px，深色背景 #161b22，边框 2 px 亮蓝色 #58a6ff。方块内部纵向三行，行间分隔细线 #30363d：
- 渲染引擎（左侧一个简约图标 + 文字）
- 物理模拟（左侧一个简约图标 + 文字）
- 场景管理（左侧一个简约图标 + 文字）

右侧上下两个方块（同样圆角 16 px、内边距充足）：
- 上方 "SparseDriveV2 Agent"，边框 2 px 绿色 #3fb950。内部一行 "6 相机输入 → 轨迹输出"，底部一行小字 "我们的主角"。
- 下方 "数据记录 / 可视化"，边框 1 px 灰色 #30363d，单行简介。

两大块之间有两条横向连线，亮蓝色 #58a6ff 2 px 粗，每条线中间有一个箭头：
- 上方连线标注 "RPC（指令：spawn / tick / control）"
- 下方连线标注 "TCP Stream（传感器数据：6 相机图像）"

所有文字使用无衬线字体，关键字与图标对齐整齐。整体风格干净、极简、技术感强。

--- narration ---
CARLA 采用经典的 Client-Server 架构
Server 端运行 Unreal Engine，负责渲染和物理模拟
Client 端就是我们要跑的自动驾驶算法
两者之间有两条通信通道
RPC 通道发送同步指令
TCP Streaming 通道持续接收传感器数据
在我们的场景里
就是 6 个相机的实时图像流


>>> 核心概念：World 与 Blueprint #B05
@enter: fade
@exit: fade
@visual: image

--- visual ---
一张 16:9 横构图的双卡片对照图，扁平化技术风格。深色背景 #0d1117。

顶部居中标题 "核心概念"，白色 #e6edf3 粗体大字。

画面中央两张并排卡片，总宽占画布 85%，间距充足。

左卡片 "World"，圆角 16 px，背景 #161b22，1 px 灰边 #30363d，内边距大：
- 顶部一行类名 "carla.World"，亮蓝色 #58a6ff，等宽字体（monospace），粗体大字。
- 下方水平分隔细线 #30363d。
- 再下方竖向四行 API 列表（等宽字体，中等字号，白色 #e6edf3）：
  - get_map()
  - spawn_actor()
  - set_weather()
  - apply_settings()

右卡片 "Blueprint Library"，同样的卡片样式：
- 顶部类名 "BlueprintLibrary"，亮蓝色 #58a6ff，等宽字体粗体。
- 分隔线下方四行示例 ID（等宽字体）：
  - vehicle.tesla.model3
  - sensor.camera.rgb
  - walker.pedestrian.0001
  - filter('vehicle.*')

两卡片之间有一个右指箭头图标，亮蓝色 #58a6ff，箭头下方一行小字 "选模板 → 生成实体"。

整体风格干净极简，文字必须按字面准确渲染（API 名、参数、点号都不能错）。

--- narration ---
CARLA 的核心入口是 World 对象
它代表整个仿真世界
提供生成车辆、获取地图、设置天气等所有操作
要创建任何实体
先从 Blueprint Library 选模板
每种车辆、传感器、行人都有唯一 ID
选好 Blueprint 之后调用 spawn 方法
就能在仿真世界里生成实体


>>> Actor 体系 #B06
@enter: fade-up
@exit: fade
@visual: image

--- visual ---
一张 16:9 横构图的层级树状图，扁平化技术风格。深色背景 #0d1117。

顶部居中标题 "Actor 体系"，白色 #e6edf3 粗体大字。

画面主体是一个三层树形结构，居中布局，总宽占画布 80%。

根节点（顶部居中）：一个亮蓝色 #58a6ff 实心圆角矩形，宽度约 220 px，内部白色粗体文字 "Actor"。

根节点下方三条灰色细连线 #30363d 向下分叉到三个子节点（横向均匀排列）：

子节点 1 "Vehicle"，深色背景 #161b22 圆角矩形，2 px 橙色边 #f0883e。
节点下方紧跟一组简约图标 + 文字（每行一个，灰色 #8b949e 中等字号）：
- Ego Vehicle（hero 标签）← 我们的主车
- NPC 车辆
- apply_control() / set_autopilot()

子节点 2 "Sensor"，同样卡片样式，2 px 绿色边 #3fb950。子项：
- attach_to 父 Actor
- listen(callback) 接收数据
- Camera / LiDAR / RADAR / IMU

子节点 3 "Walker"，同样卡片样式，2 px 紫色边 #a371f7。子项：
- 行人 + AI Controller
- 骨骼控制（WalkerBoneControl）
- 自主导航到随机位置

画面底部居中一个细长胶囊形提示条，深色背景 #161b22，圆角 8 px：
"Traffic Light / Traffic Sign — 由地图自动生成，不可手动 spawn"，灰色文字。

风格干净，所有文字按字面渲染，节点对齐整齐。

--- narration ---
CARLA 中所有实体统称 Actor
分为三大类
Vehicle 是核心
标记为 hero 的就是 Ego Vehicle
也就是我们要用 SparseDriveV2 控制的主车
Sensor 必须附着在 Actor 上
通过 listen 回调接收数据
Walker 是行人，可以自主行走
这个 Actor 体系就是构建整个仿真场景的基础


>>> 地图系统 #B07
@enter: fade
@exit: fade
@visual: image

--- visual ---
一张 16:9 横构图的三卡片信息图，扁平化技术风格。深色背景 #0d1117。

顶部居中标题 "地图系统"，白色 #e6edf3 粗体大字。

画面中央三张横向并排的卡片，总宽占画布 80%，每张卡片宽度均等、间距充足，圆角 16 px、深色背景 #161b22、1 px 灰边 #30363d、内边距大。

每张卡片内部布局相同（自上而下）：
- 顶部地图缩略小图（简约线条风格，俯视示意），灰色调
- 中部地图名字（亮蓝色 #58a6ff 粗体）：Town03 / Town05 / Town12
- 下方一行特色描述（中等字号，灰色 #8b949e）：
  - Town03：最复杂的标准城市 · 环岛 · 隧道 · 高低差
  - Town05：方格路网 · 多车道交叉口
  - Town12：超大地图 10×10 km · 高速 + 城区
- 卡片底部一行小字（仅 Town03 有，绿色 #3fb950）：Bench2Drive 常用地图

三张卡片下方居中一个胶囊形信息条，深色背景 #161b22 圆角 8 px：
"地图 = 3D 模型（Unreal）+ OpenDRIVE（.xodr 道路定义）"，白色中等字号文字。

整体风格极简、信息密度适中、文字清晰。

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
@visual: image

--- visual ---
一张 16:9 横构图的代码 + 步骤说明对照图，扁平化技术风格。深色背景 #0d1117。

顶部居中标题 "最小 CARLA 实验"，白色 #e6edf3 粗体大字；下方一行副标题 "从零到车在仿真里跑起来"，亮蓝色 #58a6ff 中等字号。

画面分为左右两栏：

左栏（占画布宽 55%）是一个 Python 代码块，背景 #161b22 圆角 12 px，等宽字体（monospace），代码语法高亮：
- 关键字 #ff7b72
- 字符串 #a5d6ff
- 注释 #8b949e
- 普通文本 #e6edf3

代码内容（按字面渲染、缩进 4 空格）：

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

右栏（占画布宽 42%）是四个对应步骤的说明，每个说明是一个带亮绿色 ✓ 图标的小卡片，自上而下垂直排列：
- ① 连接成功 → CARLA 窗口出现在屏幕上
- ② 同步模式激活 → 仿真等待 tick 指令
- ③ Ego Vehicle 出现在地图上，俯视看到一辆 Tesla
- ④ tick 推进 → Ego 开始向前行驶

每个说明卡片：深色背景 #161b22 圆角 8 px、绿色 #3fb950 文字、左侧 ✓ 图标对齐。

画面底部居中一条强调横幅（亮蓝色 #58a6ff 实心背景，圆角 8 px，深色文字 #0d1117 粗体）：
"这 25 行代码 = 所有 CARLA 实验的骨架"

所有代码必须按字面准确渲染，包括引号、点号、缩进。无装饰元素。

--- narration ---
来看一个最小 CARLA 实验的完整代码
只有二十几行
连接 Server、设置同步模式
选一辆 Tesla Model 3 作为 Ego Vehicle
然后进入主循环
每次 tick 走一步
给一点油门让车前进
这二十几行代码就是所有 CARLA 实验的骨架
后面每集我们都在不断完善这个循环


>>> 实际运行画面 #B09
@enter: fade-up
@exit: fade
@visual: video(./assets/basic_driving_chase.mp4)

--- visual ---
（本块使用本地视频 ./assets/basic_driving_chase.mp4，无需生成图片）

CARLA 仿真实际运行画面：Ego 车在 Town04 公路上行驶，第三人称跟车视角，
同步模式 20 Hz，每帧由 Client 主动推进。

--- narration ---
这就是刚才那二十几行代码
在 CARLA 里的实际运行画面
一辆 Tesla Model 3 在 Town04 的公路上行驶
同步模式下，每一帧都由 Client 端精确推进
从下一集开始
我们给这辆车装上传感器
让它能"看到"周围的世界


>>> 本集总结 #B10
@enter: fade-up
@exit: fade
@visual: image

--- visual ---
一张 16:9 横构图的小结收尾图，扁平化技术风格。深色背景 #0d1117。

顶部居中标题 "EP01 小结 · 下一步"，白色 #e6edf3 粗体大字。

画面中央竖向排列四条要点，每条左侧有一个亮蓝色 #58a6ff 4 px 宽的短竖条作为视觉前缀。文字白色 #e6edf3 中等字号，行间距充足：

1. CARLA = Unreal Engine 仿真器，Client-Server 架构
2. Actor 体系：Vehicle（Ego 主车）/ Sensor / Walker
3. 二十几行代码 = 最小实验骨架
4. 主线：在 CARLA 里跑 SparseDriveV2 → Bench2Drive 考试  ← 这条用亮蓝色 #58a6ff 文字

要点下方居中是一组转场视觉：左边一个简约 Ego 车线条图标，中间一个亮蓝色右指箭头，右边一个简约相机图标（也是亮蓝色 #58a6ff）。下方一行小字 "下一步：给车装上传感器"。

画面底部居中一行下集预告，亮蓝色 #58a6ff 中等字号：
"下一集：传感器与数据采集 — 给 Ego 装上六只眼睛"

风格干净极简，所有文字清晰可读。

--- narration ---
来回顾这一集
CARLA 是开源的 Unreal Engine 仿真器
采用 Client-Server 架构
所有实体都是 Actor
Ego Vehicle 是我们的主车
二十几行代码就能让一辆车在仿真里跑起来
记住主线
在 CARLA 里跑 SparseDriveV2
用 Bench2Drive 考试验证
下一集我们给这辆 Ego 车装上传感器
看 CARLA 如何模拟自动驾驶的感知硬件
