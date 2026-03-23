---
name: ai-dtc-launcher
description: AI 一人公司 DTC 创业启动器。从蓝海市场发现到产品上架，6个阶段+7个决策引擎，全流程 AI 辅助的创业操作系统。支持中国市场（抖音/小红书/拼多多/微信）和日本市场（Amazon JP/楽天/TikTok JP）。当用户说"找蓝海市场"、"DTC创业"、"一人公司"、"选品"、"品牌真空"时激活。
---

# AI DTC Launcher — 一人公司创业启动器

将"AI驱动的一人公司DTC创业方法论"编码为可执行的操作系统。从蓝海市场发现到产品上架，每一步都有 AI 自动化执行 + 决策引擎辅助判断 + 人工检查点把关。

## 入口模式

| 命令 | 说明 | 起始阶段 |
|------|------|---------|
| `/ai-dtc-launcher discover` | 从零发现蓝海市场（无需品类方向） | Phase 1a |
| `/ai-dtc-launcher validate "品类名"` | 验证指定品类是否值得进入 | Phase 1b |
| `/ai-dtc-launcher resume {项目名}` | 从上次检查点继续 | 上次阶段 |
| `/ai-dtc-launcher status {项目名}` | 查看项目仪表盘 | — |

## 执行流程

```
用户启动
    │
    ▼
┌─ Phase 1a: 蓝海扫描 ────────────────┐
│ 自动: AI 生成候选品类 + 多源趋势验证   │
│ 引擎: 蓝海五维判定 + 趋势交叉验证      │
│ 🔴 检查点: 选定 1-2 个品类            │
└──────────────────────────────────────┘
    │ ✅
    ▼
┌─ Phase 1b: 市场验证 ────────────────┐
│ 自动: 市场规模 + 头部玩家 + 供应链      │
│ 输出: Go/No-Go 建议                  │
│ 🔴 检查点: 确认进入此市场              │
└──────────────────────────────────────┘
    │ ✅
    ▼
┌─ Phase 2: 选品雷达 ─────────────────┐
│ 自动: 爆款内容分析 + 商品提取 + 利润测算 │
│ 引擎: 爆品潜力评分                    │
│ 🔴 检查点: 选定 1-3 个产品            │
└──────────────────────────────────────┘
    │ ✅
    ▼
┌─ Phase 3: 消费者透视 ───────────────┐
│ 自动: 痛点聚类 + 品牌真空检测 + 竞品扫描 │
│ 引擎: 品牌真空检测器                   │
│ 🔴 检查点: 确认差异化方向              │
└──────────────────────────────────────┘
    │ ✅
    ▼
┌─ Phase 4: 品牌建筑师 ───────────────┐
│ 自动: 用户画像 + 品牌对标 + 视觉方案    │
│ 引擎: 人群-品牌匹配法                  │
│ 🔴 检查点: 确认品牌方向                │
└──────────────────────────────────────┘
    │ ✅
    ▼
┌─ Phase 5: 产品落地 ─────────────────┐
│ 自动: AI 产品设计 + 供应链 + 素材包     │
│ 🔴 检查点: 确认产品就绪                │
└──────────────────────────────────────┘
    │ ✅
    ▼
┌─ Phase 6: 增长引擎 ─────────────────┐
│ 自动: 存量激活 + 爆款内容 + 精准投放    │
│ 引擎: 三秒病毒法则 + 精准投放漏斗       │
│ 🔴 检查点: MVP 验证 → 投放预算确认     │
└──────────────────────────────────────┘
```

## 项目初始化

当用户首次启动时：

1. **收集用户现有资产信息**：询问用户各平台粉丝数（视频号、B站、抖音、小红书）、是否有营业执照、预算范围，填入 `meta.json` 的 `user_assets` 字段。这些信息将影响后续渠道选择和增长策略。
2. **创建项目数据目录**：

