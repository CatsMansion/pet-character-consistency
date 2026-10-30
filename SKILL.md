---
name: pet-character-consistency
displayName: "Pet Character Consistency (角色一致性)"
category: "game-asset"
slug: pet-character-consistency
description: "Continuous content production for 'pet (especially cat) photo to anthropomorphized character design' that keeps one character from drifting across multiple generations, shots, and materials. Covers freezing the character design fingerprint, reference-image role declaration, height handling for multi-character scenes, dynamic poster and short-video generation, per-frame QA, and outward display-boundary judgment. Use for character design sheets, anchor images, canonical full-body, turnaround three-view, character spec cards, group shots, height-calibrated ensemble photos, character dynamic posters or videos, character consistency maintenance. Triggers: 猫娘, anthropomorphic character, character design, anchor image, canonical body, three-view, group shot, dynamic poster, character consistency, pet character, character spec card."
agent_created: true
description_zh: "用于「宠物（尤其猫）照片 → 拟人角色设定」的连续内容生产，保证同一角色在多次生成、多个镜头、多种物料里不漂移。覆盖角色设计指纹冻结、参考图职责声明、多角色同框的身高处理、动态海报与短视频生成、逐帧质检、对外展示边界判定。当任务涉及拟人角色设定图、锚点图、规范全身图、转面三视图、角色规格卡、多角色群像、身高校准合影、角色动态海报或角色短视频、角色一致性维护时使用。Triggers 猫娘、拟人角色、角色设定、锚点图、规范全身、三视图、群像、动态海报、角色一致性、宠物角色、角色规格卡。"
---

# Pet Character Consistency · 使用入口

> 真内容在 `references/`：`continuity-memory.md`（资产结构与连续记忆）、`prompt-blocks.md`（可直接复制的提示词片段库）。本文件是**入口与流程总览**，具体块去 references 取。

## 何时用
宠物（尤其猫）照片 → 拟人角色设定的连续生产：保证同一角色在多次生成、多镜头、多物料里不漂移。
覆盖：身份板、锚点图、规范全身/转面三视图、角色规格卡、多角色群像、身高校准合影、动态海报/短视频、逐帧质检、对外展示边界。

## 三不漂移原则（硬）
1. **整段逐字冻结**：外貌与服装描述整段复制，禁拆变量槽位（`{发色}` 这类会漂移）。只动 `variable` 段；动 `frozen` 必须先由人指定唯一一处。
2. **参考图职责声明 + 状态排除**：每张参考图逐张写明锁什么；锚点图附带的状态（表情/姿态/旧配色）必须显式排除——图的信息永远压过文字，文字想生效须先在图层面把对应信息否掉。
3. **连续记忆承接**：每段 `end_state` 必须等于下一段 `start_state`；起始快照不能引用本段自己的 `end_state`（循环依赖）。

## 标准流程
1. **建身份板**（`prompt-blocks.md` §二）：纯素底，设定集式多视角布局，身份锁定用，不是海报。
2. **冻结设计指纹**（`continuity-memory.md` §一）：写 JSON，`frozen` 整段冻结，`variable` 留自由度，附 `color_card` 与 `negative`。
3. **写派单/提示词**（`prompt-blocks.md` 全篇）：职责声明 → 状态排除 → 体态硬约束 → 五官规范块 → 风格/负向约束 → （群像/动态）专用块。
4. **生成后质检**：图片质检（外观/体态/画面/合规，`prompt-blocks.md` §七）+ 视频抽帧质检（§六，cv2 均匀抽 6 帧逐帧比对脸/发色/服装/尾形/肢体数/背景）。
5. **跨镜头/跨集**：用 ID 规范（`cat_/loca_/prop_`）复用资产，续集传旧 ID 自动加载原设定。

## 漂移排查
`continuity-memory.md` §六 的列因果表：改 A 连带 B、这次不像上次、群像缺人、尾巴形状变、视频局部被重画、比例忽大忽小——逐条对号入座。

## 说明
- 这是 Ronny 自有 IP（Cat Mansion / LunaPet）的方法论沉淀；示例角色名（皮皮/露娜/koko）为占位示例，按需替换。
- 不绑定任何生成平台；提示词块中英对照，英文进 prompt，中文为使用说明。
