# 提示词片段库

可直接复制使用的片段。英文部分用于提示词，中文部分为使用说明。

---

## 一、参考图职责声明

放在提示词开头，逐张写明每张参考图锁定什么。**这是零成本、收益最高的一条。**

```text
【参考素材职责】
图1 = [角色A]身份图：只锁定[脸型、五官比例、发型、发色、瞳色、体型、服装、配饰、视觉气质]。
图2 = [角色B]身份图：只锁定[同上各项]。
图3 = 场景图：只锁定[场景结构、主锚、固定地标、光线方向、关键物体关系]。
图4 = 构图 / 分镜参考：STORYBOARD PLAN ONLY，只参考动作、空间、景别、构图与顺序，
      不参考最终人物长相、材质或画风。
```

未提供参考图的角色，写「无参考，按设计指纹生成」；未入场的角色，写「本片段不出现」。

---

## 一之二、⭐ 状态排除声明（2026-09-23 加，与职责声明同等重要）

上面只写了「锁定什么」。**锚点图还附带一整套拍摄当时的状态，模型会连状态一起继承** —— 必须逐类显式排除。

```text
The reference image provides IDENTITY ONLY: face shape, hairstyle, eye colour, and overall
vibe. Do NOT copy its expression (that is a state, not the baseline). Do NOT copy its pose
(that is a state, not her body). Do NOT copy its outfit colours — the outfit is fully
redescribed below and must follow the TEXT, not the reference image.
```

**三类状态与不排除的后果：**

| 类别 | 锚点上附带的典型状态 | 后果 |
|---|---|---|
| 表情 | 锚点是一张生气脸 | 所有派生图都凶 |
| 姿态 | 耸肩含胸、垂臂半握拳、脖前倾 | 所有派生图都弓背 |
| 服装配色 | 卡其外套 + 芥末黄内搭 | 配色怎么改都被带回来 |

> **机制**：图里的信息永远压过文字。文字想生效，**必须先在图层面把对应信息「否掉」**。

**诊断套路**：派生图**集体**出现同一种偏差 → 先查这里有没有漏排除，再看提示词。

---

## 一之三、体态硬约束块（所有常态图必带）

锚点的站姿不是她的身体。**这一块与角色指纹分开存放**，因为它属于镜头层。

```text
upright spine, chest open, shoulders relaxed and level (not raised, not hunched forward),
neck long, head level, arms hanging naturally with open relaxed hands (no clenched fists)
```

含胸 / 耸肩 / 半握拳**只允许**出现在明确指定的状态图（生气 / 应激 / 哈气）。

---

## 一之四、⭐ 五官绘制规范块（解决「脸不够可爱」，2026-09-23）

可爱度最大的杠杆是**眼部**，而它最常被漏写。**只写「大而圆的眼睛」远远不够。**

```text
eyes set relatively low on the face with a moderately wide gap between them, large rounded
eye openings with a full arched upper lid, a high iris-to-eye ratio with big rounded irises,
one large soft highlight placed high in each eye, soft defined upper lashes, eyebrows short
and gently arched, placed high with a wide gap between the brows and the eyes, eyebrow
colour a soft lighter brown, never dark or heavy — pretty and expressive as well as cute;
a short face shape with a soft jawline that is rounded but gently tapered (soft, not
childish), a small neat chin, small narrow nose, small mouth set low, features gathered in
the lower part of the face, full round cheeks, a faint soft blush across the cheeks,
refined delicate features, thin clean linework
```

**身材（「美」的那一半，与脸分工）：**

```text
{身高} cm tall, six-head-tall proportions (a petite adult woman, not chibi), a slender neck
with a clean shoulder line, a high waistline with long leg proportions, a neat narrow
silhouette
```

**⛔ 配套反向约束（必带，否则一路滑向低龄）：**

```text
never baby-faced, never chibi proportions, never heavy blush, never overly wide-set eyes,
never a fully circular chin, never a childlike body
```

**头身比**：`6 + (身高cm − 150) × 0.025`，由身高定不看年龄。150 cm = 6 头身。

---

## 二、身份板（Character Identity Board）

用于创建角色的身份锁定素材，**不是海报**。

```text
创建一张角色身份板，使用上传参考图中的[角色]作为唯一主体。

用途：后续 AI 图像与视频生成中的身份锁定，不是海报。

背景：纯白或柔和中性色，无环境、无品牌标志、无水印、无无关道具。

布局：角色设定集式布局，大面积留白，各视角互不遮挡，脸与肢体完整可见。

包含：
- 全身视角（中立站姿）
- 正面 / 背面 / 左右侧面
- 半身 / 脸部近景
- 坐姿 / 弯腰 / 蹲姿 / 标志性动作
- 3–5 个剧情需要的细微表情
- 发型、服装、鞋、配饰、关键道具细节

身份锁定：所有视角保持完全相同的脸型、五官比例、发型、服装、配饰、体型、
年龄感与视觉气质。不要换脸、不要换装、不要增加第二个角色、不要合并肢体。

文字只保留必要名称或标签；无法保证正确文字时宁可不生成文字。
```

**背景必须素底。** 带环境、带窗景、带光斑的素材会污染后续生成。

---

## 三、风格与负向约束

