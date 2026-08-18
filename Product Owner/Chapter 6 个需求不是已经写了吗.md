番外篇：Step 6 — Refinement
# 《“这个需求不是已经写了吗？”》
故事背景

公司正在开发一个巴士售票系统。

目前乘客可以：

搜索巴士 → 选择班次 → 选择座位 → 付款 → 获得车票

Business Team 突然提出一个新需求：

“我们要支持 Promo Code。”

于是 PO 很快建立了一张 Jira Ticket：

User Story

As a passenger,
I want to apply a promo code,
so that I can get a discount.

PO 看着 Ticket：

“写好了，可以进 Sprint 了。”

Developer 却说：

“等一下……
Promo Code 到底怎么算？”

于是故事正式开始。

## 第一幕：一句 User Story，背后其实有几十个问题

PO：

“不是很简单吗？
用户输入 Promo Code，然后扣 Discount。”

Developer：

“假设票价 RM100。”

Promo Code = SAVE20

“到底是：

RM100 - RM20

还是：

RM100 - 20%

？”

PO：

“20%。”

Developer：

“Maximum discount 呢？”

PO：

“什么意思？”

Developer：

“如果有人买 RM1,000 的票：

RM1,000 × 20%
= RM200 discount

公司真的愿意给吗？”

PO：

“……”

这就是 Refinement 开始发挥作用的地方。

Refinement 不是：

“把 Jira Ticket 写漂亮一点。”

而是：

把一个模糊的 Business Idea，逐渐变成 Development Team 可以安全开发的需求。

## 第二幕：开始 Refinement

于是 PO 安排了一场 Refinement Meeting。

参与者：

PO
Business
Developer
QA
UI/UX
Tech Lead

屏幕上显示：

SAVE20 Promo Code

PO：

“我们今天不是决定怎么写 Code。”

“我们要先确认：

这个需求到底应该怎么工作？

”

## 第三幕：先确认 Happy Path

PO 在白板写：

Ticket Price = RM100
Promo Code = SAVE20
Discount = 20%
Maximum Discount = RM30

那么：

RM100 × 20%
= RM20


Final Price
= RM100 - RM20
= RM80

所有人同意。

PO 写下第一个 Acceptance Criteria：

Given
Passenger has selected a RM100 ticket


When
Passenger enters valid promo code SAVE20


Then
System applies 20% discount


And
Final ticket price becomes RM80

这就是：

Happy Path

也就是正常情况。

但 Refinement 绝对不能停在这里。

## 第四幕：QA 开始“攻击”需求

QA：

“如果用户输入错误 Promo Code 呢？”

例如：

SAVE200

PO：

“显示 Invalid Promo Code。”

于是增加：

Scenario 2 — Invalid Code
Given
Passenger is on payment page


When
Passenger enters an invalid promo code


Then
System must not apply discount


And
Display:


"Invalid promo code"

QA：

“如果 Promo Code 已经过期？”

例如：

Promo Start:
1 Aug


Promo End:
10 Aug


Today:
14 Aug

于是：

Promo Code Expired

系统应该显示：

Promo code has expired.

## 第五幕：Developer 开始寻找 Business Rule

Developer：

“一个 Promo Code 可以无限使用吗？”

Business：

“不行，每个 Customer 只能用一次。”

Developer：

“怎么认 Customer？”

Business：

“Account。”

Developer：

“如果 Guest Checkout 呢？”

Business：

“……”

这就是 Refinement 很重要的原因。

一个 Business Requirement：

“每个 Customer 只能用一次。”

技术上其实可能完全不够。

因为系统必须知道：

Customer Identity

到底是什么。

可能是：

User ID
Email
Phone Number
IC Number
Payment Card

不同选择会产生完全不同的系统设计。

## 第六幕：PO 开始建立 Business Rules

经过讨论，团队决定：

BR01
Promo Code 有 Start Date


BR02
Promo Code 有 End Date


BR03
Promo Code 可以是 Percentage Discount


BR04
Promo Code 可以有 Maximum Discount


BR05
每个 Registered User 只能使用一次


BR06
Guest User 不能使用 Promo Code


BR07
Promo Code 只适用于特定 Route


BR08
Promo Code 不能与其他 Promotion 同时使用

原本只有一句：

“Support Promo Code”

经过 Refinement 后，已经开始变成真正的 Product Rule。

## 第七幕：突然发现 Scope 比想象中大

Developer：

“BR07 说 Promo Code 只适用于特定 Route。”

PO：

“对。”

Developer：

“那么 Admin 要在哪里设 Route？”

现场突然安静。

因为原本大家只想到：

Passenger 输入 Promo Code

却忘记 Promo Code 是谁建立的。

于是系统其实需要：

Admin Portal
      ↓
Create Promo
      ↓
Select Route
      ↓
Set Start Date
      ↓
Set End Date
      ↓
Set Discount
      ↓
Set Usage Limit

于是一个“小小 Promo Code”需求开始变成：