```
data/projects/{项目名}/
├── meta.json          ← 项目状态（当前阶段、决策历史）
├── market-report.md   ← Phase 1 输出
├── product-candidates.md ← Phase 2 输出
├── consumer-insight.md   ← Phase 3 输出
├── brand-brief.md        ← Phase 4 输出
├── product-package.md    ← Phase 5 输出
└── growth-plan.md        ← Phase 6 输出
```

初始 meta.json：
```json
{
  "schema_version": "1.0",
  "name": "{项目名}",
  "created": "{日期}",
  "market": "china",
  "current_phase": "phase-1a",
  "current_step": "step-1",
  "status": "in_progress",
  "phases_completed": [],
  "phase_outputs": {},
  "history": [],
  "key_decisions": [],
  "mvp_thresholds": {
    "min_orders_7d": 30,
    "max_return_rate": 0.15,
    "min_positive_rate": 0.80
  },
  "user_assets": {
    "wechat_video_followers": 0,
    "bilibili_followers": 0,
    "douyin_followers": 0,
    "xiaohongshu_followers": 0,
    "has_business_license": false,
    "budget_range": "unknown"
  }
}
```

## 阶段执行

每进入一个阶段时：

1. 使用 Read 工具加载对应的 `phases/XX.md` 文件
2. 按该文件中的步骤逐步执行
3. 需要决策判断时加载对应的 `engines/XX.md`
4. 需要格式化输出时加载对应的 `templates/XX.md`
5. 完成后更新 `meta.json` 的阶段状态
6. 在检查点暂停，展示结果等待用户确认

## 失败回退路径

```
Phase 1a 全部 <50 分 → 放宽约束重试 → 3轮失败 → 建议 validate 模式
Phase 1b No-Go → 返回 1a 选下一个候选 → 全部用尽 → 重新扫描
Phase 2 全部利润红灯 → 检查定价/采购优化空间 → 返回 1b
Phase 3 品牌提及率 >15% → 转差异化策略 → 无可行方案 → 返回 Phase 2
Phase 6 MVP 未达标 → 诊断流量/转化问题 → 2次失败 → 暂停根因分析
```

## 已有 Skill 集成

| 阶段 | Skill | 用途 |
|------|-------|------|
| 1a, 2 | `ecommerce-searcher` | 电商平台产品搜索 |
| 1a (JP) | `amazon-japan-shopping` | Amazon JP 产品研究 |
| 3 | `ecommerce-searcher` | 电商评论采集 |
| 4, 5 | `gemini-imagegen` | Mood board + 产品效果图生成 |
| 5 | `content-scoring` | 电商素材质量评分 |
| 6 | `ai-video-maker` | 短视频内容生产 |
| 6 | `content-scoring` | 视频内容评分优化 |
| 6 | `bilibili-uploader` | B站自动发布 |
| 6 | `wechat-channels-publisher` | 微信视频号自动发布 |
| 6 | `growth-hacker` | AARRR 指标框架 |
| 全部 | `campaign-memory` | 项目持久化追踪 |

## 数据采集模式

不同平台采用不同采集策略：

| 模式 | 适用平台 | 方式 |
|------|---------|------|
| **Auto** | B站(API)、1688、Amazon JP | 工具自动采集 |
| **Semi-auto** | 抖音、小红书 | 用户手动导出/粘贴，AI 分析处理 |
| **Third-party** | 需要规模化抖音数据 | 用户提供蝉妈妈/飞瓜 CSV，AI 分析 |

自动采集失败时提示："无法自动访问 [平台]，请将数据粘贴过来或上传 CSV 文件。"

## 市场配置

通过 meta.json 的 `market` 字段控制市场适配：

- `"china"`: 使用百度指数/微信指数/抖音/小红书/1688/闲鱼 数据源
- `"japan"`: 使用 Yahoo! Japan/楽天/YouTube JP/Amazon JP/メルカリ 数据源
- `"global"`: 使用 Google Trends/TikTok Global/Amazon Global 数据源
