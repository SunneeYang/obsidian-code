---
name: obsidian-session
description: 基于 transcript 保存 Claude Code 会话到 Obsidian。完整记录不受上下文压缩影响。
allowed_tools: ["Bash", "AskUserQuestion", "Read", "Glob", "Write"]
---

# /obsidian-session - 保存会话到 Obsidian

基于完整的 **transcript 日志**保存 Claude Code 会话到 Obsidian，不受上下文压缩影响。

## 🎯 使用方法

```bash
/obsidian-session "标题"        # 指定标题
/obsidian-session               # 自动生成标题
```

例如：
```bash
/obsidian-session "优化数据库查询"
/obsidian-session "修复登录bug"
/obsidian-session               # 自动分析并生成标题
```

## 📋 执行步骤

### 0. 查找 Transcript

```
~/.claude/projects/<项目路径>/<session-id>.jsonl
```

**查找：**
```bash
ls -t ~/.claude/sessions/*.json | head -1 | xargs jq -r '.sessionId'
ls -t ~/.claude/projects/-*/**/*.jsonl 2>/dev/null | head -1
```

### 1. 检查文档是否存在

**不存在：** 继续执行步骤 2-5（正常生成新文档）
**已存在：** 执行步骤 6（智能合并文档）

### 2. 分析会话内容

提取：
- 主要问题和需求
- 讨论的解决方案
- 完成的成果
- 修改的文件

**分析方法：**
```bash
# 统计关键词频率
jq -r '.message.content' transcript.jsonl | grep -oE '\b[a-z]{4,}\b' | sort | uniq -c | sort -rn | head -20

# 提取用户消息
jq -r 'select(.type == "user") | .message.content' transcript.jsonl
```

### 3. 生成标题

**如果用户提供了标题：** 直接使用

**如果没有提供标题：**
- 基于步骤 2 的完整内容分析
- 统计关键词频率
- 识别主要动作和核心对象
- 生成 2-8 字标题，动词开头
- 示例：`优化数据库`、`修复bug`、`实现功能`

### 4. 生成文档

**智能标签：**
- 基础：`claude-session` + 状态
- 内容：根据 transcript 提取
  - 技术领域：`database`、`frontend`、`backend`
  - 任务类型：`bugfix`、`feature`、`optimization`
  - 具体工具：`mysql`、`redis`、`docker`
  - 关键词：`jwt`、`404-error`、`用户管理`

### 5. 保存

**使用 Obsidian CLI（优先）：**
```bash
if command -v obsidian &> /dev/null; then
    # 获取当前日期和 vault 路径
    DATE=$(date +%Y-%m-%d)
    VAULT_PATH="${OBSIDIAN_DEFAULT_VAULT:-~/Documents/work/obsidian}"

    # 创建文档（Obsidian CLI 官方命令格式）
    # vault: vault 的完整路径
    # name: 文件名（如果有空格需要用引号包裹）
    # path: 相对于 vault 根目录的文件夹路径
    # content: 文档内容
    obsidian create \
        name="$TITLE" \
        path="Claude Code/${DATE}/" \
        content="$CONTENT" \
        vault="$VAULT_PATH"

    # 验证文档是否成功创建
    FILE_PATH="Claude Code/${DATE}/${TITLE}.md"
    if [ -f "$VAULT_PATH/$FILE_PATH" ]; then
        echo "✓ 文档已创建: $FILE_PATH"
        # 可选：读取文档内容进行确认
        # obsidian read path="$FILE_PATH" vault="$VAULT_PATH"
    else
        echo "✗ 文档创建失败: $FILE_PATH"
        exit 1
    fi
else
    # 直接写入文件
    VAULT_PATH="${OBSIDIAN_DEFAULT_VAULT:-~/Documents/work/obsidian}"
    DATE=$(date +%Y-%m-%d)
    mkdir -p "$VAULT_PATH/Claude Code/$DATE"
    # 写入文件...
fi
```

**Obsidian CLI 命令格式说明：**
- `vault=<path>` - vault 的完整文件系统路径
- `name=<filename>` - 文件名（不含扩展名）
- `path=<folder>` - 相对于 vault 根目录的文件夹路径（以 `/` 结尾）
- `content=<text>` - 文档内容（支持 `\n` 换行符）

### 6. 智能合并（文档已存在）

读取现有文档 → 分析新内容 → 智能合并 → 去重 → 保存

