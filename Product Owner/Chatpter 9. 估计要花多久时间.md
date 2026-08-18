# 估计要花多久时间
对于一个全新的 system（Greenfield Project），Product Owner 不应该一开始就问 Development Team：

“整个 system 要多少 man-day？”

因为这个阶段需求通常还很模糊，直接估一个总工期，误差可能非常大。

比较成熟的做法是：先估 Scope → 拆 Feature → Refinement → 相对估算 → 用团队速度换成时间 → 加风险范围。

假设公司现在说：

「我们要做一个新的 Taxi Booking System，你告诉我多久可以上线。」

PO 可以这样做。

## Step 1：先定义 MVP，而不是估整个 System

先问：

“第一版上线，最少必须解决什么问题？”

例如 Taxi System 完整版可能有：

Customer App、Driver App、Operation Portal、Payment、Promotion、Membership、Reporting、Dynamic Pricing、Driver Settlement、Notification、GPS Tracking……

如果全部一起估，几乎一定不准。

PO 应该先定义 MVP，例如：

Capability	MVP?
Customer Login	✅
Create Booking	✅
Vehicle Selection	✅
Fare Calculation	✅
Driver Assignment	✅
Booking Status	✅
Payment	✅
Operation Portal	✅
Basic Report	✅
Promotion	❌ Phase 2
Membership	❌ Phase 2
Dynamic Pricing	❌ Phase 2

所以第一件事情不是问：

“System多久？”

而是确定：

“我们现在到底在估哪一个 Scope？”

## Step 2：把 MVP 拆成 Epic

例如：

Taxi Booking MVP


Epic 1 — Account
Epic 2 — Booking
Epic 3 — Pricing
Epic 4 — Driver Assignment
Epic 5 — Trip Management
Epic 6 — Payment
Epic 7 — Operation Portal
Epic 8 — Reporting

这个阶段仍然不要急着算天数。

因为：

Epic 太大，里面的不确定性非常高。

## Step 3：把 Epic Refinement 成 User Story

例如 Booking：

Epic: Booking


US01 Customer selects pickup location
US02 Customer selects destination
US03 System calculates estimated fare
US04 Customer selects vehicle type
US05 Customer confirms booking
US06 System searches available driver
US07 Driver accepts booking
US08 Customer sees driver information
US09 Customer tracks driver arrival
US10 Customer cancels booking

然后 PO + Developer + QA 一起 Refinement。

例如：

Customer cancels booking

大家开始问：

什么时候可以 cancel？


Driver accept 后可以吗？


Driver arrived 还可以吗？


已经开始 trip 呢？


Cancel 有没有 penalty？


Payment 已经扣了怎么办？


Driver 有没有 compensation？

这些问题没有回答之前，这个 Story 根本不适合拿来估时间。

这也是为什么 Refinement 对新 System 特别重要。

## Step 4：Developer 估 Complexity，不是 PO 自己估 Development Time

PO 负责：

What / Why / Priority / Acceptance Criteria

Development Team 负责：

Technical Complexity / Effort / Risk

例如用 Story Point：

Story	SP
Login	3
Select Location	5
Fare Calculation	8
Create Booking	5
Driver Matching	13
Driver Accept	5
GPS Tracking	13
Payment	13
Cancel Booking	8
Basic Report	5

全部 MVP Refinement 后，例如：

Total = 240 Story Points

注意：

240 SP ≠ 240 days。

Story Point 是相对复杂度，不是时间。

Step 5：用 Team Velocity 转成 Sprint

假设团队已经稳定，可以做到：

30 SP / Sprint

而：

MVP = 240 SP

那么：

240÷30=8 sprints

如果：

1 Sprint = 2 weeks

那么：

8×2=16 weeks

初步可以说：

Development 大约需要 16 weeks。

但这里有一个很大的问题。

如果是全新 Team / 全新 System，你可能根本没有 Velocity。

这时候不要假装知道“30 SP”。

## Step 6：全新 Team 没有 Velocity，怎么办？

可以先做 2–3 Sprint Calibration。

例如：

Sprint 1：

Team 完成 21 SP

Sprint 2：

Team 完成 26 SP

Sprint 3：

Team 完成 24 SP

Average：

(21+26+24)÷3≈24SP

之后再重新 Forecast：

240÷24=10 sprints

也就是：

约 20 weeks

所以项目开始时可以给 Management 一个范围，而不是假装给一个精确日期。

例如：

Current forecast: 4–6 months
Confidence: Low
After Sprint 3 we will reforecast based on actual velocity.

这个比说：

“5月17日一定完成。”

专业得多。

## Step 7：不要忘记 Non-Feature Work

这是新 System 最容易漏掉的部分。

240 SP 很可能只包含 Business Features，但新 System 还可能需要：

Architecture
Repository setup
CI/CD
DEV environment
SIT environment
UAT environment
Production environment


Database design
Authentication
Authorization
Logging
Monitoring
Audit trail


Security testing
Performance testing
Data migration
Integration testing


