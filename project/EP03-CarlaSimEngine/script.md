>>> 开场 #B01
@enter: fade-up
@exit: fade
@visual: animation

--- visual ---
全屏深色背景 (#0d1117)。画面垂直居中布局，内容占画布 85% 宽度：
[0s] 顶部出现系列标签 "CARLA × SparseDriveV2 仿真教程"，字号 28px，颜色 #8b949e。
[0.3s] 主标题 "EP03: 仿真引擎与 API" 淡入，白色 (#e6edf3)，粗体，字号 88px，居中。
[0.8s] accent 色横线从中心向两侧扫出。
[1.2s] 副标题 "让 tick 循环跑起来，把数据喂给算法"，字号 34px，颜色 #8b949e。
[1.8s] 左下角延续 EP02：Ego 车图标 + 6 相机图标（已安装 ✓）。右侧出现一个新图标：循环箭头（#58a6ff），标注 "本集：同步控制循环"。

--- narration ---
欢迎来到第三集
前两集我们创建了 Ego 车、装上了传感器
这集我们解决一个问题 —— 让整个系统有节奏地运转起来
CARLA 的同步模式、Traffic Manager 和 Python API
是实际跑实验时最核心的知识


>>> 异步 vs 同步模式 #B02
@enter: fade-up
@exit: fade
@visual: animation

--- visual ---
深色背景 (#0d1117)，内容区域占画布 90% 宽度。
[0s] 顶部居中标题 "异步 vs 同步模式"，字号 64px，粗体，白色，距顶 80px。

[0.5s] 下方出现左右两栏对比，总宽占画布 88%，间距 48px：

左栏 "异步模式 (默认)"，宽度 45%：
  标题字号 36px，颜色 #f0883e
  分隔线
  时序图：两条水平轨道 "Server" (#58a6ff) 和 "Client" (#3fb950)
    Server 轨道上等间距排列小方块（表示 tick），间距不均匀
    Client 轨道上的方块与 Server 不对齐
  下方说明（字号 24px）：
  "Server 全速跑，Client 随时读"
  "时间步不固定，不保证确定性"

右栏 "同步模式 (推荐)"，宽度 45%：
  标题字号 36px，颜色 #3fb950
  时序图：Server 和 Client 方块严格一一对齐
  Client 向 Server 发 "tick()" 箭头，Server 收到后才走一步
  下方说明：
  "Client 每 tick 推一步"
  "固定时间步，完全确定性"

[4s] 底部出现强调条："研究实验 + 算法训练 → 同步模式是唯一选择"，字号 26px，颜色 #0d1117，背景 #58a6ff，圆角 8px，内边距 12px 24px。

--- narration ---
CARLA 有两种运行模式
异步模式下 Server 全速运行，Client 随时读取
时间步不固定，每次跑都可能不同
**同步模式**才是做研究的正确选择
Client 每调用一次 tick，Server 才走一步
配合固定时间步，整个仿真完全确定性可复现
算法训练和 Bench2Drive 评测都必须用同步模式


>>> 固定时间步 #B03
@enter: fade
@exit: fade
@visual: animation

--- visual ---
深色背景 (#0d1117)，内容区域占画布 88% 宽度。
[0s] 顶部居中标题 "固定时间步与 Sub-Stepping"，字号 56px，粗体，白色，距顶 80px。

[0.5s] 画面中央出现代码块，宽度占画布 70%，背景 #161b22，圆角 12px，内边距 24px：
```
settings = world.get_settings()
settings.synchronous_mode = True
settings.fixed_delta_seconds = 0.05
world.apply_settings(settings)
```
等宽字体，字号 28px，关键字高亮 (#ff7b72)，数字高亮 (#58a6ff)。

[2s] 代码块右侧出现时间轴示意：一条水平线，每 0.05s 一个标记（小圆点），标注 "20 ticks / 秒"。

[3s] 下方出现 Sub-Stepping 示意：每个 tick 内部再被切分成多个子步。一个 tick 矩形（宽 120px）内部用虚线分割为 5 个子步，标注 "物理子步 ≥ 60Hz → 每个子步 ≤ 0.01666s"，字号 22px，颜色 #8b949e。

--- narration ---
设置同步模式只需要四行代码
fixed_delta_seconds 设为 0.05 秒
意味着仿真以 20Hz 的频率推进
物理引擎会在每个 tick 内部做 Sub-Stepping
把大步细分成多个子步来保证碰撞检测精度
子步频率建议不低于 60Hz


>>> Traffic Manager：NPC 的大脑 #B04
@enter: fade-up
@exit: fade
@visual: animation

--- visual ---
深色背景 (#0d1117)，内容区域占画布 92% 宽度。
[0s] 顶部居中标题 "Traffic Manager"，字号 56px，粗体，白色，距顶 60px。副标题 "NPC 车辆的五阶段决策流水线" 字号 26px，颜色 #58a6ff。

[0.5s] 画面分为上下两部分：

上半部 "五阶段流水线"，五个阶段横排，总宽占画布 90%，每个阶段宽 170px，高 100px，圆角 12px，背景 #161b22：
  "① ALSM" (#58a6ff 边框) → "② 定位" (#3fb950) → "③ 碰撞检测" (#f0883e) → "④ 交通灯" (#a371f7) → "⑤ PID 控制" (#d29922)
  下方标注：扫描世界状态 → 规划路径 → 轨迹冲突 → 红绿灯 → 输出油门刹车
各阶段依次从左侧滑入，间隔 0.25s。

下半部 "场景效果"，一个俯视路口示意，总宽占画布 70%，高 120px，背景 #0d1117，边框 1px #30363d，圆角 8px：
[2.5s] Ego 车前方有车切入（红色箭头标注）
[3s] 路口有横向来车（橙色标注）
[3.5s] 行人过马路（紫色标注）
标注 "Traffic Manager 负责所有 NPC 行为，制造丰富的交互场景" 字号 20px，颜色 #8b949e

--- narration ---
**Traffic Manager** 运行在 Client 端，控制所有 NPC 车辆
它的内部是一条五阶段流水线
先扫描世界状态，再规划每辆车的路径
检测轨迹冲突，处理红绿灯
最后用 PID 控制器输出油门和转向
它能为 Ego 车制造各种交互场景
前车切入、横向来车、行人过马路
这些正是 Bench2Drive 要考察的场景


>>> Traffic Manager 配置 #B05
@enter: fade
@exit: fade
@visual: animation

--- visual ---
深色背景 (#0d1117)，内容区域占画布 88% 宽度。
[0s] 顶部居中标题 "Traffic Manager 配置"，字号 52px，粗体，白色，距顶 80px。

[0.5s] 画面中央出现代码 + 注解并排布局，总宽占画布 85%：

左半代码块，宽 55%，背景 #161b22，圆角 12px，内边距 20px，等宽字体，字号 24px：
```
tm = client.get_trafficmanager(8000)
tm.set_synchronous_mode(True)

tm.distance_to_leading_vehicle(v, 5.0)
tm.vehicle_percentage_speed_difference(v, -20)
tm.ignore_lights_percentage(v, 50)
tm.auto_lane_change(v, True)
```

右半注解面板，宽 38%，背景半透明 #161b22cc，圆角 8px，内边距 16px，字号 22px，间距 24px：
  "5.0 → 跟车距离 5 米"
  "-20 → 比限速快 20%"
  "50 → 50% 闯红灯率"
  "True → 允许自动变道"

--- narration ---
Traffic Manager 可以全局设定，也可以对单辆车精确调参
跟车距离、超速比例、闯红灯概率、变道策略
全都可配
这让你能构造从温和到激进的各种驾驶场景
对测试算法的鲁棒性非常有用


>>> 天气与光照 #B06
@enter: fade
@exit: fade
@visual: animation

--- visual ---
深色背景 (#0d1117)，内容区域占画布 88% 宽度。
[0s] 顶部居中标题 "天气与光照系统"，字号 56px，粗体，白色，距顶 80px。

[0.5s] 画面中央出现 6 个天气卡片（2×3 网格），总宽占画布 82%，间距 20px：
  每个卡片宽 220px，高 100px，圆角 12px，不同背景色模拟天气：
  "ClearNoon" 渐变 #1a3a5c→#2d5a8e
  "HardRain" 暗色 #1a2332 + 雨线纹理
  "ClearNight" 深色 #0a0e14
  "Foggy" 灰色 #3a3a3a
  "ClearSunset" 暖色渐变 #4a2020→#8a4020
  "DustStorm" 沙色 #5a4a30
每张卡片标注天气名（字号 22px），依次淡入（间隔 0.12s）。

[3s] 网格下方出现关键标注："天气仅影响视觉和传感器数据 —— 不影响车辆物理（无打滑效果）"，字号 24px，颜色 #d29922，背景 #161b22，圆角 8px，内边距 10px 20px。

--- narration ---
CARLA 内置 23 种天气预设，覆盖晴雨雾夜沙尘暴
天气参数可以实时通过 API 调整
重要细节：天气变化只影响视觉和传感器
不会改变车辆的物理行为，雨天不会打滑
Bench2Drive 会在不同天气条件下评测
这对算法的鲁棒性是一个挑战


>>> Python API：连接与创建 #B07
@enter: fade-up
@exit: fade
@visual: animation

--- visual ---
深色背景 (#0d1117)，内容区域占画布 88% 宽度。
[0s] 顶部居中标题 "Python API — 连接与创建"，字号 56px，粗体，白色，距顶 70px。

[0.5s] 画面中央出现代码块，宽度占画布 78%，背景 #161b22，圆角 12px，内边距 24px：
等宽字体，字号 26px，语法高亮：
```python
import carla

# 1. 连接 Server
client = carla.Client('localhost', 2000)
client.set_timeout(10.0)
world = client.get_world()

# 2. 同步模式
settings = world.get_settings()
settings.synchronous_mode = True
settings.fixed_delta_seconds = 0.05
world.apply_settings(settings)

# 3. 生成 Ego Vehicle
bp_lib = world.get_blueprint_library()
ego_bp = bp_lib.find('vehicle.tesla.model3')
spawn = world.get_map().get_spawn_points()[0]
ego = world.spawn_actor(ego_bp, spawn)
```
代码分三段，对应注释编号，每段依次淡入（间隔 1s）。
关键字 #ff7b72，字符串 #a5d6ff，注释 #8b949e。

--- narration ---
来快速回顾 Python API 的标准开头
连接 Server → 同步模式 → 生成 Ego Vehicle
这是每个 CARLA 实验的前三步
接下来是这一集的关键 —— 传感器 + 主循环


>>> 同步数据闭环：完整的 tick 循环 #B08
@enter: fade
@exit: fade
@visual: animation

--- visual ---
深色背景 (#0d1117)，内容区域占画布 94% 宽度。
[0s] 顶部居中标题 "同步数据闭环"，字号 56px，粗体，白色，距顶 60px。副标题 "每帧都在这个环里运转" 字号 28px，颜色 #58a6ff。

[0.5s] 画面中央出现一个环形流程图，这是本集的核心画面。环上的节点沿圆形轨道排列（圆直径占画布 70%），节点用带箭头的弧线连接：

节点 1（12 点位置）"world.tick()"：
  矩形，宽 180px，高 64px，圆角 12px，背景 #161b22，边框 2px solid #58a6ff，字号 24px，粗体
  [0.5s] 亮起

→ 顺时针弧线箭头 →

节点 2（3 点位置）"Sensor Callback"：
  矩形，同等尺寸，边框 #3fb950
  内部 "6 相机 + 其他传感器采集数据"，字号 20px
  [1.2s] 亮起

→ 弧线箭头 →

节点 3（6 点位置）"Data Align & Queue"：
  矩形，同等尺寸，边框 #f0883e
  内部 "同一 frame_id 对齐 · 按帧组织"，字号 20px
  [1.9s] 亮起

→ 弧线箭头 →

节点 4（9 点位置）"Model Inference"：
  矩形，同等尺寸，边框 #a371f7
  内部 "SparseDriveV2 Forward · 感知 → 规划 → 轨迹"，字号 20px
  [2.6s] 亮起

→ 弧线箭头 →

节点 5（回到上方偏左）"apply_control()"：
  矩形，同等尺寸，边框 #d29922
  内部 "VehicleControl(throttle, steer, brake)"，字号 20px
  [3.3s] 亮起

→ 弧线箭头回到节点 1，闭环

[4s] 环的中心出现标注 "tick 间隔 50ms → 整个环必须在 50ms 内完成 → 推理延迟是硬约束"，字号 22px，颜色 #d29922。

[5s] 环的右侧出现代码片段（透明度 60%，作为参考），展示主循环的 6 行核心代码，等宽字体，字号 20px。

--- narration ---
这是整个系列最重要的图 —— **同步数据闭环**
每一帧都按这个环运转
world.tick 推进仿真一步
传感器回调采集 6 个相机和其他传感器数据
同一帧的数据按 frame ID 对齐、进入队列
然后送入 SparseDriveV2 做一次完整的推理
从感知、建图到规划，输出一条轨迹
最后 apply_control 把油门、转向和刹车发送给 Ego 车
然后进入下一帧
tick 间隔 50 毫秒，整个环必须在这 50 毫秒内完成
推理延迟是硬约束，这也是 Sparse 范式追求效率的原因


>>> 本集总结 #B09
@enter: fade-up
@exit: fade
@visual: animation

--- visual ---
全屏深色背景 (#0d1117)。画面垂直居中布局，内容占画布 85% 宽度：
[0s] 顶部标题 "EP03 小结 · 搭建完成"，字号 56px，粗体，白色，距顶 80px。
[0.5s] 画面中央出现一条水平进度条（宽 80%，高 8px，背景 #30363d，圆角 4px），进度条填充到约 50%（accent 色 #58a6ff），标注 "仿真环境搭建完成 ✓" 字号 24px。
下方纵向排列已完成的能力清单，行间距 36px：
  "✓ Ego Vehicle — 创建、控制" 字号 28px，颜色 #3fb950
  "✓ 传感器系统 — 6 相机 + 辅助传感器" 字号 28px，颜色 #3fb950
  "✓ 同步控制循环 — tick → callback → queue → control" 字号 28px，颜色 #3fb950
  "○ 算法模块 — 下一阶段" 字号 28px，颜色 #8b949e

[3.5s] 底部出现桥接文字："仿真环境就绪。接下来把视角转向这个循环的核心 —— Model Inference。"，字号 26px，颜色 #58a6ff。
[4.5s] 下集预告："下一集：端到端自动驾驶范式演进 — 为什么选择 Sparse？"，字号 28px，颜色 #58a6ff。

--- narration ---
三集下来，我们在 CARLA 端的基础搭建已经完成
Ego Vehicle 创建、传感器系统安装、同步控制循环跑通
tick → sensor callback → data queue → model inference → apply_control
这个闭环是后续一切的基础
从下一集开始，我们把视角转向这个环里最关键的那一步
Model Inference 到底在做什么
端到端自动驾驶是怎么从传感器输入走到规划输出的
