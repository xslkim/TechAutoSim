>>> 开场 #B01
@enter: fade-up
@exit: fade
@visual: image

--- visual ---
一张 16:9 横构图的扁平化教程封面图。深色背景 #0d1117。

主体居中布局：
- 顶部标签 "AutoSim 项目实战 · 番外"，灰色 #8b949e 字号 28px。
- 主标题 "EP07: 8 分到 9 分"，白色 #e6edf3 粗体字号 112px，居中。
- 主标题下方 16px 处一条 4px 粗的亮蓝色 #58a6ff 横线，宽度等于主标题宽度。
- 副标题 "多 Agent 协作修场景库"，灰色 #8b949e 字号 44px，距主标题下方 60px。

画面中央偏下是一个对比胶囊条（横向排列、总宽占画布 78%、高度 96px、深色背景 #161b22、圆角 16px、内边距大）：
左半 "epic_v2 (昨天)"：橙色 #f0883e 边框，中央数字 "8 PASS · 1 WARN · 1 FAIL" 字号 36px。
中间一个亮蓝色 #58a6ff 大箭头 "→" 字号 64px。
右半 "epic_v3 (今天)"：绿色 #3fb950 边框，中央数字 "9 PASS · 0 WARN · 1 FAIL" 字号 36px粗体高亮。

底部一行小字 "用 Cursor Agent 把场景库做扎实"，亮蓝色 #58a6ff 字号 32px。

整体风格极简、留白克制、对齐严格。

画面风格参考：类似 Notion / Linear 文档中的扁平化技术插图，深色主题、低饱和配色。画面干净、无噪点、无照片级写实纹理、无阴影、无渐变背景。所有中文文字必须准确渲染，不得出现乱码、缺笔或方块。文字与背景对比度 ≥ 4.5:1，确保在 1920×1080 视频帧中清晰可读。重要内容集中在画面中央 80% 安全区内。无任何 3D 写实渲染、无照片、无光晕特效。

--- narration ---
EP06 我们把闭环评测跑通了
但工程跑通**不等于**场景质量过关
昨天 epic_v2 批跑的成绩是
**8 通过、1 警告、1 失败**
今天我们要做的事很具体
让那条 WARN 变成 PASS
让那条勉强 PASS 的近撞远离危险线
最后用两个 **Cursor Agent 并发**把它做完

>>> 三类失败：ENG / ALG / SCN #B02
@enter: fade
@exit: fade
@visual: image

--- visual ---
一张 16:9 横构图的三分类示意图，扁平化技术风格。深色背景 #0d1117。

顶部居中标题 "失败的三种身份"，白色 #e6edf3 粗体字号 88px。
副标题 "verify_batch.py 自动诊断每条失败"，亮蓝色 #58a6ff 字号 36px。

画面中央三张大卡片横向排列（总宽占画布 90%、间距 48px、每张高度 420px、圆角 16px、深色背景 #161b22、3px 不同色边框、内边距 36px）：

卡片 1 "ENG"（紫色 #a371f7 边框）：
- 顶部标签 "Engineering" 字号 32px 灰色 #8b949e。
- 中央大字 "ENG" 字号 88px 紫色粗体。
- 下方说明 "参数 / 控制器 / 渲染" 字号 32px。
- 底部一行 "本仓库可改" 字号 28px 亮蓝色。

卡片 2 "ALG"（红色 #f85149 边框）：
- 顶部标签 "Algorithm"。
- 中央大字 "ALG" 字号 88px 红色粗体。
- 说明 "模型 / 域差 / 训练数据" 字号 32px。
- 底部 "需换模型或微调" 字号 28px 金色 #d29922。

卡片 3 "SCN"（青色 #2ea3a8 边框）：
- 顶部标签 "Scenario"。
- 中央大字 "SCN" 字号 88px 青色粗体。
- 说明 "Bench2Drive XML / Town 几何" 字号 32px。
- 底部 "需改场景定义" 字号 28px 亮蓝色。

画面底部一行金色 #d29922 中等字号粗体 "本期专攻：cut_in_right SCN  +  static_cross 近撞 ENG"，字号 36px。

整体风格干净、三栏对齐严格、所有英文缩写按字面准确渲染。

画面风格参考：类似 Notion / Linear 文档中的扁平化技术插图，深色主题、低饱和配色。画面干净、无噪点、无照片级写实纹理、无阴影、无渐变背景。所有中文文字必须准确渲染，不得出现乱码、缺笔或方块。文字与背景对比度 ≥ 4.5:1，确保在 1920×1080 视频帧中清晰可读。重要内容集中在画面中央 80% 安全区内。无任何 3D 写实渲染、无照片、无光晕特效。

