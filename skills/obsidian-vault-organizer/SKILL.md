---
name: obsidian-vault-organizer
description: 整理 Obsidian 知识库的技能，包括梳理链接关系、整理标签、更新索引文档
version: 1.0.1
author: Claude Code
trigger:
  - 当用户要求整理 Obsidian 知识库
  - 当需要梳理文档链接关系
  - 当需要检查和统一标签规范
  - 当需要更新或创建索引文档
---

# Obsidian 知识库整理技能

## 技能概述

本技能用于整理和维护 Obsidian 知识库，包括文档链接关系梳理、标签规范检查、索引文档更新等。充分利用已安装的 Obsidian 插件和 Claude Code 的 Obsidian 相关技能。

## 相关技能协作

整理过程中会调用以下技能：

| 技能 | 用途 | 调用时机 |
|-----|------|---------|
| `obsidian:obsidian-cli` | 读取、创建、搜索笔记 | 需要批量操作文档时 |
| `obsidian:obsidian-markdown` | 处理 Obsidian 特有语法 | 需要使用 wikilinks、callouts、embeds 时 |
| `obsidian:obsidian-bases` | 创建数据库视图 | 需要结构化数据展示时 |
| `obsidian:json-canvas` | 创建可视化关系图 | 需要展示文档关系时 |
| `obsidian-session` | 保存整理会话记录 | 整理完成后自动记录 |
| `obsidian:defuddle` | 提取网页内容 | 需要引用外部文档时 |

## 触发条件

当用户提出以下请求时触发：
- "整理知识库"
- "检查文档链接"
- "整理标签"
- "更新索引"
- "梳理文档关系"

## 知识库结构

