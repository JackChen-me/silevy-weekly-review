# GuijiOS Weekly Review

自动生成每周复盘周报的 Claude Skill，从 Cowork 和 Claude Code 双端对话记录中提取本周所有工作内容，输出两份报告：

- **对内周报**：给自己看的全面复盘，含成果清单、时间分配、关键决策、下周计划和反思
- **对外周报**：面向公开读者的精选周记，自动隐去敏感信息

## 特性

- **全量数据采集**：覆盖 Cowork（Claude Desktop 桌面端）全部会话（含归档）和 Claude Code（终端 CLI）全部对话，自动去重 Cowork 派生的子进程
- **数据驱动分类**：不预设工作类别，首次运行时从实际对话内容自动聚类，用户确认后持久化；后续运行自动检测新类别
- **敏感信息过滤**：可配置的过滤规则，确保对外周报不泄露财务、人事、运营数据等隐私信息
- **自动验证**：用 subagent 交叉检查事实一致性和信息泄露

## 安装

下载 `GuijiOS-weekly-review.skill` 文件，双击安装到 Claude Desktop。

或者将 `GuijiOS-weekly-review/` 文件夹复制到你的 skills 目录：

```bash
cp -r GuijiOS-weekly-review/ ~/.claude/skills/GuijiOS-weekly-review/
```

## 使用

在 Cowork 或 Claude Code 中输入：

```
写周报
```

```
总结一下这周
```

```
weekly review
```

首次运行时会引导你完成简单配置（身份标签、对外周报格式、敏感信息规则），分类体系由 AI 从你的实际对话数据中自动推断。

## 配置

配置文件 `config.json` 首次运行时自动生成，包含以下可定制项：

| 字段 | 说明 |
|------|------|
| `identity` | 身份标签和对外周报的自我介绍 |
| `categories` | 工作分类（首次运行自动填充，后续自动演进） |
| `external_report` | 对外周报的标题模板、主题数量、写作风格、目标读者 |
| `sensitive_filters` | 敏感信息过滤规则（类别 + 示例） |
| `file_naming` | 输出文件命名模板 |

详见 `references/config-guide.md`。

## 文件结构

```
GuijiOS-weekly-review/
├── SKILL.md                      # 主指令文件
├── README.md                     # 本文件
├── references/
│   └── config-guide.md           # 配置字段详细说明
└── assets/
    └── config-template.json      # 默认配置模板
```

## License

MIT