UAT
Bug fixing
Deployment
Production readiness
Training
Documentation

例如 Development 16 weeks，并不代表：

Week 16 就可以 Go Live。

可能实际变成：

Discovery / Refinement      3 weeks
Architecture / Foundation  3 weeks
Feature Development       16 weeks
Integration / Hardening    3 weeks
UAT                        3 weeks
Production Readiness       2 weeks

但这些也不应该简单全部串行相加，因为 Architecture、CI/CD、Testing、Refinement 很多可以跟 Development overlap。

最终可能 Forecast：

约 22–26 weeks 才能 Go Live。

## Step 8：PO 最终应该给 Management 什么？

不要只给：

“6个月。”

我更建议 PO 给：

项目	Forecast
MVP Scope	8 Epics / ~240 SP
Team	5 Developers + 2 QA
Sprint	2 weeks
Expected Velocity	22–28 SP
Development	~9–11 Sprints
Expected Go-Live	~5–6 months
Confidence	Low / Medium
Biggest Risks	Payment、GPS、3rd-party integration
Reforecast	After Sprint 2–3

这样 Management 知道：

这个数字是怎么来的，也知道什么东西可能让它改变。

最重要的概念：Estimate ≠ Commitment

新 System 的 Forecast 应该随着项目越来越清楚而越来越准确。

可以想成一个漏斗：

Idea
│
│   4–8 months
│   Confidence: Very Low
▼
Discovery
│
│   5–7 months
│   Confidence: Low
▼
Refinement
│
│   22–28 weeks
│   Confidence: Medium
▼
Sprint 1–3
│
│   Actual Velocity available
▼
Forecast
│
│   24–26 weeks
│   Confidence: Higher
▼
Go Live

所以 PO 的工作不是“猜 Developer 要做几天”。

PO 真正要建立的是：

Scope → Backlog → Refinement → Estimate → Velocity → Forecast → Reforecast

这套机制。

尤其是全新 System，我会把管理层问的 “多久可以完成？” 转换成：

“以目前已知的 MVP scope，我们预计需要 X–Y 个月；目前 confidence 是 Low。完成 Discovery/Refinement 和前 2–3 个 Sprint 后，我们会根据实际 velocity 更新 forecast。”

这才是比较可靠的 Product Owner estimation 方法。

可是当business 做tender时需要相对准确的时间

对，这就是 Tender / RFP 项目和一般 Agile Product 最大的冲突之一。

Tender 阶段 Business 往往必须写：

项目价格 RM X
Implementation：6 months
UAT：1 month
Go-Live：Month 8

但这时候 Developer 甚至还没有真正做 Refinement。

所以 Tender 不能等到 Sprint 有 Velocity 才估。这里需要另外一套 Pre-Sales Estimation / Tender Estimation 方法。

Tender 阶段，我会这样估

核心流程是：

Tender Requirement → Scope Boundary → WBS → Complexity Estimate → Dependency/Risk → Resource Model → Schedule → Contingency

重点是：Tender 不应该直接从「200个 requirements」跳到「8个月」。

### 1. 先把 Tender Requirement 做 Requirement Decomposition

例如客户 Tender 写：

System shall provide online taxi booking capability.

这句话不能直接估。

PO / BA / Tech Lead 要拆：

Taxi Booking


├── Search
│   ├── Pickup location
│   ├── Destination
│   └── Vehicle availability
│
├── Pricing
│   ├── Base fare
│   ├── Distance fare
│   ├── Toll
│   └── Surcharge
│
├── Booking
│   ├── Create booking
│   ├── Modify booking
│   ├── Cancel booking
│   └── Booking history
│
├── Driver
│   ├── Driver matching
│   ├── Accept / reject
│   └── Driver tracking
│
└── Notification
    ├── Push
    ├── SMS
    └── Email

Tender estimation 的准确度，很大程度取决于你拆得够不够细。

### 2. 建立 Estimation Sheet

这时候不一定要用 Story Point。

Tender 阶段我反而比较推荐 Person-Day / Person-Hour + Complexity，因为最终 Business 需要 Cost 和 Timeline。

例如：

Module	BE	FE	Mobile	QA	Total
Login	3	2	2	2	9
Booking	12	8	10	8	38
Pricing	8	3	3	5	19
Driver Matching	15	5	10	8	38
Payment	10	5	5	8	28
Reporting	8	8	0	5	21
Total	56	31	30	36	153 PD

但 153 PD 不能直接拿来算项目 Timeline。

因为还有很多东西没算。

### 3. 加上「看不到的工作」

Tender 最容易亏钱就在这里。

Business Requirement 通常只写 Feature。

但 Development 实际还有：

工作	Estimate
Business Features	153 PD
Architecture / Solution Design	15 PD
DB Design	8 PD
Environment / CI/CD	12 PD
Integration	20 PD
Security	10 PD
Performance Testing	8 PD
UAT Support	15 PD
Deployment	5 PD
Documentation	10 PD
Training / Handover	5 PD
PM / Coordination	20 PD
Subtotal	281 PD

所以原本看起来：

