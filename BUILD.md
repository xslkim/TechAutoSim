# AutoVideo 构建指南

> 给负责构建的 Agent / 操作者：本仓库下 6 集 `project/EP01..EP06` 是输入资源，
> 按本指南把每集渲染成 MP4。脚本规范见 [`AUTHORING.md`](AUTHORING.md)。

---

## 0. 前置条件（必须先完成）

### 0.1 参考音色 `B00.wav`

所有 `project/EPxx/meta.md` 都引用 `voiceRef: ../../B00.wav`，即仓库根目录下的
`TechAutoSim/B00.wav`。该文件**不在仓库内**，必须由你提供：

- 时长 **10–30 秒**
- 单人清晰人声，**无背景音乐 / 噪声**
- **WAV** 格式，16 kHz 或 22.05 kHz / 24 kHz 均可，单声道或立体声
- 风格建议：自然语速、中性语气、播音腔 / 自媒体腔都可以，与教程内容匹配

放置：

```bash
cp /your/voice/reference.wav /home/ubuntu/TechAutoSim/B00.wav
```

> ⚠️ 6 集**共享同一参考音色**，所以提供一次即可。换 wav 后所有集都会换音色。

### 0.2 视频素材（assets/）

每集 `project/EPxx/assets/` 下的 mp4 已就绪（部分集没有 assets 是预期的，对应集
不引用本地视频）。素材清单：

| 集 | 资产文件 |
|----|---------|
| EP01 | `basic_driving_chase.mp4`, `basic_driving_topdown.mp4` |
| EP02 | `CAM_FRONT.mp4`, `CAM_FRONT_LEFT.mp4`, `CAM_FRONT_RIGHT.mp4`, `CAM_BACK.mp4`, `CAM_BACK_LEFT.mp4`, `CAM_BACK_RIGHT.mp4` |
| EP03 | `cutin_topdown.mp4`, `cutin_chase.mp4` |
| EP04 | （无 assets，全靠生成图） |
| EP05 | `CAM_FRONT.mp4`, `CAM_FRONT_LEFT.mp4`, `CAM_FRONT_RIGHT.mp4`, `model_driving_topdown.mp4` |
| EP06 | `pass_cutin_topdown.mp4`, `fail_changelane_topdown.mp4`, `fail_changelane_chase.mp4` |

所有视频均为 H.264 + `yuv420p`，1080p 或 540p，10 fps。

### 0.3 文生图 API

本项目脚本**几乎所有块都用 `@visual: image` 模式**，构建管线需要可用的文生图
API。验证方式：随便挑一个块，确认 `--- visual ---` 描述能跑通 prompt 流程并
生成图片。

---

## 1. 构建命令

> 具体命令依赖你使用的 AutoVideo 构建器实现。下面是**通用模板**。

### 1.1 单集构建

```bash
cd /home/ubuntu/TechAutoSim
autovideo build project/EP01-CarlaOverview
# 产物：build/carla-overview/{video.mp4, audio.wav, subtitles.srt}
```

构建步骤（管线内部）：

1. 解析 `meta.md` + `script.md`（按 `>>>` 切块）
2. 每块视觉资产：
   - `@visual: image` → 调文生图 API，按 prompt（即 `--- visual ---` 全文）生成
     PNG，缓存到 `build/<slug>/public/images/<block_id>.png`
   - `@visual: video(./assets/xxx.mp4)` → 拷贝到 `build/<slug>/public/videos/<block_id>.mp4`
3. 每块旁白：调 TTS，按行生成 wav，按 200ms 静音拼接
4. 字幕：按 narration 行 + TTS 实际时长生成 SRT
5. Remotion 渲染：把图片 / 视频 + 字幕 + 音频按块拼成最终 mp4

### 1.2 批量构建 6 集

```bash
for ep in project/EP*; do
  autovideo build "$ep" || { echo "$ep failed"; break; }
done
```

### 1.3 仅渲染（图片 / 视频 / 音频已生成时）

```bash
autovideo build project/EP01-CarlaOverview --skip-gen
```

---

## 2. 质量检查

构建完成后人工抽检：

| 检查项 | 通过标准 |
|--------|----------|
| 音画同步 | 字幕与口型偏差 ≤ 200ms |
| 字幕换行 | 单条字幕不应换行（如换行说明原始 narration 超 50 中字 / 70 英字符） |
| 图片清晰度 | 文生图产物分辨率 ≥ 1280×720，文字可读 |
| 视频接缝 | 视频块与图片块切换处不应有黑帧或闪烁 |
| 时长合理 | 单集 5–8 分钟（见下表预算） |

预期时长（按中文 5 字/秒估算 + 200ms 行间静音）：

| 集 | 预算 |
|----|------|
| EP01 | 5.4 min |
| EP02 | 4.7 min |
| EP03 | 5.7 min |
| EP04 | 5.5 min |
| EP05 | 7.0 min |
| EP06 | 6.8 min |
| **合计** | **≈35 min** |

---

## 3. 已知约束

### 3.1 视觉以**静态图片**为主

本项目所有原本应为 "animation" 的块都已改写为 `@visual: image`，每块产出**一
张静态构图**。视觉描述写成了**文生图 prompt**：

- 包含风格关键词、配色（hex）、字号、布局比例、文字内容
- 不包含时间轴 `[Xs]`、不包含 "依次淡入 / 从左滑入" 等动画动词
- 入场 / 退场动画（`@enter` / `@exit`）由 Remotion 外层负责

**只有 video 块和真正必要的过场仍为动态**。这是有意为之 ——静态画面利于知识
传播和截图引用。

### 3.2 标题字号实际上限

文生图模型对 "字号 96 px" 的指示理解为相对大小，最终成图字号取决于模型。
prompt 已写明"主标题大字 / 副标题中字 / 正文小字"等语义对照，作为兜底。

### 3.3 LaTeX / 复杂公式

`L = L_det + L_map + ...` 这类公式直接在图上以等宽字体呈现，**不**强求 LaTeX
渲染。如果图片模型把字符画错（比如 `L_det` 渲染成 `Ldet`），可在 prompt 末尾
追加 "render formulas exactly as written, monospace font, no auto-formatting"。

---

## 4. 故障排查

| 现象 | 排查 |
|------|------|
| TTS 启动失败 | 检查 `B00.wav` 是否存在、是否符合 §0.1 要求 |
| 文生图超时 | 多数图片 prompt 很长，确认 API 支持 ≥ 2000 字符 prompt |
| 字幕换行严重 | 找到对应 narration 行，按 `AUTHORING.md §4.4` 拆短 |
| 渲染卡死 | 检查显存（Remotion 1080p ≈ 4 GB）和磁盘空间（单集 ~2 GB 中间产物） |
| 视频块时长与块时长不一致 | 默认循环播放至块结束；如需精确对齐用 `@duration: <n>s` |

---

## 5. 交付物

每集构建完成后，产物位于：

```
build/<slug>/
├── video.mp4         ← 最终成片（1920×1080, 30 fps, H.264 + AAC）
├── audio.wav         ← 完整旁白音轨
├── subtitles.srt     ← 字幕文件
├── public/
│   ├── images/       ← 每个 image 块的 PNG（命名为 B01.png, B02.png ...）
│   └── videos/       ← 每个 video 块的 mp4
└── meta.json         ← 构建元信息（时长、块数、字幕统计）
```

打包发布：

```bash
cd build/<slug>
zip -r ../<slug>.zip video.mp4 subtitles.srt public/
```