--- narration ---
EP06 提到过 verify_batch 这个验收脚本
它会把每个失败 case 自动归到三类身份
**ENG** 是工程问题，参数控制可以改
**ALG** 是算法局限，模型本身就这样
**SCN** 是场景几何问题，Bench2Drive 没设计好
今天我们专攻两条
一条 SCN——cut_in_right 警告
一条 ENG——static_cross 近撞 1.93 米


>>> 决策路径与并发架构 #B03
@enter: fade-up
@exit: fade
@visual: image

--- visual ---
一张 16:9 横构图的并发架构图，扁平化技术风格。深色背景 #0d1117。

顶部居中标题 "今晚的施工计划"，白色 #e6edf3 粗体字号 88px。
副标题 "两个 Cursor Agent · 串行 + 并行混合", 灰色 #8b949e 字号 36px。

画面中央上半部分（占高 50%）是双轨道流程图，总宽占画布 90%：

轨道 A "Stream A · 场景工程师"（亮蓝色 #58a6ff 边框、深色背景 #161b22、圆角 16px、内边距 32px）：
- 顶部标签 "需要 CARLA 资源 · 必须串行" 字号 28px 金色 #d29922。
- 中部两个卡片左右排列，中间一个右指箭头：
  卡片 T1 "修 cut_in_right (SCN)" 字号 36px 白色，下方小字 "AutoSimCutInRight 子类" 28px。
  卡片 T2 "修 static_cross (ENG)" 字号 36px 白色，下方小字 "cruise + warmup feedback" 28px。

轨道 B "Stream B · 基础设施"（绿色 #3fb950 边框）：
- 顶部标签 "无 CARLA 依赖 · 内部并行" 字号 28px 绿色 #3fb950。
- 中部两个卡片并排（无箭头）：
  卡片 T3 "CI smoke pipeline" 36px。
  卡片 T4 "README / docs 同步" 36px。

两条轨道之间有一条灰色 #30363d 虚线，标注 "时间轴 → 同时运行"，字号 28px 灰色 #8b949e。

画面底部一行胶囊（深色背景 #161b22 圆角 8px、内边距 24px、白色 #e6edf3 字号 32px）：
"路径 A：先把 8 PASS 的场景库做扎实，再谈 Phase 2"

整体风格干净、双轨道对齐严格。

画面风格参考：类似 Notion / Linear 文档中的扁平化技术插图，深色主题、低饱和配色。画面干净、无噪点、无照片级写实纹理、无阴影、无渐变背景。所有中文文字必须准确渲染，不得出现乱码、缺笔或方块。文字与背景对比度 ≥ 4.5:1，确保在 1920×1080 视频帧中清晰可读。重要内容集中在画面中央 80% 安全区内。无任何 3D 写实渲染、无照片、无光晕特效。

--- narration ---
施工计划是这样的
四个任务分两条流
**Stream A** 是场景工程师
负责改 cut_in_right 和 static_cross
两个任务都要起 CARLA 跑闭环
所以必须串行
**Stream B** 是基础设施
写 smoke 流水线和文档同步
不依赖 CARLA
可以和 Stream A 同时跑
我用两个 Cursor Agent 把这两条流并发分发出去
我自己从这一刻开始就只是看进度

>>> T1 根因：cut_in_right 永远不切入 #B04
@enter: fade
@exit: fade
@visual: image

--- visual ---
一张 16:9 横构图的双场景对比示意图，扁平化技术风格。深色背景 #0d1117。

顶部居中标题 "T1 根因：NPC 从未真切入" 字号 80px 白色 #e6edf3 粗体。
副标题 "Bench2Drive CutInFrom_right_Lane @ Town04 弯道段" 字号 32px 金色 #d29922。

画面中央上半部（占高 55%）是俯视示意图，总宽占画布 90%、深色背景 #161b22、圆角 16px、内边距 32px：
- 一段从上往下、向左轻微弯曲的双车道路面（用浅灰色 #30363d 车道线表示弯道）。
- 左车道（Ego 车道）一辆蓝色 #58a6ff Ego 矩形从画面顶部驶向底部，留下一条蓝色虚线轨迹。
- 右车道（NPC 车道）一辆红色 #f85149 NPC 矩形从 Ego 后方追上，留下一条红色虚线轨迹。
- 两条轨迹**全程平行**，红色 NPC 轨迹只是从 Ego 后方逐步前移，最终从 Ego 右前方继续往前——**始终未跨越车道线**。
- 中间一条横向标注 "横向距离：2.9 m → 12 m（单调外移）" 字号 32px 金色 #d29922。

画面下半部居中是诊断证据卡片（深色背景 #161b22 圆角 12px、内边距大、等宽字体 monospace 字号 30px、白色 #e6edf3）：

