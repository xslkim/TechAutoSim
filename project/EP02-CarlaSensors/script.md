>>> 开场 #B01
@enter: fade-up
@exit: fade
@visual: animation

--- visual ---
全屏深色背景 (#0d1117)。画面垂直居中布局，内容占画布 85% 宽度。
[0s] 顶部出现系列标签 "CARLA × SparseDriveV2 仿真教程"，字号 28px，颜色 #8b949e。
[0.3s] 主标题 "EP02: 传感器与数据采集" 淡入，白色 (#e6edf3)，粗体，字号 96px，居中。
[0.8s] accent 色横线从中心向两侧扫出，宽度 400px。
[1.2s] 副标题 "给 Ego 车装上眼睛、耳朵和触觉"，字号 36px，颜色 #8b949e。
[1.8s] 画面左下角出现 Ego 车图标（从 EP01 延续），旁边标注 "已创建 ✓" 字号 18px 绿色。然后 6 个相机图标（#58a6ff）依次出现在车周围，标注 "本集任务：安装传感器"。

--- narration ---
欢迎来到第二集
上一集我们创建了 Ego Vehicle，让它能在仿真里跑起来
这集我们给这辆车装上传感器
让它能像真实的自动驾驶汽车一样感知周围环境


>>> 传感器全景 #B02
@enter: fade
@exit: fade
@visual: animation

--- visual ---
深色背景 (#0d1117)，内容区域占画布 92% 宽度。
[0s] 顶部居中标题 "传感器全景"，字号 64px，粗体，白色，距顶 70px。

[0.5s] 画面中央出现一个俯视 Ego 车图标（居中，宽 120px），周围环绕传感器标注：
  车辆前方标注 "6× RGB Camera" (#58a6ff) — 环视覆盖
  车顶标注 "LiDAR" (#3fb950) — 旋转扫描
  车内标注 "IMU + GNSS" (#f0883e) — 定位
  下方分类标签行，间距 16px：
  "相机族" "距离传感器" "定位传感器" "事件检测器"

[1.5s] 车子周围出现三个分类标签组，纵向排列在画面右侧（宽 360px）：
第一行 "相机族" 标签 + "RGB / Depth / Semantic Seg / Instance Seg / DVS / Optical Flow"，字号 20px，颜色 #8b949e
第二行 "距离" 标签 + "LiDAR / Semantic LiDAR / RADAR"
第三行 "定位+事件" 标签 + "GNSS / IMU / Collision / Lane Invasion"

[3s] 底部出现统一工作流标注："所有传感器：spawn(blueprint, transform, attach_to=ego) → listen(callback)"，字号 24px，等宽字体，颜色 #58a6ff。

--- narration ---
CARLA 的传感器分为三大类
相机族种类最丰富，从 RGB 到语义分割共六种
距离传感器包括 LiDAR 和 RADAR
还有 GNSS、IMU 和事件检测器
所有传感器都遵循同一套工作流
创建 Blueprint、挂载到 Ego 车、注册 listen 回调
其中 6 个 RGB 环视相机是 SparseDriveV2 的唯一输入


>>> RGB 相机：算法的眼睛 #B03
@enter: fade-up
@exit: fade
@visual: animation

--- visual ---
深色背景 (#0d1117)，内容区域占画布 92% 宽度。
[0s] 顶部居中标题 "RGB Camera — 算法的眼睛"，字号 56px，粗体，白色，距顶 70px。

[0.5s] 画面主体采用"座舱视角"布局：
中央大区域（宽 65%）显示 Ego 车俯视图，周围 6 个相机用扇形 FOV 标出：
  FRONT (#58a6ff) / FRONT_LEFT (#3fb950) / FRONT_RIGHT (#f0883e)
  BACK (#a371f7) / BACK_LEFT (#d29922) / BACK_RIGHT (#f85149)
6 个扇形合起来覆盖 360°，逐一出现（间隔 0.25s）。

[2s] 俯视图右侧出现关键参数面板（宽 280px，背景 #161b22，圆角 12px，内边距 20px）：
  标题 "sensor.camera.rgb" 字号 22px，等宽字体，颜色 #58a6ff
  "image_size_x: 1920" 字号 20px
  "image_size_y: 1080" 字号 20px
  "fov: 110" 字号 20px
  "sensor_tick: 0.05" 字号 20px

[3.5s] 俯视图下方出现一行小字标注 "SparseDriveV2 纯视觉方案：6 个 RGB 相机 = 全部输入，无 LiDAR"，字号 22px，颜色 #3fb950，背景 #161b22，圆角 8px，内边距 10px 20px。

--- narration ---
**RGB Camera** 是最重要的传感器
SparseDriveV2 的六个环视相机就是这个类型
前方、前左、前右、后方、后左、后右
六个相机完整覆盖车辆周围 360 度
可以配置分辨率、视场角和采样频率
SparseDriveV2 是纯视觉方案
六个 RGB 相机就是全部输入，不需要 LiDAR


>>> 深度与语义分割相机 #B04
@enter: fade
@exit: fade
@visual: animation

--- visual ---
深色背景 (#0d1117)，内容区域占画布 92% 宽度。
[0s] 顶部居中标题 "Depth & Semantic Segmentation"，字号 56px，粗体，白色，距顶 70px。

[0.5s] 画面中央出现一个驾驶场景的示意面板（宽 70%，高 300px，背景 #0d1117，边框 1px #30363d，圆角 12px），内部分为"同一场景，四种视图"的四宫格：

左上格 "RGB 原始"：彩色场景示意（用色块表示道路、车辆、天空）
右上格 "Depth"：从近处亮到远处暗的灰度渐变，标注 "近 → 远，三通道编码距离"
左下格 "Semantic Seg"：伪彩着色，道路紫色、车辆红色、植被绿色、天空白色，标注 "28 个类别"
右下格 "Instance Seg"：同类不同实例不同色调，两辆红色车用不同深浅红区分，标注 "类别 + 实例 ID"

四格依次点亮：[0.5s] RGB → [1s] Depth → [1.5s] Semantic → [2s] Instance。

[3.5s] 画面底部出现标注 "训练阶段使用 · 提供完美像素级 Ground Truth"，字号 24px，颜色 #d29922，背景 #161b22，圆角 8px。

--- narration ---
除了 RGB，CARLA 还提供了深度、语义分割和实例分割相机
**Depth** 输出每个像素到相机的距离
**语义分割**给每个像素打上 28 个类别标签中的一个
**实例分割**在此基础上区分同类的不同个体
这些数据在**训练阶段**非常重要
它们提供了完美的像素级 Ground Truth
用来监督感知模型的训练


>>> LiDAR 与 RADAR #B05
@enter: fade-up
@exit: fade
@visual: animation

--- visual ---
深色背景 (#0d1117)，内容区域占画布 88% 宽度。
[0s] 顶部居中标题 "LiDAR & RADAR"，字号 64px，粗体，白色，距顶 80px。

[0.5s] 画面分为左右两栏，总宽占画布 85%，间距 40px：

左栏 "LiDAR — 激光雷达"，宽度 48%，背景 #161b22，圆角 16px，内边距 24px，边框 1px #30363d：
  上方示意图：从中心圆形 LiDAR 向外发射多条射线（#58a6ff），射线末端形成 3D 点云（绿色小圆点散布），整体呈现旋转扫描的效果
  下方参数（字号 22px，行间距 24px）：
  "channels: 32 / 64"
  "range: 100m · rotation: 10Hz"
  "points_per_second: 600K"
  底部标注 "Semantic LiDAR 变体：点云 + 语义标签"，字号 20px，颜色 #3fb950

右栏 "RADAR — 毫米波雷达"，宽度 48%，同样式：
  上方示意图：一个扇形锥形区域（#f0883e，带透明度）
  下方说明（字号 22px，行间距 24px）：
  "锥形探测区域"
  "返回：速度 + 方位角 + 深度"
  "探测距离可配置"

两栏依次淡入，间隔 0.5s。
[3.5s] 底部强调："SparseDriveV2 不使用 LiDAR/RADAR，但它们是其他方案的标准配置"，字号 22px，颜色 #8b949e。

--- narration ---
**LiDAR** 通过旋转扫描生成三维点云
可以配置通道数、探测距离和旋转频率
**RADAR** 用锥形区域探测，返回速度和方位角
这两种传感器在很多自动驾驶方案中都是标配
但 SparseDriveV2 选择了纯视觉路线，不依赖它们


>>> 定位与事件检测 #B06
@enter: fade
@exit: fade
@visual: animation

--- visual ---
深色背景 (#0d1117)，内容区域占画布 88% 宽度。
[0s] 顶部居中标题 "定位与事件检测传感器"，字号 56px，粗体，白色，距顶 80px。

[0.5s] 下方出现两行布局：

上行 "定位传感器"，三个卡片横排，总宽占画布 82%，间距 28px：
  卡片 "GNSS" (#3fb950 边框)："纬度/经度/海拔 · 可配置噪声模型"
  卡片 "IMU" (#f0883e 边框)："加速度计 + 陀螺仪 · 高斯噪声"
  卡片 "罗盘" (#58a6ff 边框)："朝向 · 磁偏角模拟"

下行 "事件检测器"，三个条目纵向排列，行间距 16px：
  条目 1 (红色图标 #f85149) "Collision Detector — 碰撞时触发回调"
  条目 2 (黄色图标 #d29922) "Lane Invasion — 压线时触发"
  条目 3 (蓝色图标 #58a6ff) "Obstacle Detector — 前方障碍物告警"

[3.5s] 底部标注 "事件检测器 → Bench2Drive 扣分项的直接来源"，字号 22px，颜色 #3fb950，背景 #161b22，圆角 8px。

--- narration ---
**GNSS** 和 **IMU** 提供定位和姿态信息
可以加入噪声来模拟真实传感器的误差
三种**事件检测器**在闭环评测中至关重要
碰撞、压线、闯红灯的每一次违规
都是通过它们记录并计入最终的 Driving Score


>>> Ground Truth：训练与推理的区别 #B07
@enter: fade-up
@exit: fade
@visual: animation

--- visual ---
深色背景 (#0d1117)，内容区域占画布 90% 宽度。
[0s] 顶部居中标题 "Ground Truth 的使用边界"，字号 56px，粗体，白色，距顶 70px。

[0.5s] 画面中央出现左右分屏对比，总宽占画布 88%，间距 0px（紧密对比）：

左半 "训练阶段"，宽度 48%，背景 #0d1117，边框 2px solid #3fb950，圆角 12px，内边距 24px：
  上方场景示意：Ego 车俯视图 + 传感器画面，图像上叠加了 3D BBox 标注框（绿色 #3fb950，虚线）、语义分割叠加层
  下方标注 "监督信号" 字号 28px，颜色 #3fb950
  列表（字号 22px）：
  "GT 包围盒 → L_det"
  "GT 语义图 → L_map"
  "GT 轨迹 → L_plan"
  底部 "模型学习：正确结果是什么" 字号 20px，颜色 #8b949e

右半 "推理 / 闭环评测"，宽度 48%，背景 #0d1117，边框 2px solid #f0883e，圆角 12px，内边距 24px：
  上方场景示意：同样的 Ego 车和传感器画面，但**没有任何标注叠加**，只有原始图像
  下方标注 "输入" 字号 28px，颜色 #f0883e
  列表（字号 22px）：
  "仅原始传感器数据"
  "6 × RGB 图像"
  "无 GT、无标注、无地图"
  底部 "模型推断：自己判断一切" 字号 20px，颜色 #8b949e

两屏之间用红色竖线分隔（2px #f85149），上方标注 "不能偷看！" 字号 24px，颜色 #f85149。

[4s] 底部出现总结："GT 是训练时的老师，不是考试时的答案"，字号 26px，颜色 #e6edf3，背景 #161b22，圆角 8px。

--- narration ---
一个非常重要的区分
**训练阶段**，Ground Truth 是监督信号
包围盒、语义图、轨迹 —— 模型用它们学习"正确结果"
但到了**推理和闭环评测阶段**
模型只能看原始传感器数据
6 张 RGB 图像，不能偷看 GT，不能偷看高精地图
GT 是训练时的老师，不是考试时的答案


>>> 六相机数据流：从仿真到算法 #B08
@enter: fade
@exit: fade
@visual: animation

--- visual ---
深色背景 (#0d1117)，内容区域占画布 92% 宽度。
[0s] 顶部居中标题 "六相机数据流"，字号 56px，粗体，白色，距顶 60px。副标题 "从 CARLA 仿真到 SparseDriveV2 输入" 字号 28px，颜色 #58a6ff。

[0.5s] 画面中央出现数据流管线图，从左到右，总宽占画布 90%：

阶段 1（左侧）：Ego 车 + 6 相机俯视图（扇形 FOV）
  [0.5s] 6 个相机同时亮起（闪烁一次），表示同一帧采集

→ 箭头 + 标注 "tick" 字号 20px →

阶段 2：6 个图像矩形（2×3 排列，每个 100×60px，背景 #30363d，用不同的相机色边框）
  [1.2s] 每个矩形内出现 "frame_id = N" 标注（字号 14px），6 个全部相同，强调同步性
  下方标注 "同一帧 · 同一 timestamp" 字号 20px，颜色 #3fb950

→ 箭头 + 标注 "queue" →

阶段 3：一个图像队列示意（6 个矩形叠在一起，像一叠卡片）
  [2s] 标注 "Image Queue (FIFO)"，字号 22px
  下方 "6 × H × W × 3" 字号 20px，等宽字体

→ 箭头 + 标注 "stack & normalize" →

阶段 4（右侧）：一个大矩形 "SparseDriveV2 Model"，宽 280px，高 120px，圆角 12px，背景 #161b22，边框 2px solid #3fb950
  [3s] 内部 "Forward Pass → Trajectory" 字号 22px
  下方 "唯一的传感器输入" 字号 18px，颜色 #8b949e

[4s] 整个数据流下方出现强调标注："纯视觉端到端：6 个 RGB 图像进，1 条轨迹出"，字号 26px，颜色 #58a6ff。

--- narration ---
来看这 6 个相机如何把数据喂给算法
每一帧，CARLA 同步采集 6 个相机的图像
所有图像带有相同的 frame ID 和 timestamp
进入一个 FIFO 队列，按帧组织
然后 stacking 并归一化，送入 SparseDriveV2 模型
6 个 RGB 图像进，1 条规划轨迹出
这就是纯视觉端到端的完整数据流


>>> 本集总结 #B09
@enter: fade-up
@exit: fade
@visual: animation

--- visual ---
全屏深色背景 (#0d1117)。画面垂直居中布局，内容占画布 85% 宽度：
[0s] 顶部标题 "EP02 小结 · 三要素明确"，字号 56px，粗体，白色，距顶 80px。
[0.5s] 画面中央出现三角关系图，三个节点用 accent 色连线构成三角形：
  上方节点 "CARLA" (#58a6ff) — "闭环仿真环境 · 提供世界 + 传感器数据" 字号 24px
  左下节点 "SparseDriveV2" (#3fb950) — "参加考试的 Agent · 6 相机 → 轨迹" 字号 24px
  右下节点 "Bench2Drive" (#f0883e) — "考试协议 · 220 路线 + DS 评分" 字号 24px
三个节点依次淡入：[0.5s] CARLA → [1.5s] SparseDriveV2 → [2.5s] Bench2Drive。
[3s] 三条连线（accent 色，2px）同时出现，三角形闭合。中心出现 "闭环" 字样，字号 28px，颜色 #e6edf3。
[4s] 底部出现下集预告："下一集：CARLA 仿真引擎与 API — 让 tick 循环跑起来"，字号 28px，颜色 #58a6ff。

--- narration ---
这集我们给 Ego 车装上了传感器系统
6 个 RGB 环视相机是 SparseDriveV2 的全部输入
深度、语义分割等传感器提供训练用的 GT 监督
但要记住，推理时模型只能看原始传感器数据
这三者的关系要永远记住
CARLA 是仿真环境，SparseDriveV2 是考试 Agent
Bench2Drive 是评分考试协议
下一集我们深入仿真引擎和 Python API
让 tick 循环真正跑起来
