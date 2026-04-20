---
name: awesome-design-skill
description: UI设计风格选择器，从design-md风格库中选择合适的设计系统作为UI开发指导。支持50+知名品牌设计风格（Linear、Apple、Stripe、Vercel等）。当用户要求"设计页面"、"制作页面"、"创建UI"、"设计界面"、"用XX风格设计"等任务时触发此skill。也用于用户询问可用设计风格列表。**重构场景**：当用户要求"将XX改为YY风格"、"用YY风格重构XX"、"重新设计XX页面"等涉及现有页面风格改造的任务时也触发此skill。
---

# Awesome Design Skill

根据用户需求，从 design-md 风格库中选择合适的设计系统作为 UI 开发指导，并将 DESIGN.md 复制到当前工作目录。

## 脚本文件

| 脚本 | 用途 |
|-----|------|
| `scripts/list-styles.sh` | 列出所有可用的设计风格 |
| `scripts/smart-select.sh [需求描述]` | 智能选择设计风格（根据需求关键词匹配，无匹配则随机） |
| `scripts/random-style.sh` | 随机选择一个设计风格 |
| `scripts/get-design.sh <风格名称>` | 获取指定风格的 DESIGN.md 路径 |
| `scripts/copy-design.sh <风格名称> [目标目录]` | 复制 DESIGN.md 到指定目录（默认当前目录） |

## 工作流程

### 用户指定风格
1. 运行 `scripts/get-design.sh <风格名称>` 验证风格存在并获取路径
2. 运行 `scripts/copy-design.sh <风格名称>` 复制 DESIGN.md 到当前目录
3. 读取当前目录的 DESIGN.md 作为风格指导
4. 告知用户使用的设计风格

### 用户未指定风格

**重要：优先检查项目现有设计规范**

1. **首先检查项目目录是否存在 DESIGN.md**：
   - 检查当前工作目录是否有 DESIGN.md 文件
   - 如果存在，**必须直接使用这个文件中的设计规范**，禁止选择本 skill 中的其他风格或随机风格
   - 读取项目的 DESIGN.md 作为风格指导
   - 告知用户使用的是项目现有的设计规范

2. **如果项目目录不存在 DESIGN.md**，则进行智能匹配：
   - **分析用户需求**：理解用户要设计什么类型的页面/产品
   - **智能匹配风格**：运行 `scripts/smart-select.sh "<需求描述>"` 根据关键词匹配
     - 例如：`scripts/smart-select.sh "设计一个项目管理dashboard"`
     - 例如：`scripts/smart-select.sh "做一个音乐播放器界面"`
     - 例如：`scripts/smart-select.sh "创建企业级支付页面"`
   - 如果智能匹配未能找到合适风格，则使用 `scripts/random-style.sh` 随机选择
   - 运行 `scripts/copy-design.sh <选中的风格>` 复制 DESIGN.md 到当前目录
   - 读取 DESIGN.md 作为风格指导
   - **告知用户选择的设计风格及原因**

### 智能匹配关键词参考

根据用户需求中的关键词选择合适的风格：

| 需求类型 | 推荐风格 | 关键词 |
|---------|---------|--------|
| 项目管理/任务工具 | linear.app | 项目管理、issue、任务、看板、dashboard |
| 支付/金融科技 | stripe | 支付、金融、fintech、api、企业级 |
| 高端产品展示 | apple | 产品页、高端、简洁、landing、消费电子 |
| 音乐/媒体播放 | spotify | 音乐、播放器、media、音频 |
| 协作/文档工具 | notion | 笔记、文档、协作、workspace |
| 设计/创意工具 | figma, framer | 设计、协作、creative、创意 |
| 开发者工具 | vercel, cursor | 开发者、代码、terminal、编辑器 |
| AI产品 | claude | AI、人工智能、对话、助手、llm |
| 深色主题 | linear.app, vercel | 暗黑、深色、dark mode |
| 浅色主题 | apple, notion | 浅色、亮色、light mode |
| 旅行/预订 | airbnb | 旅行、民宿、预订、booking |
| 加密货币 | coinbase | 加密、crypto、区块链 |
| 数据分析 | posthog | 数据分析、analytics、监控 |

### 用户查看可用风格
运行 `scripts/list-styles.sh` 列出所有可用的设计风格。

### 用户重构现有页面
当用户要求将现有页面改为某种风格时（如"将index.html改为airbnb的风格"）：
1. 首先读取用户指定的现有页面文件，理解其当前结构和内容
2. 如果用户指定了目标风格：
   - 运行 `scripts/get-design.sh <目标风格>` 验证风格存在
   - 运行 `scripts/copy-design.sh <目标风格>` 复制到当前目录
3. 如果用户未指定目标风格（如"重新设计这个页面"）：
   - **首先检查项目目录是否存在 DESIGN.md**
   - 如果存在，**必须直接使用项目现有的设计规范**，禁止选择其他风格
   - 如果不存在，分析页面内容和用途，使用智能匹配选择合适的风格
4. 读取 DESIGN.md 作为风格指导
5. 根据新风格的设计系统，重构页面的：
   - 颜色方案（背景、文字、强调色等）
   - 字体排版（字体家族、字号、行高等）
   - 间距系统（边距、内边距、元素间距）
   - 阴影和圆角
   - 组件样式（按钮、卡片、表单等）
   - 动画效果
6. 保持页面原有的功能和内容结构，仅改变视觉风格
7. 告知用户重构完成及主要变化

## DESIGN.md 文件结构

每个 DESIGN.md 包含：
- Overview - 设计概述
- Colors - 颜色系统
- Typography - 字体排版
- Spacing - 间距系统
- Shadows - 阴影效果
- Border Radius - 圆角设置
- Components - 组件样式
- Animations - 动画效果

## 输出格式

完成设计后，告知用户：
1. 使用的设计风格名称
2. 选择该风格的原因（如果是智能匹配）
3. 主要设计特点概述
4. 生成的文件列表