verify_batch.py 自动诊断 (epic_v2)：
- npc_in_lane_ticks  =  0       ← NPC 一次都没进 Ego 车道
- merge_zone_ticks   =  0       ← 也从未进入合并区
- min_lat_offset     =  2.9 m   ← 最近横向距离仍 ≥ 车道宽
- ego brake_max      =  1.00    ← 模型确实刹了，但是看到旁边有车
分类：[SCN] 场景几何问题

底部一行红色 #f85149 字号 32px 粗体 "诚实地说：epic_v2 的 cut_in_right 从来没真发生过"。

整体风格干净、轨迹对比清晰。

画面风格参考：类似 Notion / Linear 文档中的扁平化技术插图，深色主题、低饱和配色。画面干净、无噪点、无照片级写实纹理、无阴影、无渐变背景。所有中文文字必须准确渲染，不得出现乱码、缺笔或方块。文字与背景对比度 ≥ 4.5:1，确保在 1920×1080 视频帧中清晰可读。重要内容集中在画面中央 80% 安全区内。无任何 3D 写实渲染、无照片、无光晕特效。

--- narration ---
先看 T1 的根因
Bench2Drive 这条 cut_in_right
NPC 在 Town04 弯道段做变道
但是 CARLA 在弯道上拒绝生成 LaneChange 的 waypoint
NPC 干脆走了一条**平行轨迹**
横向距离从 2.9 米单调拉大到 12 米
verify_batch 据此自动判 **SCN**
Ego 确实刹了车
但那是看到旁边有车的二次反应
不是真切入触发的
这条 case 在 epic_v2 里**根本就没发生过**


>>> T1 解法：自写 Python 子类 #B05
@enter: fade-up
@exit: fade
@visual: image

--- visual ---
一张 16:9 横构图的代码 + 流程示意图，扁平化技术风格。深色背景 #0d1117。

顶部居中标题 "AutoSimCutInRight 子类" 字号 84px 白色 #e6edf3 粗体。
副标题 "不动 upstream，在 Python 侧改激进 LaneChange 参数" 字号 36px 亮蓝色 #58a6ff。

画面分上下两部分。

上半部（占高 45%）左右两栏：

左栏 "父类 CutIn (上游 Bench2Drive)"（金色 #d29922 边框、深色背景 #161b22、圆角 12px、内边距 24px）：
- 标题字号 32px 白色。
- 等宽字体参数表（每行字号 26px 白色 #e6edf3）：
  catchup_trigger     = 5 m
  distance_same_lane  = 5 m
  lane_change_dist    = 25 m
  distance_other_lane = 300 m
- 底部小字 "默认参数：弯道生成不出 plan" 字号 24px 灰色 #8b949e。

中间一个亮蓝色 #58a6ff 大箭头 "→" 字号 64px。

右栏 "AutoSimCutInRight (本期新增)"（绿色 #3fb950 边框）：
- 标题字号 32px 白色粗体。
- 等宽字体参数表（每行字号 26px 白色，**绿色高亮变化值**）：
  catchup_trigger     = 15 m   ← 提早 10 m 触发
  distance_same_lane  = 2 m    ← 立即开始横切
  lane_change_dist    = 15 m   ← 弧长压短一半
  distance_other_lane = 40 m   ← 不要求长 plan
- 底部小字 "压回直线段完成切入" 字号 24px 绿色 #3fb950。

下半部（占高 50%）是路由示意图：
- 一个胶囊 "case_id = cut_in_right_osc2" 字号 32px 亮蓝色，连一个右指箭头。
- 一个圆角矩形 "_autosim_scenario_override 查表" 字号 30px 白色，深色背景 #161b22 圆角 12px。
- 再一个右指箭头到 "AutoSimCutInRight" 类卡片（绿色 #3fb950 边框）。
- 旁边一行小字 "case_id 层路由 · loader.py 加 30 行" 字号 24px 灰色 #8b949e。

画面底部居中一行白色 #e6edf3 字号 32px 粗体 "原则：不污染 upstream，AutoSim 自家 case 自己路由"。

整体风格干净、左右对比清晰、参数变化用绿色高亮一目了然。

画面风格参考：类似 Notion / Linear 文档中的扁平化技术插图，深色主题、低饱和配色。画面干净、无噪点、无照片级写实纹理、无阴影、无渐变背景。所有中文文字必须准确渲染，不得出现乱码、缺笔或方块。文字与背景对比度 ≥ 4.5:1，确保在 1920×1080 视频帧中清晰可读。重要内容集中在画面中央 80% 安全区内。无任何 3D 写实渲染、无照片、无光晕特效。

