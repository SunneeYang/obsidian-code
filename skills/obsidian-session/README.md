# save-session 技能

保存当前 Claude Code 会话摘要到 Obsidian 仓库，使用组织化的文件夹结构。

## 功能特性

- 自动分析会话内容，提取关键信息
- 识别独立任务，支持多任务拆分
- 生成标准化的笔记结构
- 集成 Obsidian 插件（Templater、Tasks、Dataview）
- 支持中文标题和标签分类

## 安装方法

### 方法 1：手动安装

```bash
# 创建技能目录
mkdir -p ~/.claude/skills/save-session

# 复制文件
cp -r SKILL.md ~/.claude/skills/save-session/
cp -r templates ~/.claude/skills/save-session/
```

### 方法 2：从 GitHub 安装

```bash
# 克隆仓库
git clone https://github.com/yourusername/save-session-skill.git /tmp/save-session

# 复制到技能目录
cp -r /tmp/save-session/* ~/.claude/skills/save-session/
```

## 使用方法

在 Claude Code 中：

```bash
/save-session                          # 自动分析并生成文档
/save-session 自定义标题               # 使用自定义标题创建文档
```

## 依赖要求

- Obsidian CLI 工具
- Obsidian 插件（可选）：
  - Templater - 动态模板
  - Tasks - 任务管理
  - Dataview - 数据查询

## 技能结构

```
save-session/
├── SKILL.md           # 技能主文档
├── templates/         # 模板文件
│   └── 会话笔记模板.md
└── README.md          # 本文件
```

## 配置说明

首次使用需要设置默认 vault：

```bash
obsidian-cli set-default obsidian
obsidian-cli print-default  # 验证配置
```

## 模板使用

将模板复制到目标 vault：

```bash
cp ~/.claude/skills/save-session/templates/会话笔记模板.md \
   "/path/to/vault/Templates/会话笔记模板.md"
```

## 开发者

- 光
- GitHub: https://github.com/yourusername

## 许可证

MIT License