Customer Side
+
Admin Side
+
Database
+
Validation Engine
+
Reporting
## 第八幕：PO 做出最重要的决定——拆 Story

PO：

“这个 Story 太大了。”

“不要一个 Ticket 做完全部。”

于是拆成：

Story 1
Admin can create Promo Code


Story 2
Admin can configure Promo validity period


Story 3
Admin can configure applicable routes


Story 4
Passenger can apply Promo Code


Story 5
System validates Promo eligibility


Story 6
System records Promo usage


Story 7
Admin can view Promo usage report

这就是 Refinement 其中一个非常重要的动作：

Story Splitting

因为 Developer 不应该看到：

Build Promotion System

这种巨大 Ticket。

应该看到：

一个 Sprint 可以完成、测试、验收的小 Story
## 第九幕：Tech Lead 发现 Dependency

Tech Lead：

“Passenger Apply Promo 不能先做。”

PO：

“为什么？”

Tech Lead：

“因为它依赖 Promo Configuration。”

于是画：

Admin Create Promo
        ↓
Promo Rule
        ↓
Promo Validation
        ↓
Apply Promo
        ↓
Promo Usage Tracking

这时候 PO 才发现：

Story 有 Dependency。

因此 Backlog Order 也应该调整。

## 第十幕：估 Story Point

Refinement 进入 Estimation。

Developer 看 Story：

Passenger can apply Promo Code.

Team 讨论后认为：

UI                 Small
API                Medium
Validation         Medium
Database           Small
Testing            Medium

最后估：

5 Story Points

另外一个 Story：

Promo eligibility engine

因为涉及：

Date Rule
Route Rule
Customer Rule
Usage Rule
Discount Rule

团队估：

8 Story Points

注意：

Story Point 不是 PO 自己定。

通常由：

Development Team

评估复杂度。

## 第十一幕：发现一个 Story 还是太大

团队看到：

Promo Eligibility Engine — 13 Points

Developer：

“这个太大。”

于是继续拆：

Promo Date Validation
        3


Promo Route Validation
        3


Promo Customer Validation
        5


Promo Usage Validation
        3

Refinement 的目标之一就是：

把“大块需求”不断切成可以控制的小块。

## 第十二幕：Definition of Ready

PO 最后问：

“现在这个 Story 可以进 Sprint 吗？”

团队检查：

User Story
✓


Acceptance Criteria
✓


Business Rules
✓


UI Design
✓


API Dependency
✓


Edge Cases
✓


Story Point
✓


Dependency
✓


Test Scenario
✓

全部清楚以后，这个 Story 才叫：

Ready

也就是常说的：

Definition of Ready — DoR
Refinement 到底在做什么？

可以把整个过程理解成：

Business Idea
      ↓
User Story
      ↓
Refinement
      ↓
Clarify Requirement
      ↓
Find Edge Cases
      ↓
Define Business Rules
      ↓
Identify Dependencies
      ↓
Split Story
      ↓
Write Acceptance Criteria
      ↓
Estimate Story Point
      ↓
Ready for Sprint

所以 Refinement 不是单纯：

“开会讨论 Ticket。”

真正目的其实是降低：

Unknown
一个很重要的概念：Refinement 是不断减少 Unknown

刚开始：

Requirement:


"Support Promo Code"

可能是：

Unknown = 80%
Known = 20%

经过第一次 Refinement：

Unknown = 40%
Known = 60%

第二次讨论：

Unknown = 15%
Known = 85%

最后：

Unknown ≈ 可接受程度

才进入 Sprint。

因为真正危险的是这种情况：

Sprint 开始
      ↓
Developer 开发
      ↓
突然发现 Business Rule 不清楚
      ↓
问 PO
      ↓
PO 问 Business
      ↓
Business 还要讨论
      ↓
Developer Blocked
      ↓
Sprint Delay

很多公司所谓：

“Developer 做得很慢。”

实际上可能根本不是 Developer 慢。

而是：

Backlog 没有 Refinement 好。

PO 在 Refinement 最重要的 8 个检查

以后你拿任何 User Story，都可以问：

Who？
谁使用？
Why？
解决什么 Business Problem？
Happy Path？
正常流程是什么？
Edge Case？
异常情况是什么？
Business Rule？
有哪些限制？
Dependency？
需要其他 System / API / Story 吗？
Acceptance Criteria？
怎样才算完成？
Small Enough？
一个 Sprint 做得完吗？
用一句话记住 Refinement

如果 Planning 是：

“这个 Sprint 要做什么？”

那么 Refinement 是：

“未来要做的东西，到底是什么意思？”

而一个成熟 PO 最重要的能力，并不是 写很多 User Story。

而是可以把：

模糊 Business Idea

一步一步变成：

Clear
Testable
Estimatable
Small
Independent enough
Ready for Development

的 Product Backlog Item。

所以 Step 6 Refinement 本质上其实是：

PO 带领 Business + Developer + QA，一起把 Unknown 消灭掉。

而不是 PO 自己坐在那里把 Jira Ticket 写完整。