--- narration ---
解法的底层原则是**不动上游**
新建一个 Python 子类 AutoSimCutInRight
把父类 CutIn 的四个 LaneChange 参数全部改激进
catchup 触发距离从 5 米提前到 15 米
横切起点距离从 5 米压到 2 米
变道弧长从 25 米砍到 15 米
让 NPC 在 Town04 还允许变道的**直线段**就完成切入
然后在 loader 里加一层路由
case_id 是 cut_in_right_osc2 时
直接拿子类替换上游类
loader 只多了 30 行代码
Bench2Drive 仓库**一行没改**

>>> T1 关键决策：cut_in_left 不路由 #B06
@enter: fade
@exit: fade
@visual: image

--- visual ---
一张 16:9 横构图的双案例对比示意图，扁平化技术风格。深色背景 #0d1117。

顶部居中标题 "为什么 cut_in_left 不路由？" 字号 80px 白色 #e6edf3 粗体。
副标题 "已 PASS 的不要随便动 · 永久守护测试" 字号 36px 亮蓝色 #58a6ff。

画面分左右两栏，总宽占画布 88%，间距 64px。

左栏 "cut_in_right_osc2 (路由 ✓)"（绿色 #3fb950 边框、深色背景 #161b22、圆角 16px、内边距 32px）：
- 一行标签 "epic_v2: WARN" 字号 28px 金色 #d29922 → "epic_v3: PASS" 字号 28px 绿色 #3fb950 粗体。
- 中央三行 metric（等宽字体字号 30px 白色 #e6edf3）：
  npc_in_lane_ticks  0  →  18
  merge_zone_ticks   0  →  12
  min_npc_dist_m   5.06 → 2.06
- 底部一行 "✓ 真切入触发" 字号 30px 绿色 #3fb950。

右栏 "cut_in_left_osc2 (不路由 ✗)"（红色 #f85149 边框）：
- 标签 "epic_v2: PASS · epic_v3 试路由后" 字号 28px 红色 #f85149。
- 中央三行 metric：
  mean_speed   31.3  →  10.4 km/h  ← 暴跌
  npc_in_lane  23   →  18           ← 还行
  状态        PASS  →  WARN         ← **回归！**
- 底部一行 "✗ NPC merge 后贴 ego 4 m × 300 ticks" 字号 28px 红色。

画面下半部居中是一个守护测试卡片（深色背景 #161b22 圆角 12px、内边距 24px、宽度 75%）：
- 标题 "tests/test_autosim_cut_in.py" 字号 32px 白色等宽字体粗体。
- 一行测试名 "test_loader_override_skips_cut_in_left" 字号 28px 亮蓝色 #58a6ff 等宽字体。
- 底部小字 "永久守护此决策——以后任何人想路由 cut_in_left 都会被这个测试挡住" 字号 26px 灰色 #8b949e。

整体风格干净、左右对照鲜明（绿 vs 红）。

画面风格参考：类似 Notion / Linear 文档中的扁平化技术插图，深色主题、低饱和配色。画面干净、无噪点、无照片级写实纹理、无阴影、无渐变背景。所有中文文字必须准确渲染，不得出现乱码、缺笔或方块。文字与背景对比度 ≥ 4.5:1，确保在 1920×1080 视频帧中清晰可读。重要内容集中在画面中央 80% 安全区内。无任何 3D 写实渲染、无照片、无光晕特效。

--- narration ---
有个反直觉的决策必须讲
我**不**让 cut_in_left 也走新子类
理由是 cut_in_left 在 epic_v2 里已经 PASS
我试过把它也路由
NPC 切完车道后会贴在 Ego 后方 4 米持续 300 个 tick
触发 Pure Pursuit 的 proximity yield
平均速度从 31 km/h 砸到 10 km/h
结果反而**回归到 WARN**
所以子类只路由右侧
左侧保持原样
而且我把这个决策写成了一条单元测试
**永久守护**
以后任何人想随便扩大路由范围
都会被这条测试挡住


>>> T1 修复前后对比（v2） #B07
@enter: fade-up
@exit: fade
@visual: video(./assets/v2_cutin_right_topdown.mp4)

--- visual ---
（本块使用本地视频 ./assets/v2_cutin_right_topdown.mp4，无需生成图片）

epic_v2 cut_in_right_osc2 鸟瞰录屏：
Ego 蓝色车在车道内行驶，红色 NPC 从右后方接近后**始终在右车道平行驶过**，
两车横向距离 2.9 m → 12 m 单调外移。这是修复前的 SCN 现象。

--- narration ---
先看修复前
epic_v2 的 cut_in_right 鸟瞰录屏
红色 NPC 从右后方追上来
但是它从头到尾**没有跨车道**
就这么和 Ego 平行驶过去了
verify_batch 据此判定：场景几何问题
模型其实没什么可以怪的
是 Bench2Drive 在弯道根本没设计 NPC 切入