153 PD

实际上可能已经：

281 PD

这就是为什么很多 Tender Project 最后会 overrun。

### 4. 再加 Risk Contingency

全新 System 一定有 Unknown。

不要把 Unknown 当成不存在。

例如：

Requirement clarity：Medium
Third-party integration：High
Technology：Low
Data migration：Medium
Customer UAT：High

可以根据风险加 contingency。

例如：

Base Estimate = 281 PD
Risk Contingency = 20%

那么：

281×1.20=337PD

Tender Commercial Estimate：

≈ 337 Person-Days

注意这个 20% 不是随便「老板觉得应该加20%」。

最好建立 Risk Register：

Risk	Probability	Impact	Allowance
Payment API unclear	High	High	+10 PD
Legacy migration	Medium	High	+12 PD
Customer API delay	Medium	Medium	+6 PD
Requirement ambiguity	High	Medium	+15 PD

这样你以后甚至可以解释为什么 quotation 是这个数字。

### 5. 337 PD ≠ 337 ÷ 5人 = 67天

这是 Tender estimation 另一个非常常见的错误。

假设：

337 PD
5 Developers

Business 很容易算：

337÷5≈67working days

然后：

「3个月可以完成啦。」

实际上不成立。

因为工作有 dependency：

Requirement
     ↓
Solution Design
     ↓
Database / API
     ↓
Backend
     ↓
Frontend
     ↓
Integration
     ↓
Testing
     ↓
UAT

很多工作不能完全 parallel。

而且团队不是：

5个人 × 每天100% coding

还有 meeting、refinement、bug fixing、code review、deployment、support、leave 等。

所以 Effort 和 Duration 必须分开估。

### 6. Tender 要做 Resource Loading

例如你的 Team：

1 Solution Architect
1 Tech Lead
3 Backend
2 Frontend
2 Mobile
2 QA
1 DevOps
1 BA
1 PM

然后排真正的 timeline：

Month        1    2    3    4    5    6    7    8


Discovery   ███


Design      ███  █


Infra       ███  ███


Backend          ███  ███  ███  ███


Frontend              ███  ███  ███


Mobile                ███  ███  ███


Integration                     ███  ███


SIT                                   ███


UAT                                        ███


Go-Live                                         ★

这时候才开始得到：

Estimated project duration = 8 months

而不是拿 PD 除人数。

### 7. Tender 最重要的是 Assumptions

这其实比 Estimate 本身还重要。

假设你报价：

RM800k / 8 months

一定要同时写清楚：

Assumption：

Maximum 3 external integrations


Customer API documentation available before development


Maximum 500 concurrent users


No legacy data migration


English language only


One production environment


Customer provides UAT users


UAT duration limited to 4 weeks


Maximum 2 UAT cycles


Requirement changes after sign-off
will go through Change Request

为什么？

因为客户 Tender 可能只写：

“Integrate with existing payment system.”

你估：

10 PD

后来才发现：

Payment Gateway
      +
Bank Reconciliation
      +
Refund
      +
Partial Refund
      +
Settlement
      +
Chargeback
      +
Finance Report

这已经完全不是原本的 10 PD。

如果没有 Assumption / Scope Boundary，公司就只能自己吞掉。

### 8. 所以 Tender 的「准确」其实不是一个数字

Tender 不可能做到：

“我们准确知道需要 183 天。”

真正应该做到的是：

在目前 information 下，建立一个 defensible estimate。

也就是别人问：

为什么8个月？

你可以一路解释：

Tender Requirements
        ↓
Requirement Decomposition
        ↓
WBS
        ↓
Effort Estimation
        ↓
281 PD
        ↓
Risk Assessment
        ↓
337 PD
        ↓
Resource Loading
        ↓
Dependency / Critical Path
        ↓
Project Schedule
        ↓
≈ 8 Months

而不是：

Tech Lead 看了一下，觉得大概6个月。

还有一个很重要的角色边界

如果你未来作为 Product Owner 遇到 Tender，我不会建议 PO 一个人承担 estimation。

Tender 应该是一个 Cross-functional estimation：

PO / BA 负责 Scope、Business Rules、Acceptance Boundary；Architect / Tech Lead 负责 Technical Solution、Complexity、Integration；Developers / QA / DevOps 负责各自 Effort；PM 负责 Resource Loading、Dependency、Timeline；Commercial / Finance 再把 PD、License、Cloud、Vendor、Contingency 转成 Tender Price。

所以 Business 问：

“这个 Tender 可以承诺 8 个月吗？”

PO 不应该自己回答 Yes/No。

应该经过：

Scope → Technical Estimate → Resource Plan → Risk → Schedule → Commitment

之后才决定是否承诺。

这也解释了为什么 Tender estimation 和 Sprint estimation 是两层不同的东西：Tender 阶段用 WBS + PD + Resource Loading 做 Baseline Estimate；中标进入 Delivery 后，再把 WBS 转成 Product Backlog，用 Story Point + Velocity 持续 Reforecast。两者不是互相取代，而是前后衔接。