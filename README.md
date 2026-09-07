# AI Trading Platform

**Reliability-focused trading analysis and backtesting platform built with FastAPI, PostgreSQL and Next.js.**

這是一個以 **可重現（reproducible）**、**可稽核（auditable）** 與 **安全失敗（fail-closed）** 為核心的 AI 輔助技術分析平台。系統提供類似簡化版 TradingView 的分析介面，產生並保存研究訊號，但**不連接券商、不管理資金，也不執行真實交易**。

> **Current status — Engineering baseline complete.**
> 決定性分析引擎、風險檢查、可選的 OpenAI 二次驗證、PostgreSQL 不可變稽核軌跡、回測框架與 Next.js 分析介面皆已完成工程基線。BTCUSDT／ETHUSDT 使用 Binance 公開 Spot Kline API 的已收盤 OHLCV；沒有可靠行情來源時系統會明確拒絕，而不是補造價格。

## Engineering Highlights

| 面向                           | 實作成果                                                                                                                 |
| ---------------------------- | -------------------------------------------------------------------------------------------------------------------- |
| **Backend architecture**     | FastAPI、Pydantic、SQLAlchemy、Alembic、PostgreSQL 16；API、backtesting、database、engines、market data、schemas 與 services 分層 |
| **Database integrity**       | PostgreSQL `CHECK` 與 trigger 保護 lifecycle、execution evidence、snapshot 與 AI-validation evidence，包含直接 SQL 改寫防護         |
| **Reproducible backtesting** | Dataset、strategy、configuration、source 與 run 使用 canonical identity；分析與回測共用決定性引擎                                       |
| **Temporal correctness**     | 僅使用已收盤 K 線，處理 cutoff、多週期對齊與 delayed confirmation，避免 look-ahead bias / repainting                                     |
| **Bounded AI**               | OpenAI 只可確認、拒絕或降低既有候選信心，不得創造方向或改寫 Entry／TP／SL；停用 AI 時核心流程仍可運作                                                        |
| **Full-stack quality**       | Next.js／TypeScript 儀表板、request-race protection、明確 unavailable / no-signal 狀態，以及 CI、單元、整合與瀏覽器測試                       |

## Verification Snapshot

| Quality gate                      |                                                  Result |
| --------------------------------- | ------------------------------------------------------: |
| Backend tests                     |                                          **899 passed** |
| Real PostgreSQL integration tests |                                          **109 passed** |
| Backend line coverage             |                                              **90.90%** |
| Frontend unit/component tests     |                                           **69 passed** |
| Real Chromium browser cases       |                                           **74 passed** |
| Static / build gates              | Ruff, mypy, TypeScript, ESLint, production build passed |

這些數字驗證的是**工程規則、資料完整性與回歸防護**，不代表策略獲利、真實成交品質或 production trading readiness。

## Architecture at a Glance

```text
Market Data
    ↓
Deterministic Analysis Engine
(Indicators → Structure → SMC/ICT)
    ↓
Risk Engine
    ↓
Optional Bounded AI Validation
    ↓
Final Signal
    ↓
PostgreSQL Audit Trail / Backtest / Statistics
    ↓
Next.js Analysis Dashboard
```

### Engineering case study: performance without changing semantics

P3 incremental replay 在完整輸出差異測試下維持與 reference path 的語意等價：R1 共 **1,440 個 cutoff 全部一致**，量測整體吞吐約提升 **2.9×**。但後段 evaluation cost 仍持續成長，因此結果保留為 `PERFORMANCE_STILL_INSUFFICIENT`，沒有為了漂亮數字改動已凍結的策略、風險或執行規則。

**深入閱讀：** [Project Status](PROJECT_STATUS.md) · [Verification](VERIFICATION.md) · [Security](SECURITY.md) · [P3 Engineering Report](experiments/r1e_p3_incremental/P3_REPORT.md)
