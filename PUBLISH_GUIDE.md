# Obsidian Skills 发布指南

本指南说明如何将 Obsidian 相关技能发布到 Claude Code 市场。

## 📦 仓库结构

```
obsidian-skills/
├── .claude-plugin/
│   └── marketplace.json          # 市场配置文件（必需）
├── skills/
│   ├── obsidian-session/         # 会话保存技能
│   │   ├── SKILL.md
│   │   ├── templates/
│   │   ├── README.md
│   │   ├── LICENSE
│   │   └── skill.json
│   └── [future-skills]/         # 未来可以添加更多技能
└── README.md                     # 仓库说明
```

## 🚀 发布步骤

### 1. 修改个人信息

需要修改的文件：
- `.claude-plugin/marketplace.json` - 市场所有者信息
- `skills/obsidian-session/skill.json` - 技能元数据
- `README.md` - 仓库说明

### 2. 推送到 GitHub

```bash
cd /tmp/obsidian-skills-marketplace
git init
git add .
git commit -m "feat: 初始化 Obsidian 技能市场"

git remote add origin https://github.com/SunneeYang/obsidian-skills.git
git branch -M main
git push -u origin main
```

### 3. 用户安装

```bash
# 添加市场
/plugin marketplace add https://github.com/SunneeYang/obsidian-skills

# 安装技能
/plugin install obsidian-session

# 使用技能
/obsidian-session
```

## 🔧 命名说明

### 为什么叫 obsidian-session？

- **obsidian** - 清楚表明是与 Obsidian 集成
- **session** - 表示保存会话内容
- 比 `save-session` 更具体和准确

### 为什么用 obsidian-skills？

- 可以包含多个 Obsidian 相关技能
- 为未来扩展留出空间
- 更通用和可维护

## 📚 参考资源

- [Claude Code 官方文档 - 插件市场](https://code.claude.com/docs/en/plugin-marketplaces)
- [Anthropic 官方插件市场](https://github.com/anthropics/claude-plugins-official)
