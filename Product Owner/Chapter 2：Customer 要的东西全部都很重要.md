# Chapter 2：Customer 要的东西全部都很重要！

## 本章核心问题

QuickRide 的 Product Owner Alex 遇到了一个非常典型的问题：

> 每一个部门都说自己的 Requirement 是最高 Priority。

Sales 要 Online Booking。
Operation 要 Vehicle ETA。
Finance 要 Refund。
Marketing 要 Promo Code。
Management 要 Dashboard。
Customer Service 要 Reschedule。
Driver Team 又说 Driver App 不做好，前面的功能全部没有意义。

问题不是：

> 「哪一个 Feature 比较重要？」

真正的问题是：

> **「我们现在到底想解决什么 Business Problem？」**

---

# 第一幕：Backlog 爆炸了

星期一早上。

Alex 打开 Jira。

屏幕显示：

**Product Backlog：87 items**

其中排在前面的有：

| Feature                     | Request By       |
| --------------------------- | ---------------- |
| Customer App                | Management       |
| Online Booking              | Sales            |
| Counter Booking Enhancement | Counter          |
| Credit Card                 | Finance          |
| E-Wallet                    | Finance          |
| Driver App                  | Operation        |
| GPS Tracking                | Operation        |
| Vehicle ETA                 | Customer Service |
| Voucher                     | Marketing        |
| Promo Code                  | Marketing        |
| Membership                  | Marketing        |
| Dynamic Pricing             | Management       |
| WhatsApp Notification       | Customer Service |
| SMS Notification            | Customer Service |
| Sales Dashboard             | Sales            |
| Driver Dashboard            | Operation        |
| Refund                      | Finance          |
| Cancellation                | Customer Service |
| Reschedule                  | Customer Service |

Alex 看着 Jira。

Alex：

> 「这哪里是 Product Backlog……」
>
> 「这是公司的愿望清单吧？」

这时候 Sales Manager 走过来。

Sales：

> 「Alex，Online Booking 一定要 Priority 1。」
>
> 「Customer 都已经习惯 online booking 了。」

Alex：

> 「OK。」

不到五分钟。

Operation Manager：

> 「Driver App 才应该 Priority 1。」
>
> 「没有 Driver App，你 Online Booking 进来以后谁接单？」

Alex：

> 「也有道理……」

Finance：

> 「Credit Card integration 必须先做。」
>
> 「没有 Payment，Booking 有什么意义？」

Marketing：

> 「Promo Code 呢？」
>
> 「Competitor 都已经在做 promotion 了。」

Customer Service：

> 「你们先解决 Cancellation。」
>
> 「每天 Customer 打电话来 cancel，我们全部 manual 做。」

最后 Management 说：

> 「全部都 important。」
>
> 「你作为 Product Owner，排一下 priority。」

Alex：

> 「……」

---

# 第二幕：Alex 开始用「谁声音大谁先做」

Alex 决定召开 Prioritization Meeting。

会议室里坐了六个 Department Head。

Alex：

> 「我们今天决定接下来两个 Sprint 做什么。」

Sales：

> 「Online Booking。」

Operation：

> 「Driver App。」

Marketing：

> 「Promo Code。」

Finance：

> 「Payment。」

Management：

> 「Dashboard。」

Customer Service：

> 「Cancellation。」

Alex：

> 「那我们 vote？」

大家投票。

结果：

```text
Online Booking     █████ 5
Driver App         █████ 5
Payment            ████  4
Dashboard          ████  4
Cancellation       ████  4
Promo Code         ███   3
```

Alex 看着结果：

> 「还是全部很重要啊。」

于是 Alex 做了一个很多公司都会做的决定：

> **每一个 Department 都给一点。**

Sprint Backlog：

```text
Online Booking UI        20%
Driver App Login         20%
Sales Dashboard          20%
Promo Code Database      20%
Cancellation API         20%
```

两个月以后。

Management：

> 「Online Booking 可以用了？」

Developer：

> 「还不能。」

Operation：

