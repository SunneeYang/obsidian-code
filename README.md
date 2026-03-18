# Obsidian Skills - Claude Code 技能市场

Claude Code 技能市场 - Obsidian 集成工具集，提供与 Obsidian 笔记软件的无缝集成。

## 📦 包含的技能

### obsidian-session

保存 Claude Code 会话摘要到 Obsidian 仓库。

**功能特性：**
- 自动分析会话内容，提取关键信息
- 识别独立任务，支持多任务拆分
- 生成标准化的笔记结构
- 集成 Obsidian 插件（Templater、Tasks、Dataview）
- 支持中文标题和标签分类

**使用方法：**
```bash
/obsidian-session              # 自动分析并生成文档
/obsidian-session 标题         # 使用自定义标题创建文档
```

### obsidian-vault-organizer

整理和维护 Obsidian 知识库。

**功能特性：**
- 链接关系梳理（检查死链、发现孤立文档）
- 标签系统整理（统一格式、规范使用）
- 索引文档更新（自动统计、分类）
- 可视化支持（Canvas 关系图）
- 插件集成（Dataview、Tasks、Templater）

**使用方法：**
```bash
整理我的 Obsidian 知识库
检查文档链接
整理标签
更新索引文档
```

## 🚀 安装方法

### 方法 1：使用 Claude Code 插件市场（推荐）

```bash
# 添加市场
/plugin marketplace add https://github.com/SunneeYang/obsidian-skills

# 安装技能
/plugin install obsidian-session
```

### 方法 2：手动安装

```bash
# 克隆仓库
git clone https://github.com/SunneeYang/obsidian-skills.git /tmp/obsidian-skills

# 复制技能到本地
cp -r /tmp/obsidian-skills/skills/obsidian-session ~/.claude/skills/
```

## ⚙️ 配置要求

### 必需工具
- Obsidian CLI 工具
- Claude Code

### 可选插件
- **Templater** - 动态模板和自动化
- **Tasks** - 任务管理和跟踪
- **Dataview** - 数据查询和索引

### 首次使用配置

```bash
# 设置默认 vault
obsidian-cli set-default obsidian
obsidian-cli print-default  # 验证配置

# 复制模板到 vault
cp ~/.claude/skills/obsidian-session/templates/会话笔记模板.md \
   "/path/to/vault/Templates/"
```

## 📚 相关资源

- [obsidian-session 技能文档](https://github.com/SunneeYang/obsidian-skills/blob/main/skills/obsidian-session/SKILL.md)
- [obsidian-vault-organizer 技能文档](https://github.com/SunneeYang/obsidian-skills/blob/main/skills/obsidian-vault-organizer/SKILL.md)
- [Claude Code 官方文档](https://code.claude.com/docs/en/overview)
- [Obsidian 官网](https://obsidian.md/)

## 🤝 贡献

欢迎提交 Issue 和 Pull Request！

## 📄 许可证

MIT License

## 👨‍💻 作者

光 - [GitHub](https://github.com/SunneeYang)
