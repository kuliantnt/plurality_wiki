# 首页问题修复说明

## 🐛 原问题

1.**首页 URL 错误**- 点击"首页"跳转到 `/index-material/` 而不是 `/`
2.**侧边栏显示**- 首页是否应该显示侧边栏（已解决，默认显示）
3.**README.md 冲突**- `docs/README.md` 与 `index.md` 冲突

## ✅ 解决方案

### 1. 修复首页 URL

**问题原因**：MkDocs 要求首页必须命名为 `index.md`，使用其他名称会导致 URL 不正确。

**解决方法**：

- ✅ 将 `index-material.md` 的内容复制到 `index.md`
- ✅ 在 nav 配置中使用 `index.md`
- ✅ 保留 `index-material.md` 和 `index-simple.md` 作为备份

### 2. 侧边栏控制

Material 主题支持通过 frontmatter 控制首页是否显示侧边栏：

**隐藏侧边栏（适合纯展示型首页）**：

```yaml
---
hide:

  - navigation  # 隐藏左侧导航
  - toc         # 隐藏右侧目录

---
```

**显示侧边栏（当前配置，推荐）**：

```markdown

# Plurality Wiki - 多意识体百科

（不添加 frontmatter，默认显示侧边栏）
```

### 3. README.md 冲突解决

**问题**：`docs/README.md` 与 `docs/index.md` 都会被 MkDocs 视为首页，导致冲突。

**解决**：

- ✅ 删除 `docs/README.md`
- ✅ 保留根目录 `README.md`（用于 GitHub 项目说明）

## 📁 当前文件结构

```text
docs/
├── index.md              # 首页（Material 增强版，当前使用）
├── index-material.md     # Material 版备份
├── index-simple.md       # 通用版备份
└── （README.md 已删除）

根目录/
└── README.md            # GitHub 项目说明（不冲突）
```

## 🔄 主题切换指南

### 使用 Material 主题（当前）

```bash

# index.md 已经是 Material 版本，无需操作

mkdocs serve
```

访问 `[http://127.0.0.1:8000/`](http://127.0.0.1:8000/`) ✅ 正确的首页 URL

### 切换到 ReadTheDocs / MkDocs 默认主题

```bash

# 1. 备份当前 Material 版本

cp docs/index.md docs/index-material-backup.md

# 2. 使用通用版本

cp docs/index-simple.md docs/index.md

# 3. 切换主题配置

cp mkdocs.yml.readthedocs mkdocs.yml

# 4. 测试

mkdocs serve
```

### 恢复 Material 主题

```bash

# 1. 恢复 Material 版首页

cp docs/index-material.md docs/index.md

# 2. 恢复 Material 配置

cp mkdocs.yml.material-backup mkdocs.yml

# 3. 测试

mkdocs serve
```

## 🎯 最佳实践

### 推荐配置（当前）

- **Material 主题** : 使用增强版首页（index-material.md → index.md）

  - 包含卡片网格、Material 图标、内容标签页
  - 视觉效果现代化
  - 用户体验更好

- **其他主题** : 使用通用版首页（index-simple.md → index.md）

  - 纯 Markdown 语法
  - 兼容性好
  - 降级优雅

### 侧边栏建议

- **隐藏侧边栏** : 适合纯展示型首页（如产品官网）
-**显示侧边栏**（推荐）：适合文档站点，方便导航

当前配置 **显示侧边栏**，用户可以：

- 在左侧导航中快速跳转到不同章节
- 在右侧目录中查看首页结构
- 更符合文档站点的使用习惯

## 🔧 自定义首页布局

### 完全隐藏侧边栏（宽屏展示）

在 `docs/index.md` 开头添加：

```yaml
---
hide:

  - navigation
  - toc

---
```

### 只隐藏右侧目录

```yaml
---
hide:

  - toc

---
```

### 完全显示（当前配置）

```markdown

# Plurality Wiki - 多意识体百科

（不添加 frontmatter）
```

## 📊 URL 对比

| 配置 | 首页 URL | 状态 |
|------|---------|------|
| ❌ `nav: - 首页: index-material.md` | `/index-material/` | 错误 |
| ✅ `nav: - 首页: index.md` | `/` | 正确 |

## ⚠️ 注意事项

### 1. index.md 必须是首页

MkDocs 规范要求：

- 首页文件名必须是 `index.md`
- 放在 `docs/` 目录下
- 在 nav 中引用为 `index.md`

### 2. 主题切换时需要替换首页内容

不同主题需要不同的首页内容：

- Material → 使用 index-material.md
- ReadTheDocs/其他 → 使用 index-simple.md

切换时记得复制对应版本到 index.md：

```bash
cp docs/index-simple.md docs/index.md  # 切换到通用版
cp docs/index-material.md docs/index.md  # 切换到 Material 版
```

### 3. 备份文件的作用

- `index-material.md` - Material 增强版源文件
- `index-simple.md` - 通用版源文件
- 这些备份文件 **不会** 被 MkDocs 构建（除非在 nav 中引用）

## 🎉 修复结果

现在：

- ✅ 首页 URL 正确：`/`
- ✅ 侧边栏正常显示
- ✅ README.md 冲突已解决
- ✅ Material 主题功能完整
- ✅ 支持主题切换

---

**最后更新**: 2025-10-05
