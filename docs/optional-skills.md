# 可选 Skills

## 目标
- 记录适合按需引入、但不建议默认进入基础模板的外部 Skill。
- 帮助项目在需要特定能力时快速判断是否值得接入。
- 避免基础模板因强工具绑定而变得过重。

## 使用原则
- 默认不将强平台绑定 Skill 纳入基础工作流。
- 仅当项目场景、工具链和输入条件都满足时，再按需启用。
- 引入前应先说明：
  - Skill 解决什么问题
  - 依赖哪些外部工具或 MCP
  - 为什么当前项目值得引入

## 已收录 Skills

### Stitch 设计链路
适用于：
- 使用 Stitch 做设计生成或设计驱动前端开发的项目
- 希望把设计信息、设计提示词、页面生成和后续集成串成一条流程的项目

### design-md
- 来源：
  - [design-md](https://skills.sh/google-labs-code/stitch-skills/design-md)
- 定位：
  - 分析 Stitch 设计项目，并生成语义化 `DESIGN.md`，作为后续 Stitch 生成界面的设计真相源。
- 适用场景：
  - 项目正在使用 Stitch
  - 已有至少一个设计完成的 Stitch screen
  - 希望通过 `DESIGN.md` 约束后续 UI 生成结果
- 依赖前提：
  - Stitch MCP Server
  - 至少一个可分析的 Stitch 设计 screen
  - 对 Stitch Prompting Guide 的基本理解
- 建议结论：
  - 作为可选设计扩展引入
  - 不建议默认纳入通用多 Agent 模板基线
- 原因：
  - 强依赖 Stitch 生态
  - 只对部分设计驱动项目有价值
  - 对不使用 Stitch 的项目会增加理解与维护负担
- 安装方式：
```bash
npx skills add https://github.com/google-labs-code/stitch-skills --skill design-md
```

### enhance-prompt
- 来源：
  - [enhance-prompt](https://skills.sh/google-labs-code/stitch-skills/enhance-prompt)
- 定位：
  - 将模糊的 UI 想法整理成更适合 Stitch 生成的结构化提示词，并可结合 `DESIGN.md` 保持设计一致性。
- 适用场景：
  - 用户给出的 UI 想法过于模糊
  - 需要把零散需求整理成稳定的 Stitch prompt
  - 多页面项目希望保持一致的设计语言
- 依赖前提：
  - Stitch 工作流
  - 最好已有 `DESIGN.md`
- 建议结论：
  - 推荐作为 Stitch 设计链路的高价值可选 Skill
  - 不建议默认纳入通用模板基线
- 原因：
  - 对使用 Stitch 的项目帮助很大
  - 但对不走设计生成工作流的项目几乎无价值
- 安装方式：
```bash
npx skills add https://github.com/google-labs-code/stitch-skills --skill enhance-prompt
```

### react:components
- 来源：
  - [react:components](https://skills.sh/google-labs-code/stitch-skills/react%3Acomponents)
- 定位：
  - 将 Stitch 设计拆解并落地为更模块化的 React 组件与相关前端结构。
- 适用场景：
  - 项目使用 React
  - 希望把 Stitch 设计结果转成更干净的组件结构
  - 需要把设计到实现的链路工程化
- 依赖前提：
  - Stitch MCP
  - React 项目
  - 对组件拆分和本地前端结构有明确要求
- 建议结论：
  - 推荐作为 Stitch -> React 落地能力的可选扩展
  - 不建议默认纳入所有项目基线
- 原因：
  - 强依赖 React 与 Stitch
  - 对普通文档型或后端型项目无直接价值
- 安装方式：
```bash
npx skills add https://github.com/google-labs-code/stitch-skills --skill react:components
```

### stitch-loop
- 来源：
  - [stitch-loop](https://skills.sh/google-labs-code/stitch-skills/stitch-loop)
- 定位：
  - 通过 Stitch 生成、页面集成、任务接力的循环机制，进行更自动化的网站构建。
- 适用场景：
  - 想把 Stitch 生成流程串成多轮自动迭代
  - 项目已经具备较明确的网站愿景与设计基线
  - 需要“设计生成 -> 集成 -> 下一轮任务”闭环
- 依赖前提：
  - Stitch MCP
  - `.stitch/DESIGN.md`
  - `.stitch/SITE.md`
  - 最好还有可用的本地站点结构
- 建议结论：
  - 作为高级可选 Skill 收录
  - 不建议默认进入基础模板
- 原因：
  - 工作流较重，依赖条件多
  - 更适合成熟的 Stitch 网站生成链路，而不是通用模板
- 安装方式：
```bash
npx skills add https://github.com/google-labs-code/stitch-skills --skill stitch-loop
```

### remotion
- 来源：
  - [remotion](https://skills.sh/google-labs-code/stitch-skills/remotion)
- 定位：
  - 基于 Stitch 设计稿生成 walkthrough 视频或演示视频。
- 适用场景：
  - 产品需要演示视频、营销视频或交互 walkthrough
  - 设计稿已经在 Stitch 中成型
- 依赖前提：
  - Stitch MCP
  - Remotion MCP 或 Remotion CLI
  - 可用的 Node.js / npm 环境
- 建议结论：
  - 作为展示与营销产物扩展加入
  - 不建议默认纳入开发模板基线
- 原因：
  - 场景明确但不高频
  - 更偏展示资产生产，不属于大多数项目的核心开发流程
- 安装方式：
```bash
npx skills add https://github.com/google-labs-code/stitch-skills --skill remotion
```

### UI 组件工程化
适用于：
- 需要把界面实现标准化、组件化的前端项目
- 已明确使用 React + Tailwind 等现代前端栈的项目

### shadcn-ui
- 来源：
  - [shadcn-ui](https://skills.sh/google-labs-code/stitch-skills/shadcn-ui)
- 定位：
  - 提供 shadcn/ui 组件发现、安装、集成和定制的工程化指导。
- 适用场景：
  - 项目使用 React + Tailwind
  - 想按需接入 shadcn/ui 组件和 blocks
  - 希望保留组件源码而不是依赖外部 UI 库黑盒
- 依赖前提：
  - React 18+
  - Tailwind CSS 3+
  - 可用的 shadcn 相关工具链
- 建议结论：
  - 作为前端 UI 工程化扩展推荐加入
  - 不建议默认纳入所有项目基线
- 原因：
  - 价值很高，但技术栈限定明显
  - 对非 React / Tailwind 项目不适用
- 安装方式：
```bash
npx skills add https://github.com/google-labs-code/stitch-skills --skill shadcn-ui
```

### 通用创意资产
适用于：
- 需要生成视觉素材、插图、封面图、Mockup 或产品图的项目
- 不一定依赖 Stitch，但需要更强的图像产出能力

### imagegen
- 来源：
  - [imagegen](https://skills.sh/openai/skills/imagegen)
- 定位：
  - 通过 OpenAI 图像能力生成或编辑项目所需图片资产。
- 适用场景：
  - 生成网站视觉图、插图、封面图
  - 生成 UI mockup、产品图、Logo 草图
  - 对现有图片进行编辑、替换背景、局部修改
- 依赖前提：
  - 正常使用内置图像能力即可
  - 若显式走 CLI fallback，需 `OPENAI_API_KEY`
- 建议结论：
  - 推荐作为通用创意资产扩展加入
  - 不建议默认进入基础工作流模板
- 原因：
  - 通用性高，但并非每个项目都需要图片生成
  - 放入 optional 比放入 baseline 更合适
- 安装方式：
```bash
npx skills add https://github.com/openai/skills --skill imagegen
```

## 引入判断清单
在决定是否引入某个外部 Skill 前，至少检查以下问题：

1. 它是否服务于当前项目的真实高频需求
2. 它是否依赖特定平台、MCP 或第三方生态
3. 它是否会提高大多数项目的通用效率，而不是只服务少数场景
4. 如果不引入，现有模板是否已经足够支持当前工作
5. 引入后是否需要新增文档、流程说明或维护成本

## 推荐策略
- 通用、高频、低耦合的 Skill：
  - 可考虑纳入长期基线
- 强平台绑定、强场景绑定的 Skill：
  - 建议记录在本文件中，按需使用