>>> T1 修复后（v3）：真切入发生 #B08
@enter: fade
@exit: fade
@visual: video(./assets/v3_cutin_right_topdown.mp4)

--- visual ---
（本块使用本地视频 ./assets/v3_cutin_right_topdown.mp4，无需生成图片）

epic_v3 cut_in_right_osc2 鸟瞰录屏：
启用 AutoSimCutInRight 子类后，红色 NPC 从右车道**真实切入** Ego 车道（轨迹明显跨过车道线），
Ego 检测到切入后输出减速轨迹，min_npc_dist 收敛到 2.06 m，
npc_in_lane_ticks 从 0 提升到 18，merge_zone_ticks 从 0 提升到 12。

--- narration ---
再看修复后
同一个 case 跑 epic_v3
NPC 在还允许变道的直线段
**完成了真正的切入**
Ego 检测到切入车辆
立即输出减速轨迹
最近距离 2.06 米
npc_in_lane_ticks 从 0 跳到 18
merge_zone_ticks 从 0 跳到 12
verify_batch 自动从 WARN 升到 PASS
**这才叫一次真正的 cut-in**

>>> T2 根因：1.93 米是怎么来的 #B09
@enter: fade-up
@exit: fade
@visual: image

--- visual ---
一张 16:9 横构图的运动学公式图，扁平化技术风格。深色背景 #0d1117。

顶部居中标题 "T2 根因：纯运动学不足" 字号 80px 白色 #e6edf3 粗体。
副标题 "static_cross_osc2 · 撞穿距离 12.9 m vs 可用 6 m" 字号 36px 金色 #d29922。

画面中央上半部（占高 50%）是一个时间轴示意图（总宽占画布 90%）：
- 顶部一条横向时间线（亮蓝色 #58a6ff 4px 实线），上面四个等距节点（深色背景 #161b22 圆角 12px、内边距 16px）：
  节点 1 "warmup 起点"  ego_v = 0 km/h
  节点 2 "warmup +20 tick"  ego_v = 36 km/h     ← 此时已撞距 6.18 m
  节点 3 "tick 0 (闭环开始)"  ego_v = 36.6 km/h  brake = 1.00
  节点 4 "tick 6 撞最近点"  ego_v = 27.9 km/h    npc_dist = 1.94 m ⚠️
- 每个节点下方一行 metric 字号 26px 白色 #e6edf3。

下半部（占高 45%）是一个公式块（深色背景 #161b22 圆角 12px、内边距 32px、等宽字体 monospace）：
- 标题 "为什么停不下来" 字号 36px 白色粗体。
- 第一行公式（字号 38px 白色，粗体）：
  min_stop_dist = v² / (2 · a_max) = (10 m/s)² / (2 · 4 m/s²) = 12.5 m
- 第二行（字号 38px 红色 #f85149 粗体）：
  available_dist = 6.18 m   ← 远小于需要
- 第三行（字号 32px 灰色 #8b949e）：
  结论：warmup 把 Ego 推太快，brake = 1.00 也来不及

画面底部一行金色 #d29922 字号 32px 粗体 "诊断：纯运动学问题，不是模型差，也不是控制器差"。

整体风格干净、公式按字面准确渲染。

画面风格参考：类似 Notion / Linear 文档中的扁平化技术插图，深色主题、低饱和配色。画面干净、无噪点、无照片级写实纹理、无阴影、无渐变背景。所有中文文字必须准确渲染，不得出现乱码、缺笔或方块。文字与背景对比度 ≥ 4.5:1，确保在 1920×1080 视频帧中清晰可读。重要内容集中在画面中央 80% 安全区内。无任何 3D 写实渲染、无照片、无光晕特效。⚠️ 本图包含数学公式。公式符号使用标准数学排版，确保平方、除号、等号准确可读。

--- narration ---
T2 的根因是**纯运动学不足**
warmup 阶段把 Ego 加速到 36 km/h
但是 static_cross 的障碍物
就放在 Ego 正前方 6 米
36 km/h 全力刹车
理论最小停车距离是 12.5 米
可用距离只有 6 米
就算 brake 一开始就拉满 1.0
也来不及
最后实测撞到 1.93 米
这不是模型差
也不是控制器软
就是**起跑速度太快**


>>> T2 方案 A 反作用：YIELD 反而加速 #B10
@enter: fade
@exit: fade
@visual: image

--- visual ---
一张 16:9 横构图的反作用机制图，扁平化技术风格。深色背景 #0d1117。

顶部居中标题 "为什么直接加 YIELD 反而错了" 字号 76px 白色 #e6edf3 粗体。
副标题 "proximity_yield 是覆盖式，不是 cap-only" 字号 36px 金色 #d29922。

画面中央是一个公式对比 + 数值示例图（总宽占画布 88%、深色背景 #161b22 圆角 16px、内边距 36px）：