> 「Driver App 可以 dispatch？」

Developer：

> 「还不能。」

Marketing：

> 「Promo Code 可以 launch？」

Developer：

> 「还不能。」

Finance：

> 「Refund 呢？」

Developer：

> 「还没有。」

结果：

> **五个东西都做了一点。**
>
> **但是没有一个 Business Problem 被解决。**

---

# 第三幕：真正的问题出现了

某一天 Management 问：

> 「为什么这个月 Taxi Sales 又没有增长？」

Alex 开始调查。

他跑到机场 Counter。

早上 10:30。

Customer：

> 「我要一辆 6 Seater 去 KL。」

Counter Staff 查系统。

```text
6 Seater Available = 0
```

Counter：

> 「Sorry，目前没有车。」

Customer：

> 「多久有车？」

Counter：

> 「不知道。」

Customer：

> 「那算了，我叫 Grab。」

Alex：

> 「等一下。」

他问 Counter：

> 「刚才这个 Customer 有没有记录下来？」

Counter：

> 「没有啊。」

Alex：

> 「为什么？」

Counter：

> 「因为没有卖票。」

Alex：

> 「所以系统看到的是什么？」

Counter：

> 「Sales = 0。」

Alex 突然意识到一个问题。

系统看到：

```text
Sold Ticket = 0
```

但现实其实是：

```text
Demand = 1
Supply = 0
Lost Sale = 1
```

---

# 第四幕：Management 原来问错问题了

Alex 回办公室。

打开 Dashboard：

```text
6 Seater Sales

January    RM120,000
February   RM118,000
March      RM116,000
April      RM115,000
```

Management 一直认为：

> 「Demand 不够。」

所以 Marketing 提出：

```text
Promo Code
Voucher
Membership
Dynamic Pricing
```

但 Alex 开始怀疑：

> 「如果 Customer 本来就想买，只是没有车呢？」

那么 Promo Code 根本没有解决问题。

甚至可能更糟。

假设：

```text
Current Demand = 100
Available Supply = 70
```

最多只能完成：

```text
70 Trips
```

Marketing 做 Promotion：

```text
Demand → 130
Supply → 70
```

Sales 还是：

```text
70 Trips
```

但是 Customer 被拒绝更多：

```text
Lost Demand = 60
```

Alex：

> 「我们可能正在用 Marketing Feature，解决 Supply Problem。」

---

# 第五幕：PO 不应该先问「做什么」

Alex 找 Management。

Alex：

> 「我想先暂停讨论 Feature Priority。」

Management：

> 「为什么？」

Alex：

> 「因为现在每个 Feature 都可以讲出一个理由。」
>
> 「我们继续这样讨论，永远不会有答案。」

Alex 在白板写：

# WHY → WHAT

然后说：

> 「我们现在一直在讨论 WHAT。」

```text
Online Booking
Driver App
GPS
Voucher
Dashboard
Payment
```

> 「但是我们没有先确认 WHY。」

Alex 问 Management：

> 「未来三个月，公司最想改善什么？」

Management：

> 「Sales。」

Alex：

> 「为什么 Sales 上不去？」

Management：

> 「不知道。」

Alex：

> 「那我们的 Product Goal 不应该是『Build Online Booking』。」

因为：

```text
Build Online Booking
```

是 **Output**。

而不是 **Outcome**。

---

# 第六幕：什么叫 Product Goal？

Alex 在白板写：

### 错误的 Product Goal

> Build Customer App.

为什么错？

因为做完 App，并不代表 Business 有改善。

---

### 另一个错误例子

> Implement GPS Tracking.

这也是 Feature。

---

### 比较好的 Product Goal

> Increase Airport Taxi Completed Trips.

开始比较接近 Business Outcome。

但是还是不够明确。

---

Alex 最后和 Management 定义：

> **未来 3 个月，减少因为 Vehicle Availability 不明确及车辆不足造成的 Lost Sales，并提高 Completed Trips。**

进一步量化：

