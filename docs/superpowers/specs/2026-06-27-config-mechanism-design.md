# arm-learn 配置机制与英文文档自动翻译

**日期:** 2026-06-27
**状态:** 已实现

## 概述

为 arm-learn 项目增加基于 YAML 配置文件的配置机制，使技能（skills）可以根据配置项改变行为。首个配置项：ingest 英文文档时自动生成中文翻译副本。

## 动机

- 当前项目行为硬编码在各技能文件中，无法按需调整
- 英文原始文档在 wiki 中以中文撰写，但原始英文内容没有中文副本供参考
- 需要一个统一、可扩展的配置入口

## 设计

### 配置文件

**位置:** `schema/config.yaml`
**格式:** YAML（与现有 `schema/sources.yaml` 一致）

```yaml
ingest:
  translate_to_chinese: false
```

- 按功能域分组（`ingest`、未来可扩展 `search`、`lint` 等）
- 默认值为 `false`，用户手动开启
- 所有技能在 "Before You Begin" 阶段读取此文件

### 翻译输出目录

**位置:** `translations/`
**结构:** 镜像 `raw/` 的归档子目录

```
translations/
  articles/    # 英文文章的中文翻译
  docs/        # 英文文档的中文翻译
  papers/      # 英文学术论文的中文翻译
```

翻译文件命名：原始文件名加 `-zh` 后缀。

### 原始文件增加语言元数据

search 技能在 Capture 阶段保存文件时，增加 `**Language:**` 字段。

### Ingest 流程变更

在 Survey（步骤1）和 Context Loading（步骤2）之间插入翻译步骤（1.5）：检查配置和语言元数据，满足条件时生成中文翻译到 `translations/`。

### 受影响文件

| 文件 | 变更类型 | 说明 |
|------|----------|------|
| `schema/config.yaml` | 新建 | 配置文件 |
| `translations/` | 新建 | 翻译输出目录 |
| `schema/CLAUDE.md` | 修改 | 增加配置说明和目录布局 |
| `schema/prompts/ingest.md` | 修改 | 增加翻译步骤（1.5） |
| `.claude/skills/search.md` | 修改 | 增加 Language 字段和配置读取 |
| `.claude/skills/ingest.md` | 修改 | 增加配置读取 |
| `.claude/skills/lint.md` | 修改 | 增加配置读取 |