上行 "proximity_yield_speed 的实际行为" 字号 36px 白色粗体。

中部一个等宽代码块（字号 28px 白色 #e6edf3）：
def proximity_yield_speed(dist_m, cruise_ms, ...):
    if in_merge_zone(...):
        return max(2.0, 0.35 * dist_m)   ← 注意 max 而不是 min
    ...

中部右侧一个数值代入框（深色背景 #0d1117 圆角 12px、字号 30px 等宽）：
dist = 5 m  →  yield = max(2.0, 1.75) = 2.0 m/s = 7.2 km/h

下半部是两个并排卡片对比（间距 48px、每张圆角 12px、内边距 24px）：

卡片 1 "模型 brake 意图"（亮蓝色 #58a6ff 边框）：
- 大字 "1.9 km/h" 字号 64px 白色粗体。
- 下方小字 "model_est：把车停下" 字号 28px。

卡片 2 "yield 覆盖后"（红色 #f85149 边框）：
- 大字 "7.2 km/h" 字号 64px 红色粗体。
- 下方小字 "yield 把目标抬到 7 km/h，brake 被 cancel" 字号 28px。

画面底部一行红色 #f85149 字号 32px 粗体 "撤回方案 A · 但保留为永久 regression 测试"。

整体风格干净、代码与数值清晰对照。

画面风格参考：类似 Notion / Linear 文档中的扁平化技术插图，深色主题、低饱和配色。画面干净、无噪点、无照片级写实纹理、无阴影、无渐变背景。所有中文文字必须准确渲染，不得出现乱码、缺笔或方块。文字与背景对比度 ≥ 4.5:1，确保在 1920×1080 视频帧中清晰可读。重要内容集中在画面中央 80% 安全区内。无任何 3D 写实渲染、无照片、无光晕特效。

--- narration ---
我第一反应是
把 static_cross 加进 YIELD_CASES
让靠近时主动减速
**单元测试立刻挂了**
原因是 proximity_yield 这个函数
在合并区返回的是 **max(2.0, 0.35×距离)**
也就是说
NPC 离 5 米时它告诉控制器
目标速度至少 7.2 km/h
而模型本来想让车降到 1.9 km/h 停下
yield 反而把刹车意图**覆盖**了
正确做法应该是 min 而不是 max
但改了会影响 cut-in
所以方案 A **撤回**
撤回这件事必须留痕
我把它写成了一条 regression 测试
永久守护 future me 不要重蹈覆辙

>>> T2 真修法 B + C：双管齐下 #B11
@enter: fade-up
@exit: fade
@visual: image

--- visual ---
一张 16:9 横构图的方案叠加图，扁平化技术风格。深色背景 #0d1117。

顶部居中标题 "方案 B + C 叠加修复" 字号 80px 白色 #e6edf3 粗体。
副标题 "降巡航 + warmup 反馈 throttle" 字号 36px 亮蓝色 #58a6ff。

画面中央两个并排大卡片（总宽占画布 88%、间距 64px、每张圆角 16px、深色背景 #161b22、3px 不同色边框、内边距 36px）：

卡片 B "降巡航速度"（亮蓝色 #58a6ff 边框）：
- 顶部标签 "speed_fix.py" 字号 28px 灰色 #8b949e 等宽字体。
- 中央一行变化（字号 38px 等宽白色）：
  static_cross_osc2:  36  →  22 km/h
- 下方说明字号 28px 白色 "让起跑速度配得上可用距离"。
- 底部小字 "等价于 Ego 6 m/s · 最小停车 4.5 m" 字号 26px 绿色 #3fb950。

卡片 C "warmup 反馈 throttle"（绿色 #3fb950 边框）：
- 顶部标签 "run_closed_loop_record.py" 字号 28px 灰色 #8b949e 等宽字体。
- 中央伪代码（等宽字体字号 26px 白色 #e6edf3）：
  if v >= cruise:
      warmup_throttle = 0.0
  elif v >= 0.95 * cruise:
      warmup_throttle = 0.2
  else:
      warmup_throttle = 0.7
- 下方说明字号 28px 白色 "warmup 不再无脑加速到顶"。
- 底部小字 "让方案 B 真起作用，避免越速 13 km/h" 字号 26px 绿色。

画面底部居中是验收 metric 对比卡片（深色背景 #161b22 圆角 12px、内边距 24px、宽度 75%、等宽字体）：

字号 32px 白色 #e6edf3：
                  epic_v2     epic_v3
min_npc_dist_m    1.93        3.88     ← 离危险线 ≥ 2 m
tick 0 ego_speed  36.6 km/h   20.7 km/h
tick 0 npc_dist   6.18 m      10.25 m
brake_max         1.00        1.00

