# uml-复习手册

**这是什么**：给本人自己复习用的 **UML 复习手册**（本人 2026-09-26：「**都画出来，我把这个基础知识都差不忘了。**」）。
**谁做**：`research.investigator`（调查者）—— 这是他的长期职责；每轮交完走 `report` 通道，经理判。
**口径**：UML 2.5 **14 种图全画**；每种图四样齐全；**给人看**（中文、通俗），不是内部工程文档。

## 目录约定
- `docs/` 手册正文（`00-计划与轮次.md` 起）
- `src/` PlantUML 源（`.puml`，可 diff、可归档、丢库能重建）
- `figures/` 渲染出的图（`svg` 优先）
- `evidence/` 语法校验读数（`-checkonly` 输出 + rc + svg 清单）

## 硬判据
1. 每种图必须**四样齐全**：① 一句话（讲什么/什么时候用）② 关键元素（方框箭头各代表什么，术语中文）③ 最小示例（**全套共用同一个小例子**）④ `.puml` + 导出的图 + **校验 0 error 读数**；
2. 手册开头有「**选哪种图**」对照表（想表达什么 → 用哪张图）；
3. `java -jar plantuml.jar -checkonly` **rc=0** 且 `-tsvg` 导出成功（读数进 `evidence/`）；
4. **分轮出**：先出骨架 + 头几张给本人看，按反馈继续（**不许一口气写完再给他看**）；
5. **只出图与文档、不改代码**；图要写依据来源，不确定的关系标「待确认」。

## 第 1 轮交付（2026-09-26）

- `docs/01-选哪种图.md`：目录（14 张分四轮）+ **共用小例子定稿**（随笔 App：一句定位 + 名词表）+「选哪种图」对照表（14 行）+ 每图四样模板
- `docs/02-类图.md` · `docs/03-用例图.md` · `docs/04-时序图.md`：每张四样齐全（一句话 / 关键元素（术语中文）/ 最小示例 / 源与校验）
- `src/class-diagram.puml` · `src/use-case-diagram.puml` · `src/sequence-diagram.puml` → `figures/*.svg`（3 张）
- `evidence/校验-轮1.txt`：`-checkonly` rc=0（3/3）、`-tsvg` rc=0（3/3）

## 第 2 轮交付（2026-09-26/27）

- `docs/05-对象图.md` · `docs/06-包图.md` · `docs/07-组件图.md` · `docs/08-部署图.md`：每张四样齐全（一句话 / 关键元素（术语中文）/ 共用例子最小示例 / 源与校验）
- `src/object-diagram.puml` · `src/package-diagram.puml` · `src/component-diagram.puml` · `src/deployment-diagram.puml` → `figures/*.svg`（本轮 4 张，累计 7 张）
- `evidence/校验-轮2.txt`：`-checkonly` rc=0（4/4）、`-tsvg` rc=0（4/4）、四节四样自检 4/4

## 第 3 轮交付（2026-09-27）

- `docs/09-组合结构图.md` · `docs/10-制品图.md` · `docs/11-活动图.md` · `docs/12-状态机图.md`：每张四样齐全（一句话 / 关键元素（术语中文）/ 共用例子最小示例 / 源与校验）
- `src/composite-structure-diagram.puml` · `src/artifact-diagram.puml` · `src/activity-diagram.puml` · `src/state-machine-diagram.puml` → `figures/*.svg`（本轮 4 张，**累计 11 张**）
- `evidence/校验-轮3.txt`：`-checkonly` rc=0（4/4）、`-tsvg` rc=0（4/4）、四节四样自检 4/4，另有**新增闸门**「错误占位检查」——全 11 张 svg 逐个 grep `Cannot find Graphviz/Syntax Error` ＝ **0**
  （本轮实测踩到：状态机图默认要 graphviz，加 `!pragma layout smetana` 前 `rc=0` 但 svg 是一张报错占位图 ⇒ **rc=0 ≠ 图对**）

## 第 4 轮交付（2026-09-27，收尾轮）

- `docs/13-通信图.md` · `docs/14-交互概览图.md` · `docs/15-定时图.md`：每张四样齐全（一句话 / 关键元素（术语中文）/ 共用例子最小示例 / 源与校验）
- `docs/16-总校验表.md`：**全 14 张**总核对（图名 / 源 / 图 / rc / svg 字节 / 是否 smetana / 错误占位检查）＋ 合计行 ＋ **怎么复跑（四步命令）**
- `src/communication-diagram.puml` · `src/interaction-overview-diagram.puml` · `src/timing-diagram.puml` → `figures/*.svg`（本轮 3 张，**累计 14 张**）
- `evidence/校验-轮4.txt`：本轮 3 张 rc=0、全 14 张错误占位=0、四节四样自检 4/4
- 本轮两个新坑（已修，已写进经验）：活动图/定时图**不接受游离 `note`**（用 `legend`）；定时图 `scale` 太大 → svg 562KB（改 `scale 100 as 30 pixels` 后 20.9KB）

## 工具（已就位，不许联网下）
`/home/lwgat/tools/jdk-17.0.2/bin/java` ＋ `/vol1/1000/aicache/tools/plantuml.jar`（1.2024.8）；配方见 `roles-chat/env/UML建模-环境配方.md`，坑见 `roles-chat/experiences/research.investigator/UML交付与语法自测.md`。
