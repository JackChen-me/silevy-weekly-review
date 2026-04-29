# 配置指南

`config.json` 是 silevy-weekly-review 的个性化配置文件。首次运行时由 skill 引导用户创建，之后每次运行自动读取。

用户也可以手动编辑此文件来调整周报的各项设置。

## 配置字段说明

### identity（用户身份）

用于对外周报的开头介绍。

```json
{
  "identity": {
    "label": "独立开发者",
    "intro_blockquote": "一个从大厂出来的产品人，正在用 AI 做独立开发。"
  }
}
```

- `label`：一个简短的身份标签，用于内部分类参考
- `intro_blockquote`：对外周报开头的一句话自我介绍（blockquote 格式）

### categories（工作分类）

工作分类**不需要用户手动预设**。首次运行时，skill 会从实际对话数据中自动聚类出 5-8 个类别，展示给用户确认后写入此字段。

后续运行时以此为基础框架，同时自动检测是否需要新增类别。

初始状态（首次运行前）：
```json
{
  "categories": []
}
```

首次运行后，skill 会自动填充为类似这样的结构：
```json
{
  "categories": [
    {
      "name": "产品开发",
      "keywords": ["开发", "部署", "bug", "功能", "代码", "上线", "测试"],
      "added_at": "2026-03-23",
      "source": "auto"
    },
    {
      "name": "内容创作",
      "keywords": ["文章", "公众号", "小红书", "视频", "脚本"],
      "added_at": "2026-03-23",
      "source": "auto"
    }
  ]
}
```

- `name`：类别名称，可由用户重命名
- `keywords`：从对话中提炼的代表性关键词，帮助后续运行时快速归类
- `added_at`：该类别首次出现的日期
- `source`：`"auto"`（AI 推断）或 `"user"`（用户手动添加）

用户也可以随时手动编辑此字段来增删或重命名类别。

### external_report（对外周报格式）

控制对外周报的标题、风格和结构。

```json
{
  "external_report": {
    "title_pattern": "周记 #{{number}}｜{{date_range}}",
    "topic_count": "3-5",
    "style_notes": "说人话，不讲道理只说事实，有具体细节和数字。每个主题末尾提炼一个加粗的可复用观点。",
    "closing_section": "下周干什么",
    "target_audience": "独立开发者和创业者"
  }
}
```

- `title_pattern`：标题模板，`{{number}}` 会被替换为自动递增的期数，`{{date_range}}` 替换为日期范围
- `topic_count`：每期选择的主题数量范围
- `style_notes`：写作风格的额外要求
- `closing_section`：结尾段落的标题
- `target_audience`：目标读者画像，影响内容选择和表达方式

### sensitive_filters（敏感信息过滤）

定义对外周报中需要隐去的信息类别。

```json
{
  "sensitive_filters": [
    {
      "category": "投资信息",
      "description": "具体投资标的、金额、收益",
      "examples": ["买了XX股票", "期权收益XX万"]
    },
    {
      "category": "招聘细节",
      "description": "候选人姓名、面试评价、薪资",
      "examples": ["面试了张三", "给XX开了30K"]
    },
    {
      "category": "运营数据",
      "description": "具体粉丝数、收入、转化率",
      "examples": ["公众号涨了500粉", "本月收入XX"]
    },
    {
      "category": "安全相关",
      "description": "VPN 配置、密钥、内部系统地址",
      "examples": ["服务器IP", "API key"]
    }
  ]
}
```

每个过滤规则包含类别名、描述和示例，帮助 AI 准确识别需要隐去的内容。

### file_naming（文件命名）

```json
{
  "file_naming": {
    "internal": "周报_对内_{{start_date}}-{{end_date}}.md",
    "external": "周报_对外_{{start_date}}-{{end_date}}.md",
    "date_format": "YYYYMMDD"
  }
}
```

## 完整配置示例

参见 `assets/config-template.json`。