底部一行绿色 #3fb950 字号 36px 粗体 "✓ 1.93 m → 3.88 m · 安全余量翻倍"。

整体风格干净、左右两卡片对仗、metric 表格数字清晰。

画面风格参考：类似 Notion / Linear 文档中的扁平化技术插图，深色主题、低饱和配色。画面干净、无噪点、无照片级写实纹理、无阴影、无渐变背景。所有中文文字必须准确渲染，不得出现乱码、缺笔或方块。文字与背景对比度 ≥ 4.5:1，确保在 1920×1080 视频帧中清晰可读。重要内容集中在画面中央 80% 安全区内。无任何 3D 写实渲染、无照片、无光晕特效。

--- narration ---
真正的修法是 B 和 C 叠加
**B** 把 static_cross 的巡航速度从 36 降到 22 km/h
让起跑速度配得上可用距离
**C** 改 warmup 阶段的 throttle 反馈
速度到了巡航就停止加速
不让 warmup 把车推过头
单独 B 不够
因为原 warmup 持续 throttle = 0.7 会越速 13 km/h
让 B 的调整失效
两者叠加之后
最近距离从 1.93 米升到 **3.88 米**
安全余量翻倍


>>> T2 修复后实景对比 #B12
@enter: fade
@exit: fade
@visual: video(./assets/v3_static_cross_topdown.mp4)

--- visual ---
（本块使用本地视频 ./assets/v3_static_cross_topdown.mp4，无需生成图片）

epic_v3 static_cross_osc2 鸟瞰录屏：
Ego 蓝色车以 22 km/h 巡航接近静止 NPC（红色），
检测到障碍后渐进刹车，最终在距离障碍 3.88 m 处稳定停下，brake = 1.00。
对比 epic_v2 的 1.93 m，本次安全余量翻倍。

--- narration ---
来看修复后的鸟瞰录屏
Ego 用 22 km/h 巡航靠近
模型识别到静止障碍物
brake 平滑拉到 1.0
最终在距离障碍 **3.88 米**的地方稳稳停下
对比之前 1.93 米的视觉擦碰
这次的余量足够踏实
而且不是靠 cherry-pick 的参数
是靠**配速 + warmup 反馈**这两个工程修复

>>> CI smoke + 文档同步：自动化兜底 #B13
@enter: fade-up
@exit: fade
@visual: image

--- visual ---
一张 16:9 横构图的流水线图，扁平化技术风格。深色背景 #0d1117。

顶部居中标题 "Stream B：基础设施收口" 字号 76px 白色 #e6edf3 粗体。
副标题 "43 秒端到端冒烟 · epic_v3 成为默认基线" 字号 36px 亮蓝色 #58a6ff。

画面中央上半部（占高 50%）是 4 步流水线（总宽占画布 92%、横向连接、每步圆角 12px、深色背景 #161b22 2px 不同色边框、内边距 24px）：

步骤 1 "pytest 非集成"（亮蓝色 #58a6ff 边框）：
- 大字 "17 s" 字号 56px 白色粗体。
- 下方 "61 passed (基线 51)" 字号 26px 绿色 #3fb950。

步骤 2 "ensure_carla low"（绿色 #3fb950 边框）：
- 大字 "0 s" 字号 56px 白色粗体。
- 下方 "容器复用 · 幂等" 字号 26px。

步骤 3 "dummy 闭环 8s"（紫色 #a371f7 边框）：
- 大字 "26 s" 字号 56px 白色粗体。
- 下方 "cut_in_left @ low" 字号 26px。

步骤 4 "verify_batch L1-only"（金色 #d29922 边框）：
- 大字 "0 s" 字号 56px 白色粗体。
- 下方 "工程链路完整" 字号 26px。

四步右端连一个总和胶囊（绿色 #3fb950 实心、白色 #e6edf3 字号 48px 粗体）"= 43 s"。

下半部（占高 45%）是文档同步示意图：

左半 "文档与基线收口"（深色背景 #161b22 圆角 12px、内边距 24px、宽 42%、等宽字体）：
- README.md  ← 加 Milestone 1+ 状态行
- docs/milestone_1_plan.md  ← 追加 §14
- docs/milestone_1_report.md  ← 追加 epic_v3 段
- .github/workflows/smoke.yml  ← pytest + ruff

中间一个右指箭头（亮蓝色 #58a6ff 字号 64px）。

右半 "成果"（亮蓝色 #58a6ff 边框、深色背景 #161b22 圆角 12px、内边距 24px、宽 42%）：
- epic_v3 成为 README 默认验收基线（字号 30px 白色 #e6edf3）
- verify_report.json 归档到 work_state（字号 26px 灰色 #8b949e）
- 批跑产物写进 .gitignore（字号 26px 灰色）
- 与 Stream A 解耦完成（字号 28px 绿色粗体 "✓ 无代码冲突"）

