# AI DTC Launcher — 一人公司创业启动器

将「AI 驱动的一人公司 DTC 创业方法论」编码为可执行的操作系统。从蓝海市场发现到产品上架，6 个阶段 + 7 个决策引擎，全流程 AI 辅助。

> 方法论提炼自一个真实的 AI 创业案例：利用 AI 发现普拉提防滑袜蓝海市场，从零到 210 万播放 + 7.19% 转化率的完整商业链路。

## 它能做什么

```
输入: "我想用 AI 做一个赚钱的小生意"
输出: 从选品到上架到出单的全流程执行方案
```

| 阶段 | 做什么 | AI 自动化 | 人工决策 |
|------|--------|----------|---------|
| 1a 蓝海扫描 | 从零发现有潜力的市场品类 | 候选生成 + 多源趋势验证 + 五维评分 | 选定品类 |
| 1b 市场验证 | 深度验证市场可行性 | 规模分析 + 头部梳理 + 供应链检查 | Go/No-Go |
| 2 选品雷达 | 找到具体要卖的产品 | 爆款内容分析 + 商品提取 + 利润测算 | 选定产品 |
| 3 消费者透视 | 理解用户需求和竞品弱点 | 痛点聚类 + 品牌真空检测 + 5维竞品扫描 | 确认差异化方向 |
| 4 品牌建筑师 | 定义品牌调性和视觉 | 画像生成 + 品牌对标 + AI视觉方案 + 命名 | 确认品牌方向 |
| 5 产品落地 | 从设计到供应商到上架 | AI产品图 + 供应链筛选 + 素材包生成 | 确认产品就绪 |
| 6 增长引擎 | 引流和精准投放 | 存量激活MVP + 爆款内容 + 精准投放 | 投放预算 |

## 快速开始

### 安装

将此插件添加到 Claude Code：

```bash
# 从 GitHub 安装
claude plugin install https://github.com/Tina0529/ai-dtc-launcher

# 或克隆到本地后安装
git clone https://github.com/Tina0529/ai-dtc-launcher.git
claude plugin install ./ai-dtc-launcher
```

### 使用

```bash
# 从零发现蓝海市场（无需任何想法）
/ai-dtc-launcher discover

# 验证一个你已有的品类方向
/ai-dtc-launcher validate "瑜伽垫"

# 从上次检查点继续
/ai-dtc-launcher resume pilates-socks

# 查看项目进度
/ai-dtc-launcher status pilates-socks
```

## 核心设计

### 三类模块

| 类型 | 说明 | 数量 |
|------|------|------|
| **阶段模块** (phases/) | 每个业务阶段的执行指南 | 7 个 |
| **决策引擎** (engines/) | 从方法论中萃取的量化决策规则 | 7 个 |
| **输出模板** (templates/) | 标准化的输出格式 | 5 个 |

### 7 个决策引擎

这些是从视频方法论中萃取并编码的「商业直觉」——把经验变成可执行的规则：

| 引擎 | 核心规则 | 用在哪 |
|------|---------|--------|
| **蓝海五维判定** | 增长率/头部集中度/进入门槛/品牌密度/需求稳定性，各有10/7/4/1断点，≥70分=GO | Phase 1a |
| **多源趋势交叉验证** | 全球↑中国↑=跟，全球↑中国平=抢时间差红利，≥3源确认=高置信 | Phase 1a, 2 |
| **爆品潜力评分** | 频率×0.25 + 增长×0.25 + 毛利×0.30 + 竞争×0.20，≥7分=强候选 | Phase 2 |
| **品牌真空检测器** | 用户评论中品牌提及率 <5% = 强品牌真空 | Phase 3 |
| **人群-品牌匹配** | 提取用户画像标签 → 匹配参考品牌 → 借鉴视觉DNA | Phase 4 |
| **三秒病毒法则** | 前3秒≥2种钩子（视觉冲击/痛点共鸣/悬念/利益），AI生成5方案选最优 | Phase 6 |
| **精准投放漏斗** | 自然流量→筛选高完播视频→定向投放高互动人群→ROI>2加投 | Phase 6 |

### 多市场支持

| 市场 | 趋势数据源 | 电商平台 | 供应链 | 投放渠道 |
|------|-----------|---------|--------|---------|
| **中国** (首选) | 百度指数/微信指数/抖音搜索 | 淘宝/拼多多/微信小商店 | 1688 | DOU+/视频号推广/巨量千川 |
| **日本** (扩展) | Yahoo! Japan/楽天/YouTube JP | Amazon JP/楽天/BASE | Alibaba JP | TikTok Ads JP/Yahoo! 広告 |
| **全球** (参考) | Google Trends/TikTok Global | Amazon/Shopify | Alibaba.com | TikTok Ads/Meta Ads |