```text
Current Fulfillment Rate = unknown

Target:

Fulfillment Rate
70% → 85%

Lost Sales
↓ 30%
```

现在整个 Product Team 突然有了方向。

---

# 第七幕：Feature Priority 突然变得简单

Alex 把原来的 Feature 再拿出来。

首先：

### Promo Code

Alex：

> 「Promo Code 能改善 Vehicle Fulfillment 吗？」

Marketing：

> 「不能。」

Priority：

```text
LOW
```

---

### Membership

Alex：

> 「Membership 能减少 Lost Sales 吗？」

Marketing：

> 「不直接。」

Priority：

```text
LOW
```

---

### Dynamic Pricing

Alex：

> 「现在的问题是 Price 还是没有 Vehicle？」

Operation：

> 「没有 Vehicle。」

Priority：

```text
LATER
```

---

### GPS Tracking

Alex：

> 「GPS 可以知道 Vehicle 在哪里吗？」

Operation：

> 「可以。」

Alex：

> 「能不能帮助预测多久有车？」

Operation：

> 「可以。」

Priority：

```text
HIGH
```

---

### Driver Status

```text
Available
On Trip
Returning
Break
Offline
```

Alex：

> 「这个可以知道真正 Supply 吗？」

Operation：

> 「可以。」

Priority：

```text
VERY HIGH
```

---

### Vehicle ETA

Counter Staff：

> 「这个非常有用。」

例如：

```text
6 Seater

Available Now: 0

Returning:
Vehicle A → 18 mins
Vehicle B → 35 mins
```

Counter 就可以告诉 Customer：

> 「目前没有车，但是大约 18 分钟后会有一辆。」

Customer 可能愿意等。

Priority：

```text
VERY HIGH
```

---

### Lost Demand Capture

Alex：

> 「如果没有 Vehicle，我们必须记录 Customer 原本想买什么。」

例如：

```text
Date       14 Aug
Time       10:35
Vehicle    6 Seater
Destination KLCC
Reason     No Vehicle
Result     Customer Left
```

这样以后才能知道：

```text
Demand
=
Completed Sales
+
Lost Sales
```

Priority：

```text
VERY HIGH
```

---

# 第八幕：Backlog 从 Feature List 变成 Goal Backlog

原本：

```text
1. Online Booking
2. Customer App
3. Promo Code
4. GPS
5. Dashboard
6. Membership
7. Cancellation
8. Driver App
```

没有任何逻辑。

现在变成：

# Product Goal

> Reduce Lost Sales caused by insufficient or uncertain vehicle availability.

---

## Initiative 1：Understand Demand

```text
Capture Lost Demand
Capture Requested Vehicle Type
Capture Destination
Capture Rejection Reason
```

---

## Initiative 2：Understand Supply

```text
Driver Status
Vehicle Status
GPS Location
Trip Start
Trip End
Expected Return Time
```

---

## Initiative 3：Improve Fulfillment

```text
Vehicle ETA
Suggested Alternative Vehicle
Waitlist
Reservation Queue
Dispatch Optimization
```

---

## Initiative 4：Measure Result

```text
Demand Dashboard
Fulfillment Rate
Lost Sales Rate
Vehicle Utilization
Average Customer Waiting Time
```

突然之间：

> **Backlog 不再是一堆 Feature。**

它变成：

```text
Business Problem
       ↓
Product Goal
       ↓
Initiatives
       ↓
Features
       ↓
User Stories
```

---

# 第九幕：一个 Feature 到底是不是 Priority？

Sales 又问：

> 「所以 Online Booking 不做了吗？」

Alex：

> 「不是。」

> 「Priority Low 不代表永远不做。」

Alex 在白板画：

```text
              Current Product Goal
                      │
        ┌─────────────┴─────────────┐
        │                           │
 Helps Goal                    Doesn't Help
        │                           │
        ▼                           ▼
 Consider Now                   Later
```

然后 Alex 问 Online Booking：

### Question 1

Online Booking 会不会增加 Demand？