\`\`\`
obsidian/
├── Claude Code/              # Claude Code 会话记录
│   ├── README.md            # 索引文档（必须保持最新）
│   └── YYYY-MM-DD/          # 按日期组织的会话笔记
├── OpenClaw/                # OpenClaw 使用记录
│   ├── README.md            # 索引文档（必须保持最新）
│   └── YYYY-MM-DD/          # 按日期组织的笔记
├── .obsidian/
│   └── plugins/
│       ├── dataview/        # 数据查询
│       ├── obsidian-tasks-plugin/  # 任务管理
│       ├── templater-obsidian/    # 模板系统
│       └── obsidian-git/    # Git 版本控制
└── CLAUDE.md                # 项目指南
\`\`\`

## 标签体系

### 标签分类规范

| 标签 | 使用场景 | 示例 |
|-----|---------|------|
| \`#索引\` | 索引文档 | README.md |
| \`#claude-session\` | Claude Code 会话记录 | 会话总结文档 |
| \`#openclaw\` | OpenClaw 相关 | OpenClaw 配置文档 |
| \`#bug修复\` | 修复缺陷或问题 | 问题修复记录 |
| \`#新功能\` | 实现新特性 | 功能开发记录 |
| \`#重构\` | 代码重构或优化 | 重构记录 |
| \`#性能优化\` | 性能改进 | 优化记录 |
| \`#配置\` | 环境或配置更改 | 配置文档 |
| \`#测试\` | 测试相关 | 测试记录 |
| \`#文档\` | 文档更新 | 文档更新记录 |
| \`#知识库整理\` | 知识库整理记录 | 整理会话记录 |

### 标签使用规则

1. **Frontmatter 格式**: 使用 YAML 数组
\`\`\`yaml
---
tags:
  - 标签1
  - 标签2
  - 标签3
---
\`\`\`

2. **大小写**: 使用中文标签（如 \`#新功能\`）或小写英文（如 \`#feature\`）
3. **一致性**: 同类内容使用相同标签
4. **避免冗余**: 一个文档最多 5 个标签

## Wikilink 规范

### 链接格式

\`\`\`markdown
<!-- 同目录相对链接 -->
[[2026-03-17/文档名]]

<!-- 跨目录链接 -->
[[Claude Code/README]]
[[OpenClaw/2026-03-17/文档名]]

<!-- 带别名链接 -->
[[文档名|显示文本]]

<!-- 块级链接 -->
[[文档名#^块ID]]

<!-- 标题链接 -->
[[文档名#标题]]
\`\`\`

### 链接检查清单

- [ ] 所有链接使用有效的文件路径
- [ ] 避免使用绝对路径
- [ ] 检查是否存在孤立文档（无链接指向）
- [ ] 检查是否存在死链（链接到不存在的文件）

## Obsidian Markdown 特性

### Callouts（提示框）

\`\`\`markdown
> [!INFO] 信息标题
> 信息内容

> [!WARNING] 警告标题
> 警告内容

> [!TIP] 提示标题
> 提示内容

> [!NOTE] 注意标题
> 注意内容
\`\`\`

支持的类型：INFO, WARNING, TIP, NOTE, CAUTION, IMPORTANT, QUESTION, EXAMPLE, QUOTE, SUCCESS, HELP, FAIL

### Embeds（嵌入）

\`\`\`markdown
![[文档名]]                    # 嵌入整个文档
![[文档名#章节]]              # 嵌入特定章节
![[文档名#^块ID]]             # 嵌入特定块
![[文档名|选项]]              # 带选项嵌入
\`\`\`

嵌入选项：
- `![[文档名|no-title]]` - 隐藏标题
- `![[文档名|hidden]]` - 隐藏内容但不删除

### Frontmatter 属性

\`\`\`yaml
---
title: 文档标题
date: 2026-03-18
tags:
  - 标签1
  - 标签2
status: 已完成
type: session-summary
related_tasks:
  - [[相关文档1]]
  - [[相关文档2]]
created: 2026-03-18T10:00:00
modified: 2026-03-18T15:30:00
---
\`\`\`

### 标签语法

\`\`\`markdown
# 行内标签
这是一个 #标签 示例

# 嵌套标签
这是父标签#子标签/孙标签

# 标签搜索
点击 #标签 查看所有相关文档
\`\`\`

## 文档 Frontmatter 规范

### 标准模板

\`\`\`yaml
---
title: 文档标题
date: YYYY-MM-DD
tags:
  - 标签1
  - 标签2
status: 已完成/进行中/已取消
type: session-summary/index/笔记
related_tasks:
  - [[相关文档1]]
  - [[相关文档2]]
---
\`\`\`

### 必填字段

- \`title\`: 文档标题
- \`date\`: 创建日期
- \`tags\`: 至少一个标签

### 可选字段

- \`status\`: 任务状态
- \`type\`: 文档类型
- \`related_tasks\`: 相关任务链接
- \`created\`: 创建时间
- \`modified\`: 修改时间

## 整理流程

### 第一步: 扫描知识库

使用 Bash 命令收集信息：

\`\`\`bash
# 统计文档数量
find . -name "*.md" -type f | wc -l

# 查找所有标签
grep -rh "^tags:" --include="*.md" . | sort | uniq

# 查找所有 wikilinks
grep -rh "\[\[.*\]\]" --include="*.md" . | sort | uniq

# 检查 frontmatter 完整性
find . -name "*.md" -type f -exec grep -L "^---$" {} \;
\`\`\`

### 第二步: 使用 obsidian-cli 批量操作

\`\`\`bash
# 列出所有文档
obsidian-cli list "Claude Code"

# 搜索特定标签
obsidian-cli search "标签:#bug修复"

# 搜索特定内容
obsidian-cli search "关键词"
\`\`\`

### 第三步: 检查链接关系

#### 检查死链

\`\`\`bash
# 提取所有 wikilinks 并验证文件是否存在
grep -roh "\[\[.*\]\]" --include="*.md" . | \
  sed 's/\[\[//;s/\]\]//;s/|.*//;s/#.*$//' | \
  sort -u | \
  while read link; do
    basename=$(echo "$link" | sed 's:.*/::')
    if ! find . -name "${basename}.md" | grep -q .; then
      echo "可能的死链: $link"
    fi
  done
\`\`\`

#### 检查孤立文档

使用 Dataview 查询：

\`\`\`dataview
TABLE file.link, file.inlinks
FROM -"README"
WHERE !file.inlinks AND !file.path.contains(".obsidian")
SORT file.name
\`\`\`

### 第四步: 使用 obsidian:obsidian-markdown 技能

当需要创建或编辑包含 Obsidian 特殊语法的文档时，调用 \`obsidian:obsidian-markdown\` 技能：

- 添加 wikilinks
- 创建 callouts
- 使用 embeds
- 添加 frontmatter

示例：创建一个带 callout 的索引文档

\`\`\`markdown
# 索引文档

> [!INFO] 统计信息
> - 总文档数: 12
> - 日期范围: 2026-03-17 至 2026-03-18

## 分类

### 第1类
![[2026-03-17/文档1]]
![[2026-03-17/文档2]]
\`\`\`

### 第五步: 整理标签

#### 统一标签格式

检查并修正：
- 中文标签统一使用全角
- 英文标签统一使用小写
- 避免混合使用（如 \`#Bug\` 和 \`#bug\`）

#### 标签建议

根据文档内容添加合适的标签：
- 如果是会话记录 → \`#claude-session\`
- 如果是问题修复 → \`#bug修复\`
- 如果是新功能 → \`#新功能\`
- 如果是配置相关 → \`#配置\`
- 如果是知识库整理 → \`#知识库整理\`

### 第六步: 使用 obsidian:json-canvas 创建可视化

对于复杂的文档关系，创建 Canvas 可视化：

1. 创建关系图
2. 按主题分组
3. 显示依赖关系
4. 标记孤立文档

示例调用：
\`\`\`
调用 obsidian:json-canvas 技能创建文档关系图
- 节点：每个文档
- 边：wikilink 引用关系
- 分组：按目录分类
\`\`\`

### 第七步: 更新索引文档

#### Claude Code/README.md 更新

使用 \`obsidian:obsidian-markdown\` 技能创建包含 Obsidian 特性的索引：

\`\`\`markdown
---
title: Claude Code 会话记录索引
date: 2026-03-18
tags:
  - 索引
  - claude-session
type: index
---

# Claude Code 会话记录索引

> [!INFO] 统计信息
> - **总文档数**: 12
> - **日期范围**: 2026-03-17 至 2026-03-18
> - **主要项目**: Vast 游戏开发、Claude Code 配置

## 📊 Dataview 查询

### 最近 7 天的文档

\`\`\`dataview
TABLE file.ctime["yyyy-MM-dd"] AS "创建日期", tags AS "标签"
FROM "Claude Code"
WHERE file.ctime >= date(today) - dur(7 days)
SORT file.ctime DESC
\`\`\`

### 按标签分组

\`\`\`dataview
TABLE rows.file.link
FROM "Claude Code"
FLATTEN tags AS tag
GROUP BY tag
\`\`\`

## 🗂️ 手动分类

### 1️⃣ 主题名称

| 文档 | 日期 | 标签 | 简介 |
|------|------|------|------|
| [[YYYY-MM-DD/文档名]] | YYYY-MM-DD | \`#标签1\` \`#标签2\` | 简短描述 |

## 🔗 相关

- [[OpenClaw/README]]
- [[CLAUDE.md]]
\`\`\`

### 第八步: 利用 Dataview 创建动态视图

在索引文档中添加 Dataview 查询：

\`\`\`dataview
### 📅 最近 7 天的文档

TABLE file.ctime["yyyy-MM-dd"] AS "创建日期", tags AS "标签"
FROM "Claude Code"
WHERE file.ctime >= date(today) - dur(7 days)
SORT file.ctime DESC

### 🏷️ 按标签分组

TABLE rows.file.link
FROM "Claude Code"
FLATTEN tags AS tag
GROUP BY tag
\`\`\`

### 第九步: 利用 Tasks 插件

检查并整理任务：

\`\`\`markdown
\`\`\`tasks
# 未完成的任务
not done
path includes Claude Code
sort by due
\`\`\`
\`\`\`

### 第十步: 保存整理记录

使用 \`obsidian-session\` 技能保存本次整理的会话记录：

\`\`\`
调用 obsidian-session 技能
标题: "整理 Obsidian 知识库"
\`\`\`

这将在 \`Claude Code/YYYY-MM-DD/\` 目录下创建整理记录文档。

## 常用命令

### 使用 obsidian-cli

\`\`\`bash
# 创建新文档（使用 obsidian:obsidian-cli 技能）
obsidian-cli create "Claude Code/2026-03-18/标题.md" --content "# 标题\n\n内容"

# 追加内容到现有文档
obsidian-cli create "Claude Code/README.md" --content "新内容" --append

# 搜索文档
obsidian-cli search "关键词"

# 列出目录
obsidian-cli list "Claude Code"
\`\`\`

### Git 操作

\`\`\`bash
# 查看修改
git status

# 提交整理结果
git add -A
git commit -m "docs: 整理知识库 - 更新索引、统一标签"
git push
\`\`\`

## 使用 obsidian:obsidian-bases 技能

当需要创建结构化数据视图时：

1. 创建 .base 文件
2. 定义视图（表格、卡片、列表等）
3. 添加过滤器和排序
4. 使用公式计算字段

示例应用：
- 文档清单数据库
- 任务追踪数据库
- 标签统计数据库

## 使用 obsidian:defuddle 技能

当需要引用外部文档时：

1. 使用 defuddle 提取网页内容
2. 清理格式和无关内容
3. 保存为本地 markdown
4. 添加到知识库并建立链接

## 注意事项

1. **备份优先**: 整理前先提交当前状态到 Git
2. **逐步进行**: 不要一次性修改过多文件
3. **保持一致**: 遵循已有的命名和格式规范
4. **验证链接**: 修改后检查 wikilinks 是否有效
5. **更新索引**: 每次添加新文档后更新对应的 README.md
6. **使用技能**: 充分利用 obsidian 相关技能提高效率
7. **保存记录**: 整理完成后使用 obsidian-session 保存记录

## Dataview 查询示例

### 查找所有会话记录

\`\`\`dataview
LIST
FROM "Claude Code"
WHERE type = "session-summary"
SORT file.ctime DESC
\`\`\`

### 查找孤立文档

\`\`\`dataview
LIST
FROM -"README"
WHERE !file.inlinks AND !file.path.contains(".obsidian")
SORT file.path
\`\`\`

### 按标签统计

\`\`\`dataview
TABLE length(rows) AS "文档数"
FROM "Claude Code" OR "OpenClaw"
FLATTEN tags AS tag
GROUP BY tag
SORT length(rows) DESC
\`\`\`

### 查找文档关系

\`\`\`dataview
TABLE file.inlinks AS "被引用", file.outlinks AS "引用"
FROM "Claude Code"
SORT file.mtime DESC
\`\`\`

## 整理检查清单

完成整理后确认：

- [ ] 所有文档有标准 frontmatter
- [ ] 标签格式统一且符合规范
- [ ] 无死链（所有 wikilinks 有效）
- [ ] 无孤立文档（或已确认是否需要保留）
- [ ] 索引文档（README.md）已更新
- [ ] 使用 Dataview 创建了有用的查询
- [ ] 已提交到 Git
- [ ] 文档分类合理（按主题/日期/项目）
- [ ] 使用了 obsidian 相关技能
- [ ] 使用 obsidian-session 保存了整理记录

## 常见问题

### Q: 如何处理没有 frontmatter 的旧文档？

A: 使用 \`obsidian:obsidian-markdown\` 技能添加标准 frontmatter，根据内容推断合适的标签和类型。

### Q: 索引文档如何自动更新？

A: 使用 Dataview 创建动态视图，或定期手动更新统计表格。

### Q: 如何发现文档之间的隐式关系？

A: 搜索共同关键词，查看标签重叠，分析相关任务字段，或使用 \`obsidian:json-canvas\` 创建可视化关系图。

### Q: 如何批量更新标签？

A: 
1. 使用 Bash grep 找到需要更新的文档
2. 使用 \`obsidian:obsidian-cli\` 批量读取和修改
3. 使用 \`obsidian:obsidian-markdown\` 确保格式正确

## 整理报告模板

整理完成后，使用 \`obsidian-session\` 保存的报告应包含：

\`\`\`markdown
---
title: 整理 Obsidian 知识库
date: YYYY-MM-DD
tags:
  - 知识库整理
  - claude-session
type: session-summary
---

# 整理 Obsidian 知识库

## 摘要
本次整理完成了文档链接梳理、标签统一、索引更新等任务。

## 整理内容

### 链接关系
- 检查文档数: XX
- 发现死链: XX
- 发现孤立文档: XX
- 修复链接: XX

### 标签整理
- 统一标签格式: XX 个
- 新增标签: XX 个
- 删除冗余标签: XX 个

### 索引更新
- 更新 Claude Code/README.md
- 更新 OpenClaw/README.md
- 添加 Dataview 查询: XX 个

### 创建的可视化
- 文档关系 Canvas: 1 个
- 数据库视图: XX 个

## 使用的技能
- \`obsidian:obsidian-cli\`: 批量文档操作
- \`obsidian:obsidian-markdown\`: Obsidian 特性支持
- \`obsidian:json-canvas\`: 关系可视化
- \`obsidian-session\`: 保存本次整理记录

## 修改的文件
- [[Claude Code/README]]
- [[OpenClaw/README]]
- ...其他文件

## 相关
- Git commit: {commit-id}
\`\`\`

## 相关技能

- \`obsidian-session\`: 保存 Claude Code 会话到 Obsidian
- \`obsidian:obsidian-cli\`: 使用命令行操作 Obsidian
- \`obsidian:obsidian-markdown\`: 处理 Obsidian 特有语法
- \`obsidian:obsidian-bases\`: 创建数据库视图
- \`obsidian:json-canvas\`: 创建可视化关系图
- \`obsidian:defuddle\`: 提取网页内容

## 版本历史

- **1.0.1** (2026-03-18): 新增对 obsidian 相关技能的利用
- **1.0.0** (2026-03-18): 初始版本，支持链接梳理、标签整理、索引更新