### 数据采集三种模式

| 模式 | 适用 | 说明 |
|------|------|------|
| **Auto** | B站API、1688、Amazon JP | 工具自动采集 |
| **Semi-auto** | 抖音、小红书 | 用户手动导出/粘贴，AI 分析 |
| **Third-party** | 需规模化数据 | 用户提供蝉妈妈/飞瓜 CSV |

## 文件结构

```
ai-dtc-launcher/
├── .claude-plugin/plugin.json         ← 插件配置
├── README.md                          ← 本文件
├── skills/ai-dtc-launcher/
│   ├── SKILL.md                       ← 主编排器（入口）
│   ├── phases/                        ← 阶段模块
│   │   ├── 01a-market-discovery.md    ←   蓝海扫描
│   │   ├── 01b-market-validation.md   ←   市场验证
│   │   ├── 02-product-radar.md        ←   选品雷达
│   │   ├── 03-consumer-insight.md     ←   消费者透视
│   │   ├── 04-brand-architect.md      ←   品牌建筑师
│   │   ├── 05-product-builder.md      ←   产品落地
│   │   └── 06-growth-engine.md        ←   增长引擎
│   ├── engines/                       ← 决策引擎
│   │   ├── blue-ocean-scorer.md       ←   蓝海五维判定
│   │   ├── trend-crosscheck.md        ←   趋势交叉验证
│   │   ├── hit-product-scorer.md      ←   爆品潜力评分
│   │   ├── brand-vacuum-detector.md   ←   品牌真空检测
│   │   ├── persona-brand-matcher.md   ←   人群-品牌匹配
│   │   ├── 3s-virus-rule.md           ←   三秒病毒法则
│   │   └── precision-funnel.md        ←   精准投放漏斗
│   └── templates/                     ← 输出模板
│       ├── market-scorecard.md        ←   市场评分卡
│       ├── brand-brief.md             ←   品牌简报
│       ├── cost-structure.md          ←   成本结构
│       ├── launch-checklist.md        ←   上线检查清单
│       └── daily-tracker.md           ←   增长日报
```

## 依赖的 Skill

以下 Skill 会在对应阶段被自动调用（需提前安装）：

| Skill | 用途 | 必需? | 来源 |
|-------|------|------|------|
| `ecommerce-searcher` | 电商平台产品搜索和评论采集 | 推荐 | sparticle-toolkit |
| `amazon-japan-shopping` | Amazon JP 产品研究（日本市场） | 可选 | sparticle-toolkit |
| `gemini-imagegen` | Mood board + 产品效果图生成 | 推荐 | compound-engineering |
| `content-scoring` | 内容质量评分和优化 | 推荐 | sparticle-toolkit |
| `ai-video-maker` | 短视频内容自动生产 | 推荐 | sparticle-toolkit |
| `bilibili-uploader` | B站自动发布 | 可选 | sparticle-toolkit |
| `wechat-channels-publisher` | 微信视频号自动发布 | 可选 | sparticle-toolkit |
| `growth-hacker` | AARRR 增长指标框架 | 可选 | sparticle-toolkit |
| `campaign-memory` | 项目持久化追踪 | 推荐 | sparticle-toolkit |
| **`pricing-psychology`** | **定价心理学（锚定/魅力定价/诱饵效应等9大原则）** | **推荐** | **ClawHub** |
| **`competitor-analyst`** | **结构化竞品分析框架（6步分析法）** | **推荐** | **ClawHub** |
| **`tiktok-growth`** | **TikTok/抖音 Hook 公式 + 爆款脚本结构** | **推荐** | **ClawHub** |
| `sourcing-in-china` | Made-in-China.com 供应商搜索（补充 1688） | 可选 | ClawHub |

## 预计执行时间

| 阶段 | AI 时间 | 人工时间 | 合计 |
|------|---------|---------|------|
| Phase 1 (市场发现+验证) | 45-90 min | 15-25 min | ~1.5h |
| Phase 2 (选品) | 20-40 min | 10-15 min | ~45min |
| Phase 3 (消费者透视) | 30-60 min | 15-20 min | ~1h |
| Phase 4 (品牌) | 20-30 min | 15-20 min | ~40min |
| Phase 5 (产品落地) | 30-45 min | 30+ min | ~1-2h |
| Phase 6 (增长) | 持续 | 每日10min | 持续 |
| **总计到上架** | **~3-4h** | **~2-3h** | **~1-2天** |

## License

MIT
