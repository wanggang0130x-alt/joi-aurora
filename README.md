# Joi Aurora 量化交易系统
> Joi Aurora Quantitative Trading System

[![OpenClaw Skill](https://img.shields.io/badge/Platform-OpenClaw-blue.svg)](https://openclaw.ai)
[![Version](https://img.shields.io/badge/Version-2.0.0-green.svg)]()
[![Risk Level](https://img.shields.io/badge/Risk-High-red.svg)]()

---

## 系统简介

Joi Aurora 是一套**多Agent量化交易与投资决策系统**，专为 AI Agent 团队设计。

核心模块：
- 📊 **市场分析Agent** — 实时监控市场价格、宏观背景、流动性
- ⚖️ **风险控制Agent** — Half-Kelly仓位计算、硬性规则核查
- 📈 **信号引擎** — 生成可执行交易信号（方向/止损/止盈/信心等级）
- 🔄 **编排器** — 协调三大模块，按评审闭环运作

---

## 适用场景

- Polymarket 预测市场量化策略
- BTC/ETH 短线信号检测（5min/15min）
- 外汇、宏观事件驱动交易
- 投资组合风险监控
- 仓位计算与管理系统

---

## 核心功能

### 市场分析
- 实时价格监控与趋势判断
- 宏观背景分析（VIX、美联储、通胀数据）
- 流动性扫描（Polymarket $5000+ 市场）
- 恐慌/贪婪指数监控

### 风险控制
- **Half-Kelly 仓位公式**：
  ```
  EV = p × (1 - market) - (1 - p) × market
  Kelly = EV / 盈利比例
  Half-Kelly = Kelly × 0.5
  最终仓位 = min(Half-Kelly × 总资金, 总资金 × 5%)
  ```
- **硬性规则**（不可绕过）：
  - 单笔仓位 ≤ 本金的 5%
  - 单日亏损 ≤ 本金的 5%
  - 连续 3 次亏损 → 当日停止交易
  - 情绪评分 < 6 → 建议等待
  - EV ≤ 0 → 禁止入场

### 信号分级
| 等级 | 条件 | 操作 |
|------|------|------|
| 🟢 A级 | EV > 5%，信心 ≥ 4/5 | 可执行，通知即可 |
| 🟡 B级 | EV 2-5%，信心 3/5 | 需评审后执行 |
| 🔴 C级 | EV < 2% 或信心 < 3/5 | 不建议，需额外说明 |

---

## 评审闭环

所有信号交易必须经过：

```
信号生成 → review-qa评审 → 编排器决策 → 人工确认 → 执行 → 复盘记录
```

**Level 1**：自动监控/计算，无需干预
**Level 2**：B级以上信号，强制评审
**Level 3**：大仓位（≥10%本金），三方交叉审核

---

## 快速开始

### 在 OpenClaw 中加载技能

将 `SKILL.md` 内容加载到支持 OpenClaw 的 AI Agent 中即可使用。

### 常用指令

| 查询类型 | 指令示例 |
|---------|---------|
| 市场分析 | `分析市场 BTC 1小时` |
| 仓位计算 | `计算仓位 BTC 做多 信心4 止损3%` |
| 生成信号 | `生成信号 ETH 做多 信心4` |
| Polymarket扫描 | `扫描 Polymarket 机会` |
| BTC短线 | `BTC 5分钟分析` |

---

## 文件说明

```
skill-joi-aurora/
├── SKILL.md        # OpenClaw 技能主文件（含完整系统说明）
├── README.md       # 本文件
└── metadata.json   # 技能元数据
```

---

## 策略说明

### 策略A — Polymarket 中长期
- 扫描流动性 $5000+ 市场
- EV > 2% 才入场
- 单笔不超过本金 10%

### 策略B — BTC 短线（5min/15min）
- 配合 PolyCop Bot 使用
- 信心等级 1-5 影响 edge 调整
- 严格止损，不扛单

---

## 风险提示

⚠️ **量化交易存在极高风险，本系统仅供决策辅助，不构成投资建议。**

- 请在充分了解风险后使用
- 建议先在模拟盘测试
- 遵守硬性仓位规则，不要超仓
- 连续亏损时必须停下来复盘

---

## 更新日志

### v2.0.0（2026-04-02）
- 整合 Claude Code 评审闭环机制
- 新增 review-qa 评审流程
- 标准化信号格式和交付标准

### v1.0.0（2026-03-29）
- 初始版本
- 四大核心模块上线

---

## 作者

**PawPicksCo AI Team**  
跨境电商 AI 团队 · OpenClaw Agent System

---

*本系统作为 OpenClaw Agent Skill 发布，可被其他 AI Agent 加载使用*
