# Plot Is All You Need（私有图库版）

这是 `liouhai/plot-is-all-you-need` 的完整项目副本，包含技能说明、脚本、阶段指南和自带图库 `gallery/`；同时保留我的私人图库 `gallery-local/`。本仓库为 **Private**，私人图片不会发布到 GitHub Pages。

- [打开个人图库与图片目录](PERSONAL_GALLERY.md)
- 自带图库索引：[`gallery/INDEX.md`](gallery/INDEX.md)
- 个人图库索引：[`gallery-local/INDEX.md`](gallery-local/INDEX.md)
- [上游项目](https://github.com/liouhai/plot-is-all-you-need)

---

# Plot Is All You Need

**中文** | [English](README_EN.md)

[![Plot Is All You Need 宣传片](media/promo.gif)](media/promo.mp4)

<sub>点击上图观看带配乐的完整版（48 秒）</sub>

受够了拥有精彩绝伦的实验数据却苦于没有让人眼前一亮的展示图？
受够了拥有良好的审美知道什么好看却苦于AI总是画出平平无奇的图？
受够了经常鉴赏好看的配图却苦于用时想不起来？
受够了有良好的蓝本却苦于难于和AI描述？
是的，这个skill正是解决你这些烦恼的利器。Plot Is All You Need，你只需要看，找到好看的，把一切幕后都交给agent，一个让 agent 靠**看图**而不是靠规则来画图的技能。

写画图提示词很累：你得描述想要什么图、什么风格、什么配色，而大多数人说不清，只是看到了就知道喜不喜欢。
这个技能反过来做：它自带一个图库，像装修时的样板房。你说要画图，它把合适的样例摆成一张样板册让你挑；
你可以说"B 的布局加 E 的配色"；它用你的数据画出来，再和样例并排给你验收。

**图库就是审美。** 删掉你不喜欢的图，加进你喜欢的图，画出来的东西就会跟着变。

公开图库 `gallery/` 现有 364 张图，每张都有 agent 写的鉴赏卡片，其中 14 张带画图代码，装上就能用。

## 用起来是什么样

- **你有数据**：agent 自己到图库里筛候选、自己看图，然后直接用你的数据画出 4–6 种画法的草图，
  拼成一张样板册给你挑。这时你看到的是**自己数据的草图**，不是图库里的原图；
  每张草图会注明参照了图库里哪张图，想看原图就让它摆出来。
- **你没有数据，或只想先看看有什么**：agent 把图库里的样例原图摆成样板册。
- 两种情况选法一样：说"选 C"，或者组合，比如"B 的布局 + E 的配色"。
  每一轮里既有贴近你以往口味的，也有 agent 面向这次受众推荐的，各自标明。
- 选定之后，agent 精修出 PNG、PDF 和画图脚本，再把成品和样例并排给你验收。

## 四个阶段

| | |
|---|---|
| **Appreciation** 鉴赏 | agent 看懂图库里的每张图，写成卡片。卡片你可以直接改。 |
| **Resonance** 共鸣 | 把候选图摆成样板册。每一轮既有贴近你口味的，也有 agent 面向受众推荐的，由你决定。 |
| **Rendition** 演绎 | 用你的数据把选中的图画出来。数据整理由 agent 完成。 |
| **Appraisal** 品评 | agent 对照样例自查，再把样例和成品并排给你看。满意的成品可以收回图库。 |

## 安装

### Claude Code

```bash
git clone https://github.com/liouhai/plot-is-all-you-need.git ~/.claude/skills/plot-is-all-you-need
pip install -r ~/.claude/skills/plot-is-all-you-need/requirements.txt
```

### Codex

```bash
git clone https://github.com/liouhai/plot-is-all-you-need.git ~/.agents/skills/plot-is-all-you-need
pip install -r ~/.agents/skills/plot-is-all-you-need/requirements.txt
```

Codex 会自动发现新装的技能，没有出现就重启 Codex。输入 `/skills` 可以查看已安装的技能，输入 `$plot-is-all-you-need` 可以点名调用。

### 两个都用

只克隆一次，另一边建一个符号链接，这样两边共用同一个图库和同一份品味记录：

```bash
ln -s ~/.claude/skills/plot-is-all-you-need ~/.agents/skills/plot-is-all-you-need
```

装好之后，对 agent 说"帮我把这份数据画成图"即可。

### 建议停用 scipilot-figure-skill

如果你同时装了 `scipilot-figure-skill`，建议停用它。它会明确禁止一些图型，比如饼图、3D 图、双 Y 轴，
而这些图在合适的场合可能取得很好的效果；两个技能同时触发时会给出互相矛盾的建议。
本技能的做法是：所有图照常摆出来，附上一句提醒，由你决定。

## 维护你自己的图库
仓库自带的`gallery/`下的图片是我手动收集的我认为不错的图，你自然可以维护你自己的图库。图库是重中之重，就好比统计学里的数据，是本skill一切后续的源头。
- **删图**：直接删掉 `gallery/` 里的图片，然后让 agent "整理图库"。
- **加图**：把图片交给 agent 说"收进图库"，或者运行 `python scripts/ingest.py <图片或文件夹>`。
  入库时会自动去重，只是换了配色的图不会重复收录，它的配色会记到已有那张图的卡片上。
- **改卡片**：每张图旁边的同名 `.md` 就是 agent 对它的理解。写得不对就直接改，并把 `edited` 设为 `true`。

## 品味记录 taste.md
`taste.md` 记的是你以往选过什么。仓库里没有这个文件，它由 agent 在你第一次选图后创建在技能目录下。
- **什么时候写**：你在样板册里做出选择或明确否决某种画法时，以及成品验收完成后，agent 往文件末尾追加一行。
- **写什么**：日期、给谁看、选了什么、否决了什么、一句话概括。例如：
  `2026-10-04 | 期刊正文 | <id> 的布局 + <id> 的配色 | 否决 3D 和大面积渐变 | 想要"安静但不土"`
- **怎么用**：下次摆样板册时，agent 根据它挑出标为「贴近你的口味」的那几张。它不会用来排除任何图，同一张样板册里始终还有 agent 面向受众给出的「我的推荐」。
- **可以改**：它只是一个文本文件，记得不对就直接改，想从头来就清空或删掉。

## 图的来源和版权
- 卡片里 `source` 写着"自产"的图是本仓库用模拟数据或公开数据集画的，带画图代码，可以直接改数据复用。
- 其余的图收集自公开发表的论文，版权属于原作者和出版方，放在这里只作为版式和配色的参考，
  不在本仓库许可证的授权范围内。这些图的原始出处没有逐一查明。
- 如果你是某张图的作者，希望补上出处或者移除，请提 issue，会尽快处理。

## 实测开销

一次真实使用的记录（Claude Opus 5.5，Claude Code 桌面端），仅供参考。
任务是给论文里一张 3×3 的廓线图换几种画法，Claude 到远程服务器上找到数据和原脚本，
从 367 张图的图库里筛出 12 张候选，用真实数据画了 5 种画法的草图，拼成样板册交给用户挑。
记录到交出样板册为止，不含选定之后的精修和验收。

| | |
|---|---|
| 用时 | 6 分 18 秒 |
| 模型调用 | 21 次 |
| 输出 | 2.1 万 token |
| 上下文 | 从 6.8 万涨到 15.8 万 token，增加 9.0 万 |
| Pro 5h 额度 | 约 3% |

增加的 9.0 万 token 用在了哪里：

| 去向 | token | 占比 |
|---|---|---|
| 看图（候选样板册、原图、5 张草图，共 8 张，每张约 4500） | 3.6 万 | 40% |
| Claude 的输出（画图脚本约 0.9 万，其余是思考和回复） | 2.0 万 | 22% |
| 找数据、读原来的画图脚本 | 1.8 万 | 20% |
| 技能文档和在索引里筛图 | 1.2 万 | 13% |
| 其他 | 0.4 万 | 5% |

## 目录

```
SKILL.md            技能入口
stages/             四个阶段的细则
scripts/            入库、建索引、拼样板册（见下文「脚本说明」）
gallery/            公开图库
```

## 脚本说明

平时不用自己运行，Claude 会在需要时调用。想手动维护图库时，在技能目录下运行。

| 脚本 | 用途 | 什么时候用 |
|---|---|---|
| `ingest.py` | 把图收进图库：长边压到 2000 像素、去重、把换色变体的配色记到已有卡片上、标记低质量截图、生成空卡片 | 加图时 |
| `build_index.py` | 根据所有卡片重建 `INDEX.md`（每张图一行）；加 `--prune` 会清掉图已删除的卡片 | 加图、删图、改卡片之后 |
| `contact_sheet.py` | 把图拼在一起给人看：`sheet` 拼带 A、B、C 标号的样板册，`compare` 把样例和成品并排，`swatches` 列出一张图的所有配色 | 选图和验收时 |
| `cards.py` | 读写卡片的公共函数，被上面三个脚本调用，不直接运行 | — |

```bash
python scripts/ingest.py <图片或文件夹>                 # 默认收进 gallery-local/，加 --gallery gallery 收进公开图库
python scripts/build_index.py                           # 重建索引；加 --prune 清理孤儿卡片
python scripts/contact_sheet.py sheet --out sheet.png <id> <id> ...
python scripts/contact_sheet.py compare --out cmp.png --labels "样例,成品" <id> <成品.png>
python scripts/contact_sheet.py swatches --out pal.png <id>
```

## 许可证

代码、文档、鉴赏卡片和"自产"的图以 [MIT 许可证](LICENSE) 发布。收集自论文的图不在其内，见上文「图的来源和版权」。