每次生成都带上，按角色取用。

**日系二次元统一（防写实）：**
```text
clean Japanese anime style, cel-shaded, soft flat shading, large clean eyes,
simple stylized nose and mouth, smooth clean skin, no facial hair, no stubble,
no body hair, no jaw shadow, not realistic, not photorealistic
```

**背景与人物同风格：**
```text
flat simplified anime background, simple shapes and color blocks,
no photoreal textures, no realistic bokeh, no camera depth of field,
no realistic lighting gradients — background and characters must look painted by the same hand
```

**穿鞋（男性 + 短裤组合最易被画成赤脚）：**
```text
everyone wearing shoes, visible footwear on every character
```

**脊椎直立（高冷类提示词容易诱导驼背）：**
```text
upright natural posture, straight spine, no hunching, no slouching
```

**无白角色（家猫默认联想会补出白围巾）：**
```text
no white, no white chest, no white markings, no white collar, no white socks
```

**改色类编辑必须附「保持不变」清单：**
```text
只修改[发色]。[保持不变] 服装名称与颜色、配饰、鞋、袜子长度、站姿、背景、画面构图、
线条风格全部不变。Do not alter anything else.
```

**⛔ 服装配色不回流（重出/改配色时必带，2026-09-23）：**
参考图上的旧配色绑得很深，不显式否定就会被带回来。把旧色逐一点名：
```text
no khaki, no olive green, no mustard yellow, no beige or brown outerwear
```
> 视具体角色的旧版配色替换词表。**只写新色不够，必须同时把旧色「否掉」。**

**⛔ IP 撞色禁区（商业付费产品，2026-09-23）：**
某个高辨识度的第三方 IP 吉祥物占住的颜色，主动避开并在负面清单里点名（本案例：粉色 —— 某游戏官方吉祥物的识别色）。**付费衍生品的判定比免费同人严格得多，不要赌。**

---

## 四、群像

**防漏人：**
```text
画面中共有 N 个角色，一个都不能少：[逐个点名]。
场景内 N 个座位、N 副餐具。
```

**未入场的角色必须显式声明：**
```text
[角色名] 本画面不出现。
```

**身高可读三件事（仅用于氛围图，几何准确交给校准合影）：**
```text
全员站在同一地平线上，平视机位，长焦压缩景深。
[角色A] 比 [角色B] 高，[角色B] 比 [角色C] 高。
全员脊柱直立，双脚着地。
```

**关系用坐位 / 朝向 / 视线承担，不用肢体接触：**
```text
[角色A] 身体朝向门外，视线却落在 [角色B] 身上，手里握着一样没有递出去的东西。
```

---

## 五、动态内容（L1 / L2）

**硬约束（每次必写）：**
```text
Camera completely locked off — absolutely no zoom, no pan, no dolly, no camera movement of any kind.
Everything else stays exactly identical to the first frame — same character design, same face,
same outfit, same colors, same line weight, same background.
Do not restyle. Do not add details. Do not change the art style.
```

**L1 微动（动作最多两个）：**
```text
Subtle micro-animation. The character stands still.
Only these movements: slow gentle breathing (chest and shoulders rise and fall slightly),
and one slow natural blink.
Minimal motion, calm and quiet feeling.
```

可选动作池（每次只取一到两个）：`one slow blink`、`gentle breathing`、`the tail tip sways slowly once`、`the hair tips drift slightly as if in a faint breeze`、`one ear twitches once`。

**L2 短镜头（用状态演进描述，不用时间轴秒点）：**
```text
画面从[正确的上一状态]接上。先[单一动作]，再[一个自然衔接的反应]，最后停在[目标末态]。
镜头内连续动作不超过两个。
```

**时长限制：** 低于下限（当前为 4 秒）会被服务端直接拒绝。

---

## 六、视频抽帧质检（生成后必做）

不能只看播放效果，必须抽帧逐帧比对。

```python
import cv2
from PIL import Image

cap = cv2.VideoCapture(video_path)
n = int(cap.get(cv2.CAP_PROP_FRAME_COUNT))
idxs = [int(n * i / 5) for i in range(6)]      # 均匀抽 6 帧

frames = []
for i in idxs:
    cap.set(cv2.CAP_PROP_POS_FRAMES, i)
    ok, fr = cap.read()
    if ok:
        frames.append(Image.fromarray(cv2.cvtColor(fr, cv2.COLOR_BGR2RGB)))
cap.release()
# 拼成 3×2 网格输出，逐帧核对：脸、发型、服装、配色、尾形、肢体数量、背景
```

**核对项：** 脸部与发色是否全帧一致、服装与配色是否变化、尾巴形态是否被重画、是否多出肢体、背景是否纹丝不动。

环境无 ffmpeg 时，`cv2` 可用（Python venv 内）。

---

## 七、出图质检项（生成后立即过一遍）

外观：尾形、耳形与耳背色、瞳色、白量映射、斑纹位置与面积、服装与配饰、穿鞋
体态：脊椎直立、头身比、脚是否被裁出画面、尾巴是否全程可见
画面：风格是否二次元、背景是否与人物同风格、角色数量正确、身高关系可读
合规：AI 生成标识是否保留、是否含不可外露的工艺内容