## 📊 Transcript 格式

```json
{
  "type": "user|assistant|tool_use",
  "timestamp": "2026-03-19T02:39:12.183Z",
  "message": {"role": "user", "content": "消息内容"},
  "sessionId": "87129218-ea0c-4c5f-8234-97af71673827"
}
```

## ✨ 核心优势

| 特性 | 优势 |
|-----|------|
| **完整性** | ✅ 完整保留整个会话历史 |
| **时间范围** | ✅ 不受上下文窗口限制 |
| **可靠性** | ✅ 即使上下文被压缩也能完整记录 |
| **智能分析** | ✅ AI 自动提取关键信息 |
| **自动标题** | ✅ 基于完整内容自动生成 |
| **智能标签** | ✅ 根据内容动态生成标签 |
| **智能合并** | ✅ 多次调用时智能合并 |
| **工具兼容** | ✅ 优先 Obsidian CLI，自动回退 |

## 🎯 最佳实践

**标题：** 具体的中文标题（2-8字），动词开头
**标签：** 2-7 个，优先级：核心业务 > 技术领域 > 任务类型
**内容：** 摘要简洁、方案详细、文件用 wikilinks

## 🔗 与其他 Obsidian 技能的集成

本技能可与其他 Obsidian 技能配合使用，增强功能：

### obsidian:obsidian-markdown
处理 Obsidian Flavored Markdown 语法：
- **Wikilinks**：`[[文件名]]` 自动链接到其他笔记
- **Callouts**：使用 `> [!INFO]` 等语法创建提示框
- **Tags**：`#标签` 语法自动索引
- **Properties**：YAML frontmatter 元数据

```markdown
## 修改的文件
- [[skills/obsidian-session/SKILL.md]] - 技能主文档
- [[README.md]] - 项目说明

> [!TIP] 提示
> 可以使用 obsidian:obsidian-markdown 技能来优化格式
```

### obsidian:obsidian-bases
创建会话统计数据库：
- 记录所有会话的元数据
- 按日期、项目、标签筛选
- 统计会话时长和频率

```markdown
<!-- 可创建一个 Session Base -->
会话名称 | 日期 | 标签 | 状态 | 时长
---------|------|------|------|------
优化技能 | 2026-03-19 | optimization | 已完成 | 2h
修复bug | 2026-03-19 | bugfix | 已完成 | 1h
```

### obsidian:json-canvas
可视化会话关系：
- 创建会话依赖关系图
- 展示技能演进历程
- 追踪问题和解决方案的关联

## 🔧 技术细节

**环境变量：**
- `CLAUDE_SESSION_ID`：会话 ID（自动检测）
- `OBSIDIAN_DEFAULT_VAULT`：Vault 路径（默认：`~/Documents/work/obsidian`）

**文档路径规则：**
- 基础目录：`Claude Code/`
- 日期目录：`YYYY-MM-DD/`（使用当前日期）
- 完整路径：`Claude Code/YYYY-MM-DD/标题.md`
- 示例：`Claude Code/2026-03-19/优化数据库查询.md`

**依赖：**
- 必需：Bash、Read、Write
- 可选：Obsidian CLI（推荐）、jq

**回退：** Obsidian CLI 未安装 → 直接文件写入

**相关技能：**
- `obsidian:obsidian-cli` - Obsidian 官方 CLI 工具（本技能使用）
- `obsidian:obsidian-markdown` - Obsidian Flavored Markdown 语法支持（wikilinks、callouts 等）
- `obsidian:obsidian-bases` - 数据库功能（可用于会话数据统计）
- `obsidian:json-canvas` - 可视化画布（可用于会话关系图）

## 📝 示例

### 示例 1：指定标题

```bash
/obsidian-session "优化数据库查询"
```

**生成：**
- 标题：`优化数据库查询`
- 标签：`[claude-session, 已完成, database, mysql, optimization]`

### 示例 2：自动标题

```bash
/obsidian-session
```

**基于完整内容分析生成：**
- 标题：`实现用户认证`
- 标签：`[claude-session, 已完成, feature, authentication, jwt]`

### 示例 3：智能合并

```bash
# 第一次
/obsidian-session "实现新功能"

# 第二次（继续开发）
/obsidian-session "实现新功能"
```

**自动合并：** 更新摘要、添加新方案、追加成果、更新任务状态

---
