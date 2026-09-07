# Hi, I'm 王俊麒 👋

亞洲大學資訊工程學系學生，主要專注於 **Backend / Software Engineering**。

我目前的專案方向涵蓋後端系統、資料完整性、可重現性、自動化測試，以及 AI / Machine Learning 應用。比起只完成可以執行的 Demo，我更重視系統的**正確性、可驗證性與工程可靠性**。

## Featured Projects

### AI Trading Platform

**Python · FastAPI · PostgreSQL · SQLAlchemy · Alembic · Docker · Next.js**

以可重現、可稽核與 deterministic execution 為核心的交易分析與回測平台。

* 使用 PostgreSQL constraints 與 triggers 保護交易 lifecycle、execution evidence 與歷史資料
* 建立 strategy、configuration、dataset、source 與 run 的 canonical identity，確保回測結果可重現
* 使用 closed-candle、cutoff 與 multi-timeframe alignment 降低 look-ahead bias
* OpenAI 僅作為受限制的二次驗證層，不能自行修改方向、Entry、TP 或 SL
* 建立 Backend、PostgreSQL integration、Frontend 與 Browser testing 的完整 CI quality gates

[查看專案](https://github.com/wangj6231/ai-trading-platform)

---

### WoundCare System

**Python · PyTorch · YOLO · scikit-learn · FastAPI**

傷口影像分類與照護輔助研究系統，重點放在資料品質、模型驗證與避免 Data Leakage。

* 發現原始 98.34% cross-validation 結果受到 duplicate-image leakage 影響
* 使用 MD5 content grouping 與 GroupKFold 重建 leakage-free evaluation protocol
* 25 次 leakage-free development evaluation：Accuracy **87.40% ± 2.78%**
* 一次性 locked blind test：**46 / 48（95.83%）**
* AI 分析結果必須經人工確認，不直接取代醫療人員判斷

[查看專案](https://github.com/wangj6231/woundcare-system)

## Tech Stack

**Programming**
Python · JavaScript · SQL · HTML/CSS

**Backend & Database**
FastAPI · PostgreSQL · SQLAlchemy · REST API

**Infrastructure**
Linux · Ubuntu Server · Docker · SSH · Proxmox VE · TrueNAS

**AI / ML**
PyTorch · YOLO · scikit-learn · Pandas

**Development & Testing**
Git · GitHub · Pytest · GitHub Actions

## About Me

* 🎓 亞洲大學 資訊工程學系｜預計 2027 年畢業
* 💻 求職方向：Backend Engineer / Software Engineer
* 📍 Taiwan
* 🔧 對後端系統、資料完整性、可靠性與 AI 應用有實作經驗

---

### English

Computer Science student at Asia University, Taiwan, focused on **Backend & Software Engineering**.

My projects emphasize backend architecture, reproducibility, data integrity, automated testing, and applied AI/ML.

Featured work:

* [AI Trading Platform](https://github.com/wangj6231/ai-trading-platform)
* [WoundCare System](https://github.com/wangj6231/woundcare-system)