整体风格干净、流水线清晰、数字按字面准确渲染。

画面风格参考：类似 Notion / Linear 文档中的扁平化技术插图，深色主题、低饱和配色。画面干净、无噪点、无照片级写实纹理、无阴影、无渐变背景。所有中文文字必须准确渲染，不得出现乱码、缺笔或方块。文字与背景对比度 ≥ 4.5:1，确保在 1920×1080 视频帧中清晰可读。重要内容集中在画面中央 80% 安全区内。无任何 3D 写实渲染、无照片、无光晕特效。

--- narration ---
Stream B 同时在做基础设施
四步端到端 smoke
单元测试 17 秒
CARLA 启动 0 秒——容器复用
dummy 闭环 26 秒
最后 verify_batch L1 检查 0 秒
**总共 43 秒**就能验证整条工程链
任何人 push 代码前
都可以一行命令跑一遍
此外文档也同步更新
README 状态行
plan 加章节
report 追加 epic_v3 段
**基线归档、产物忽略、零代码冲突**
和 Stream A 完全解耦

>>> 收尾：今晚的成绩单 #B14
@enter: fade-up
@exit: fade
@visual: image

--- visual ---
一张 16:9 横构图的最终成绩对比图，扁平化技术风格。深色背景 #0d1117。

顶部居中标题 "今晚的成绩单" 字号 96px 白色 #e6edf3 粗体。

画面上半部（占高 45%）是大对比卡片（总宽占画布 88%、深色背景 #161b22 圆角 16px、内边距 36px）：

左半 "epic_v2"（橙色 #f0883e 边框、半宽）：
- 大字 "8 PASS · 1 WARN · 1 FAIL" 字号 48px 白色粗体。
- 下方 "1 SCN · 1 ALG" 字号 32px 灰色 #8b949e。
- 底部 "昨天的基线" 字号 28px 灰色。

中间一个亮蓝色 #58a6ff 大箭头 "→" 字号 80px。

右半 "epic_v3"（绿色 #3fb950 边框、半宽）：
- 大字 "9 PASS · 0 WARN · 1 FAIL" 字号 48px 绿色 #3fb950 粗体高亮。
- 下方 "0 SCN · 1 ALG" 字号 32px 白色。
- 底部 "今天 + 1 PASS" 字号 28px 绿色 #3fb950。

下半部（占高 50%）是三栏总结（每栏圆角 12px、深色背景 #161b22、内边距 24px、间距 36px）：

栏 1 "工程纪律"（亮蓝色 #58a6ff 边框）：
- 标题字号 36px 白色粗体。
- 三行要点（字号 28px 白色 #e6edf3）：
  • 不动 upstream
  • 失败方案留 regression 测试
  • verify_batch 自动分类

栏 2 "下一条 FAIL"（红色 #f85149 边框）：
- 标题 "change_lane (ALG)" 字号 32px 白色粗体。
- 字号 28px：
  • 弯道横向轨迹近零
  • 域差 · 不在本期范围
  • 下一步：CARLA finetune

栏 3 "Phase 2 路口"（金色 #d29922 边框）：
- 标题 "三选一" 字号 36px 白色粗体。
- 字号 28px：
  • 四轨渲染对照
  • 多算法横评
  • 中国 case 库扩展

底部一行字号 32px 灰色 #8b949e "61 passed · 2 个 commit · origin/main 已同步"。

整体风格干净、收尾感强、绿色高亮 9 PASS 主体。

画面风格参考：类似 Notion / Linear 文档中的扁平化技术插图，深色主题、低饱和配色。画面干净、无噪点、无照片级写实纹理、无阴影、无渐变背景。所有中文文字必须准确渲染，不得出现乱码、缺笔或方块。文字与背景对比度 ≥ 4.5:1，确保在 1920×1080 视频帧中清晰可读。重要内容集中在画面中央 80% 安全区内。无任何 3D 写实渲染、无照片、无光晕特效。

--- narration ---
今晚的成绩单
**epic_v3：9 通过、0 警告、1 失败**
比昨天多一条 PASS
SCN 清零
代码和文档分成两个 commit 落地
最后已经同步到 origin/main
我自己的角色
是定义 4 个任务的验收标准
然后让两个 Cursor Agent 并发把它跑完
工程纪律有三条
不动 upstream
失败方案保留 regression 测试
失败要被 verify_batch 自动分类
唯一剩下的 FAIL 是 change_lane
那是模型在 CARLA 弯道上的域差
属于 ALG
要靠**finetune** 救场
不在本期范围
下一步要么修这条 FAIL
要么进 Phase 2
四轨渲染、多算法、中国 case 库
三选一
我们下集见