```text
YES
```

### Question 2

我们目前最主要的问题是不是 Demand 不足？

```text
UNKNOWN / Probably NO
```

### Question 3

如果 Supply 已经不够，增加 Booking Channel 会怎样？

```text
More Demand
     ↓
Same Supply
     ↓
More Rejection
```

所以：

> Online Booking 是一个 **Good Feature**。

但：

> **Good Feature ≠ Right Feature Right Now。**

这就是 Product Owner 最重要的判断之一。

---

# 第十幕：Management 再次插单

星期三。

CEO 跑过来。

> 「Competitor 出 AI Chatbot 了。」

CEO：

> 「我们也做一个。」

过去的 Alex 可能会说：

> 「OK，Priority 1。」

现在 Alex 问：

> 「AI Chatbot 要解决什么？」

CEO：

> 「Customer 可以问有没有车。」

Alex：

> 「现在我们的系统自己都不知道什么时候有车。」

CEO：

> 「……」

Alex：

> 「如果 Supply Data 都没有，我们做 Chatbot，它只会非常聪明地回答——」

AI Chatbot：

> 「Sorry, vehicle availability unavailable。」

会议室安静了三秒。

Alex：

> 「所以我们应该先解决 Vehicle Availability Data。」

CEO：

> 「Makes sense。」

这就是 Product Goal 给 PO 的力量。

PO 不需要说：

> 「我不喜欢这个 Feature。」

而是可以说：

> 「这个 Feature 目前不能有效推动我们的 Product Goal。」

讨论从：

```text
Opinion vs Opinion
```

变成：

```text
Feature vs Product Goal
```

---

# 第十一幕：真正的 Priority 不是 1、2、3、4

Alex 最后重新整理 Product Backlog。

### NOW

```text
Lost Demand Capture
Driver Status
Vehicle Status
GPS Integration
Trip Completion
Vehicle ETA
Fulfillment Dashboard
```

### NEXT

```text
Waitlist
Alternative Vehicle Suggestion
Advanced Dispatch
Reservation
```

### LATER

```text
Online Booking
Customer App
Membership
Promo Code
Voucher
AI Chatbot
```

Marketing：

> 「为什么 Promo Code 在 Later？」

Alex：

> 「不是因为 Promo Code 没价值。」

> 「而是因为我们的 Current Constraint 不是 Demand。」

---

# 第十二幕：Product Owner 真正管理的东西

旁白：

很多人认为 PO 管的是：

```text
Backlog
```

但准确来说：

> PO 管的是 **Value。**

Backlog 只是工具。

PO 真正不断问的是：

```text
What problem are we solving?

↓

What outcome do we want?

↓

What is stopping us?

↓

What should we build next?

↓

Did it actually improve the outcome?
```

---

# 最后一幕：三个月以后

新的 Dashboard 上线。

```text
Airport Taxi Performance

Demand                    10,000
Completed Trips            8,400
Lost Demand                1,600

Fulfillment Rate
84%

Top Lost Demand Reason

No 6-Seater           43%
Waiting Time Too Long 27%
No Luxury Vehicle     12%
Price                   8%
Others                 10%
```

Management：

> 「原来我们最大的 Lost Sales 是 6 Seater。」

Operation：

> 「那我们是不是应该增加 6 Seater？」

Alex：

> 「可能。」

Management：

> 「为什么是可能？」

Alex：

> 「因为下一步还要看 Vehicle Utilization。」

如果：

```text
6 Seater Utilization = 95%
Lost Demand = High
```

很可能：

> **Supply 不足。**

但是如果：

```text
6 Seater Utilization = 55%
Lost Demand = High
```

问题可能不是车辆数量。

而是：

```text
Dispatch inefficient
Vehicle waiting at wrong location
Driver unavailable
Turnaround time too long
```

Alex：

> 「Product Goal 帮我们决定先调查什么。」
>
> 「Data 再帮我们决定应该做什么。」

---

# Chapter 2 完结

---

# 最后才解释：实际 Product Owner 怎么操作？

