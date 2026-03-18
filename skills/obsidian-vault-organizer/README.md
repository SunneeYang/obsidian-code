# obsidian-vault-organizer 技能

整理和维护 Obsidian 知识库的 Claude Code 技能。

## 功能特性

- **链接关系梳理**：检查死链、发现孤立文档、分析文档关联
- **标签系统整理**：统一标签格式、规范标签使用、提供标签建议
- **索引文档更新**：自动生成统计信息、按主题分类、集成 Dataview
- **可视化支持**：使用 Canvas 创建文档关系图
- **插件集成**：充分利用 Dataview、Tasks、Templater 插件

## 安装方法

### 方法 1：手动安装

```bash
# 创建技能目录
mkdir -p ~/.claude/skills/obsidian-vault-organizer

# 复制文件
cp /path/to/obsidian-skills/skills/obsidian-vault-organizer/SKILL.md \
   ~/.claude/skills/obsidian-vault-organizer/
```

### 方法 2：从 GitHub 安装

```bash
# 克隆仓库
git clone https://github.com/SunneeYang/obsidian-skills.git /tmp/obsidian-skills

# 复制到技能目录
cp -r /tmp/obsidian-skills/skills/obsidian-vault-organizer \
   ~/.claude/skills/
```

## 使用方法

在 Claude Code 中：

```bash
整理我的 Obsidian 知识库
检查文档链接
整理标签
更新索引文档
梳理文档关系
```

## 依赖要求

### 必需工具
- Obsidian CLI 工具
- Claude Code

### 相关技能
- `obsidian:obsidian-cli` - 批量文档操作
- `obsidian:obsidian-markdown` - Obsidian 特有语法支持
- `obsidian:obsidian-bases` - 数据库视图
- `obsidian:json-canvas` - 可视化关系图
- `obsidian-session` - 保存会话记录

### Obsidian 插件（推荐）
- **Dataview** - 数据查询和动态索引
- **Tasks** - 任务管理
- **Templater** - 模板系统

## 技能结构

```
obsidian-vault-organizer/
├── SKILL.md          # 技能主文档
├── skill.json        # 技能元数据
├── README.md         # 本文件
└── LICENSE           # MIT 许可证
```

## 整理流程

1. **扫描知识库** - 统计文档、标签、链接
2. **检查链接关系** - 发现死链和孤立文档
3. **整理标签** - 统一格式和规范
4. **创建可视化** - 使用 Canvas 展示关系
5. **更新索引** - 生成 README 和 Dataview 查询
6. **保存记录** - 使用 obsidian-session 保存

## 标签体系

技能支持以下标准标签：

- `#索引` - 索引文档
- `#claude-session` - Claude Code 会话记录
- `#bug修复` - 问题修复记录
- `#新功能` - 新功能开发
- `#配置` - 配置相关
- `#知识库整理` - 知识库整理记录

## 配置说明

首次使用需要设置默认 vault：

```bash
obsidian-cli set-default obsidian
obsidian-cli print-default  # 验证配置
```

## 开发者

- 光
- GitHub: https://github.com/SunneeYang

## 许可证

MIT License