整个 Chapter 2 实际上是在教一个非常重要的 Product Management Flow：

```text
Business Problem
      ↓
Product Goal
      ↓
Success Metrics
      ↓
Identify Constraints
      ↓
Product Initiatives
      ↓
Prioritize Features
      ↓
Sprint Backlog
      ↓
Measure Outcome
```

## Step 1：不要从 Feature 开始

Stakeholder 说：

> 「我要 Promo Code。」

PO 不应该马上创建：

```text
US-1023
As a customer
I want promo code...
```

先问：

> 「你想解决什么 Business Problem？」

例如 Stakeholder 回答：

> 「Sales 太低。」

继续问：

> 「为什么你认为 Sales 低是因为没有 Promotion？」

这样 Requirement Discovery 才真正开始。

---

## Step 2：定义 Product Goal

一个比较好的 Product Goal 应该包含：

```text
Outcome
+
Target
+
Timeframe
```

例如：

> **在未来 3 个月，将 Taxi Fulfillment Rate 从 70% 提升到 85%。**

而不是：

> Build Taxi App。

因为 App 是 Output。

Fulfillment Improvement 才是 Outcome。

---

## Step 3：定义 Metrics

假设：

```text
Demand = Completed Trips + Lost Demand
```

那么：

```text
Fulfillment Rate
=
Completed Trips
───────────────
Total Demand
```

例如：

```text
Demand = 1,000

Completed = 800

Fulfillment
= 800 / 1000
= 80%
```

如果没有记录 Lost Demand：

```text
System Sales = 800
```

你根本不知道：

```text
Demand = 850？

还是

Demand = 1,500？
```

所以有时候：

> **第一个 Product Feature 甚至不是 Customer Feature。**

而是：

> **让公司可以正确 Measurement 的功能。**

---

## Step 4：找到 Constraint

不要马上 Build Solution。

先问：

```text
为什么 Fulfillment 不高？
```

可能是：

```text
Demand > Supply

Vehicle turnaround 太慢

Driver 不够

Vehicle 在错误 Location

Dispatch inefficient

Customer 不愿意等

Vehicle ETA 不透明
```

不同 Root Cause，需要完全不同的 Product Solution。

---

## Step 5：Feature 必须连接 Product Goal

可以简单建立：

| Feature               | 对 Product Goal 的帮助 | Priority |
| --------------------- | -----------------: | -------- |
| Lost Demand Capture   |                非常高 | Now      |
| Driver Status         |                非常高 | Now      |
| Vehicle ETA           |                  高 | Now      |
| GPS                   |                  高 | Now      |
| Dispatch Optimization |                  高 | Next     |
| Online Booking        |                  低 | Later    |
| Promo Code            |                 很低 | Later    |
| Membership            |                 很低 | Later    |

重点不是这个表本身。

真正重要的是每一个 Feature 都必须回答：

> **「为什么现在做？」**

---

# PO 最重要的一句话

以后有人对 PO 说：

> 「这个 Feature 很重要。」

PO 不需要反驳。

只需要问：

> **「它重要，我同意。但它对我们现在的 Product Goal 有多重要？」**

这两个问题完全不同。

---

# Chapter 2 的真正知识点

这一章真正想建立的是下面这个思维：

```text
Stakeholder Request
        ↓
不是立即变 Backlog
        ↓
Understand Problem
        ↓
Product Goal
        ↓
Measure Outcome
        ↓
Identify Constraint
        ↓
Choose Solution
        ↓
Backlog
```

所以一个成熟的 Product Owner 不是：

> **帮公司管理 Feature List 的人。**

而是：

> **帮助公司决定现在最值得解决哪个 Problem，以及为什么的人。**

而这也会直接连接到下一章更困难的问题：

> **「现在我们知道 Goal 了，但是 20 个东西都可以帮助这个 Goal，到底先做哪一个？」**

这时候才真正进入 **Backlog Prioritization、Value、Risk、Effort、Dependency 与 MVP**。
