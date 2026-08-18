# ITIL 漫画特别篇：Service Level Management

## 副标题：客户说「系统很慢」，IT 部门却说「我们没有故障」

---

# Chapter 1：到底是谁的问题？

## 场景

一家名为 **FreshGo** 的大型线上超市，每天有数万名客户通过手机 App 下单。

IT 部门负责维护：

* FreshGo App
* 网站
* Payment Gateway
* Inventory System
* Delivery Tracking System
* Customer Service Portal

星期五晚上 8 点，是 FreshGo 一星期订单量最高的时间。

突然，Customer Service 电话不断响起。

> 客户 A：
> 「为什么付款后一直转圈圈？」

> 客户 B：
> 「我已经等了 20 秒，订单还是没有完成。」

> 客户 C：
> 「你们的网站是不是坏了？」

Customer Service 马上通知 IT。

---

## IT Operations Room

Monitoring Dashboard：

```text
CPU Usage       : 54%
Memory Usage    : 62%
Server Status   : UP
Database Status : UP
Network Status  : UP
Application     : UP
```

工程师 Ken 看着 Dashboard。

Ken：

> 「系统全部都是绿色。」

经理问：

> 「那为什么客户一直投诉？」

Ken：

> 「Technically，没有 outage。」

业务经理 Alice 听到之后非常生气。

Alice：

> 「客户无法顺利付款，你告诉我系统正常？」

Ken：

> 「Server 没有 down。」

Alice：

> 「我不管 Server 有没有 down。」

> 「我要的是客户能够完成订单！」

---

# Chapter 2：IT 所说的「正常」，和业务所说的「正常」

第二天，公司召开紧急会议。

参与者：

* Alice — Business Manager
* Ken — IT Operations
* David — Service Manager
* Sarah — Customer Service Manager
* Michael — CIO

Michael 问：

> 「昨天到底发生什么事情？」

Ken：

> 「我们的 Availability 是 99.98%。」

Alice：

> 「可是客户根本无法正常付款。」

Ken：

> 「系统没有 downtime。」

Alice：

> 「但是客户平均等了 18 秒！」

Sarah：

> 「Customer Service 昨晚收到 376 个投诉。」

会议室突然安静下来。

---

David 在白板写下：

```text
IT Metric
≠
Business Experience
```

David：

> 「问题不是系统有没有运行。」

> 「问题是，我们从来没有定义什么叫做『好的服务』。」

---

# Chapter 3：什么叫「服务正常」？

David 问大家一个问题。

> 「Payment Service 要多快，才算正常？」

Ken：

> 「只要 Server 没有 down，就是正常。」

Alice：

> 「不对。」

> 「付款最好 2 秒完成。」

Sarah：

> 「客户超过 5 秒就开始重复按按钮。」

Michael：

> 「所以到底应该是多少秒？」

所有人沉默。

因为过去从来没有正式讨论过。

---

David 在白板写：

```text
Payment Response Time

2 seconds?
5 seconds?
10 seconds?
20 seconds?
```

然后他说：

> 「如果我们没有事先定义目标，发生问题以后，每个人都会有自己的标准。」

---

# Chapter 4：Service Level Management 出场

David：

> 「这就是我们需要 Service Level Management 的原因。」

## Service Level Management

Service Level Management 的核心不是：

> 「写一份 SLA。」

真正的目标是：

> **确保业务和 IT 对服务质量拥有共同、清楚而现实的理解。**

换句话说：

```text
Business Expectation
        ↓
Discussion
        ↓
Agreed Target
        ↓
Measurement
        ↓
Review
        ↓
Improvement
```

---

# Chapter 5：第一场 Service Level Workshop

David 安排了一场 Workshop。

参加者：

```text
Business
IT
Customer Service
Application Team
Infrastructure Team
Security Team
Vendor
Service Manager
```

David 没有一开始就问：

> 「SLA 要多少？」

而是问：

> 「FreshGo 最重要的业务活动是什么？」

Alice 回答：

1. 浏览商品
2. 加入购物车
3. Checkout
4. Payment
5. Order Confirmation
6. Delivery Tracking

David：

> 「哪一个最重要？」

Alice：

> 「Payment。」

原因很简单：

```text
如果 Browse 慢
→ 客户可能继续等待

如果 Payment 慢
→ 客户可能直接放弃订单
→ 公司损失收入
```

---

# Chapter 6：从业务需求开始

David继续问：

> 「什么时候 Payment Service 最重要？」

业务团队回答：

```text
星期一至星期四
09:00 – 23:00

星期五至星期日
08:00 – 01:00
```

特别重要时段：

```text
Friday 18:00 – 23:00
Saturday 10:00 – 23:00
Sunday 10:00 – 22:00
```

David把这些记录下来。

这就是：

## Service Level Requirement

也就是：

> **业务对于服务表现的需求。**

---

# Chapter 7：Availability 不只是「Server Up」

Ken提出：

> 「我们一直都有监控 Availability。」

David问：

> 「你们怎么计算？」

Ken：

```text
Server Availability
=
Server Uptime
÷
Total Time
```

David摇头。

> 「Business 不使用 Server。」

> 「Business 使用的是 Service。」

---

例如 Payment Service 包含：

```text
Mobile App
↓
API
↓
Payment Application
↓
Database
↓
Payment Gateway
↓
Bank Network
```

任何一个环节失败：

```text
Customer
↓
无法付款
```

即使 FreshGo Server 全部正常，

如果 Payment Gateway 出问题，

业务角度依然是：

```text
Payment Service unavailable
```

---

# Chapter 8：重新定义 Availability

团队决定：

Payment Service 的 Availability 应该从用户角度测量。

例如：

```text
Service Hours:
08:00 – 01:00
```

每个月：

```text
Total Service Time
=
17 hours × 30 days
=
510 hours
```

如果一个月不可用 1 小时：

```text
Availability
=
(510 - 1)
÷
510
×
100%
```

约为：

```text
99.80%
```

---

# Chapter 9：99.9% 到底是什么意思？

Alice看到 Availability Target：

```text
99.9%
```

她说：

> 「99.9% 听起来很好。」

David回答：

> 「不要只看百分比。」

> 「要转换成业务可以理解的数字。」

例如一个月约 720 小时：

```text
99%
≈ 7.2 hours downtime

99.9%
≈ 43 minutes downtime

99.99%
≈ 4.3 minutes downtime
```

David：

> 「现在你觉得 99.9% 够吗？」

Alice：

> 「如果 43 分钟刚好发生在 Friday Night？」

这就是关键。

---

# Chapter 10：平均值可能欺骗你

IT 原本报告：

```text
Monthly Availability
99.95%
```

看起来很好。

但 David 检查数据以后发现：

大部分 downtime 都发生在：

```text
Friday
20:00 – 22:00
```

也就是业务最高峰。

所以：

```text
High Availability
≠
Good Business Outcome
```

---

# Chapter 11：Response Time

然后团队讨论 Performance。

Customer Service 数据显示：

```text
0–3 seconds
客户通常正常等待

4–7 seconds
客户开始觉得慢

8–15 seconds
客户可能重复点击

>15 seconds
客户可能放弃
```

Alice提出：

> 「Payment 必须 3 秒完成。」

Application Team 马上反对。

> 「不可能。」

原因：

支付流程还依赖：

```text
Bank
Payment Gateway
Fraud Detection Service
OTP Service
```

David：

> 「Service Level Management 不是 Business 单方面要求，也不是 IT 单方面决定。」

而是：

```text
Business Need
+
Technical Capability
+
Cost
+
Risk
=
Agreed Service Level
```

---

# Chapter 12：最后决定 Performance Target

经过测试后：

团队确定：

```text
95% Payment Transactions
≤ 4 seconds

99% Payment Transactions
≤ 7 seconds
```

而不是：

```text
Average Response Time ≤ 4 seconds
```

为什么？

假设：

```text
Transaction 1 = 1 sec
Transaction 2 = 1 sec
Transaction 3 = 1 sec
Transaction 4 = 1 sec
Transaction 5 = 16 sec
```

平均：

```text
4 seconds
```

报告看起来达标。

但是最后一个客户已经等了：

```text
16 seconds
```

所以 percentile 往往更能代表真实体验。

---

# Chapter 13：Support Service Level

Sarah 提出另一个问题。

> 「客户报告付款失败以后，要多久才有人处理？」

于是团队开始定义 Incident Support。

---

## Priority 1

例如：

```text
Payment Service 完全不可用
```

目标：

```text
Acknowledgement:
≤ 5 minutes

Technical Investigation:
≤ 10 minutes

Business Communication:
≤ 15 minutes

Target Restoration:
≤ 30 minutes
```

---

## Priority 2

例如：

```text
部分用户付款失败
```

目标：

```text
Acknowledgement:
≤ 15 minutes

Target Restoration:
≤ 2 hours
```

---

## Priority 3

例如：

```text
个别客户出现异常
```

目标：

```text
Acknowledgement:
≤ 4 business hours

Target Resolution:
≤ 2 business days
```

---

# Chapter 14：Resolution 和 Restoration 不一样

Ken：

> 「为什么写 Restoration，不写 Resolution？」

David：

> 「因为两者不同。」

## Restoration

意思是：

> 尽快恢复服务。

例如：

```text
Payment Gateway A 故障

↓
临时切换到 Payment Gateway B

↓
Payment Service 恢复
```

服务恢复了。

但是 Root Cause 还没解决。

---

## Resolution

例如：

第二天 Vendor 找到 bug。

然后：

```text
Fix Bug
↓
Deploy Patch
↓
Permanent Fix
```

这才叫 Resolution。

因此：

```text
Service Restoration
≠
Permanent Resolution
```

---

# Chapter 15：开始设计 SLA

团队最后形成：

# Payment Service SLA

## Service Scope

包含：

```text
Mobile Payment
Web Payment
Credit Card
Debit Card
Online Banking
E-Wallet
```

---

## Service Hours

```text
Monday – Thursday
08:00 – 01:00

Friday – Sunday
07:00 – 02:00
```

---

## Availability

```text
Monthly Availability
≥ 99.9%
```

但还有一个条件：

```text
Peak Hours Availability
≥ 99.95%
```

Peak Hours：

```text
Friday – Sunday
18:00 – 23:00
```

---

## Performance

```text
95% Payment Transactions
≤ 4 seconds

99%
≤ 7 seconds
```

---

## Incident Response

Priority 1：

```text
Acknowledgement ≤ 5 mins
Restore ≤ 30 mins
```

Priority 2：

```text
Acknowledgement ≤ 15 mins
Restore ≤ 2 hours
```

---

## Communication

P1 Incident：

```text
Initial Notification
≤ 15 minutes

Status Update
Every 30 minutes
```

---

# Chapter 16：SLA 不是 IT 的 KPI

过了一个月。

Manager 对 Ken 说：

> 「你的 KPI 是 SLA 99.9%。」

David马上阻止。

> 「不完全正确。」

如果 SLA 变成纯粹的员工 KPI，

团队可能开始优化数字。

例如：

```text
Incident 快到 30 分钟

↓
提前关闭 Ticket

↓
重新开一个 Ticket
```

Dashboard：

```text
SLA = Passed
```

Customer：

```text
Service = Still Broken
```

---

这叫：

## Metric Gaming

当指标成为目标以后，

人可能开始优化：

```text
Metric
```

而不是：

```text
Outcome
```

---

# Chapter 17：Watermelon SLA

下个月 Service Review。

Dashboard：

```text
Availability       GREEN
Response Time      GREEN
Incident SLA       GREEN
Customer Rating    GREEN
```

全部绿色。

Michael 很满意。

可是 Alice 突然说：

> 「为什么投诉增加了 22%？」

所有人愣住。

David打开 Customer Feedback。

发现：

客户主要投诉：

```text
Payment successful
but
Order Confirmation delayed
```

Payment SLA 达标。

可是：

```text
End-to-End Experience
```

依然不好。

---

这种情况经常被称为：

## Watermelon SLA

外面：

```text
GREEN
```

切开以后：

```text
RED
```

也就是：

```text
Dashboard looks good
but
Customer experience is bad
```

---

# Chapter 18：Experience Level

David于是增加 Customer Experience 指标。

例如：

```text
Successful Checkout Rate
≥ 99%

Customers completing checkout
within 30 seconds
≥ 95%

Payment-related complaints
< 0.5%

Customer Satisfaction
≥ 4.5 / 5
```

这些指标开始把焦点从：

```text
Component
```

转向：

```text
Customer Journey
```

---

# Chapter 19：SLA 没达到怎么办？

第三个月：

```text
Availability Target:
99.90%

Actual:
99.72%
```

SLA Breach。

IT 团队很紧张。

Ken：

> 「我们是不是要被处罚？」

David：

> 「重点不是找谁负责。」

Service Level Management 真正应该问：

```text
What happened?

Why?

Business impact?

What can we learn?

What should we improve?
```

---

# Chapter 20：Service Review Meeting

每个月举行：

## Service Review

议程：

```text
1. Service Performance

2. SLA Achievement

3. Major Incidents

4. Customer Feedback

5. Trends

6. Risks

7. Improvement Opportunities
```

---

David展示：

```text
Payment Failure Rate

January    0.4%
February   0.6%
March      0.9%
April      1.2%
```

虽然 SLA 还没有 breach，

但是趋势非常明显：

```text
Service is deteriorating
```

这就是为什么：

> Service Level Management 不应该只看 Pass / Fail。

还要看：

```text
Trend
```

---

# Chapter 21：Service Improvement

调查发现：

Payment Gateway Vendor 在高峰时段开始出现 latency。

团队决定：

```text
Improvement 1

增加第二 Payment Gateway
```

同时：

```text
Improvement 2

建立 automatic failover
```

以及：

```text
Improvement 3

加入 synthetic payment monitoring
```

系统每一分钟模拟一次：

```text
Customer
↓
Checkout
↓
Payment
↓
Confirmation
```

这样 IT 不只是监控：

```text
Server
```

而是监控：

```text
真实服务体验
```

---

# Chapter 22：Supplier SLA

此时出现另一个问题。

FreshGo 对客户承诺：

```text
Payment Availability
99.9%
```

但是 Payment Gateway Vendor 的合同只有：

```text
Availability
99.5%
```

David看到后：

> 「这不可能。」

因为：

```text
Supplier
99.5%

↓

FreshGo

↓

Customer SLA
99.9%
```

FreshGo 无法稳定提供比底层关键供应商更高的服务承诺，除非有额外设计，例如：

```text
Redundancy
Failover
Multiple Suppliers
```

---

于是重新谈 Vendor Contract。

要求：

```text
Availability ≥ 99.95%

P1 Response ≤ 10 minutes

P1 Restoration ≤ 30 minutes
```

---

# Chapter 23：Operational Level Agreement

Application Team 说：

> 「Payment Incident 我们可以 30 分钟处理。」

Infrastructure Team 却说：

> 「Network Team 可能需要 1 小时。」

问题来了：

Customer SLA：

```text
Restore ≤ 30 minutes
```

但内部团队：

```text
Network Team
Restore ≤ 60 minutes
```

明显无法实现。

于是建立内部协议：

## OLA

Operational Level Agreement。

例如：

```text
Customer SLA
P1 Restore ≤ 30 mins
```

内部：

```text
Service Desk
Escalate ≤ 3 mins

Application Team
Respond ≤ 5 mins

Infrastructure Team
Respond ≤ 5 mins

Database Team
Respond ≤ 5 mins
```

这些内部目标一起支持最终 Customer SLA。

---

# Chapter 24：Service Level Management 的真正结构

现在 FreshGo 的结构变成：

```text
Customer
   ↓
SLA
   ↓
FreshGo IT Service
   ↓
-----------------
↓       ↓       ↓
App     Infra   DB
OLA     OLA     OLA
   ↓
Supplier
Contract
```

换句话说：

```text
Customer Expectation
        ↓
SLA
        ↓
Internal Capability
        ↓
OLA
        ↓
External Supplier
        ↓
Contract
```

所有目标必须互相支持。

---

# Chapter 25：ITIL 正式解释

## 什么是 Service Level Management？

在 ITIL 4 中，Service Level Management 的重点是：

> 为服务建立清晰、基于业务的目标，并确保服务交付能够针对这些目标进行评估、监控和管理。

简单来说：

```text
客户需要什么？
        ↓
我们能够提供什么？
        ↓
双方同意什么？
        ↓
我们怎么测量？
        ↓
有没有达到？
        ↓
如何改善？
```

---

# Chapter 26：Service Level Management Lifecycle

可以把整个过程理解成：

```text
Understand
↓
Define
↓
Agree
↓
Monitor
↓
Report
↓
Review
↓
Improve
```

---

## Step 1：Understand

理解：

```text
Customer
Business
Users
Service
```

重点不是问：

> 「你要多少 Availability？」

而是问：

> 「你要完成什么业务活动？」

---

## Step 2：Define

把模糊需求转换成可以测量的指标。

例如：

错误：

```text
System should be fast
```

正确：

```text
95% transactions
≤ 4 seconds
```

---

错误：

```text
System should always be available
```

正确：

```text
Monthly Availability
≥ 99.9%
```

---

## Step 3：Agree

Business 和 IT 共同确认：

```text
Target
Measurement
Responsibility
Reporting
Exception
```

---

## Step 4：Monitor

持续收集：

```text
Availability
Performance
Incident
Transaction
Customer Feedback
```

---

## Step 5：Report

建立：

```text
Service Report
Dashboard
Trend Report
```

但不要只显示：

```text
Green
Red
```

应该解释：

```text
Business Impact
Trend
Risk
Reason
```

---

## Step 6：Review

定期进行：

```text
Service Review Meeting
```

讨论：

```text
What worked?

What failed?

What changed?

What risks exist?

What should improve?
```

---

## Step 7：Improve

把机会加入：

```text
Continual Improvement Register
```

并追踪：

```text
Owner
Action
Deadline
Expected Benefit
Result
```

---

# Chapter 27：好的 SLA 应该有什么？

一个好的 SLA 不应该有 100 个指标。

真正重要的是：

```text
少量
+
重要
+
可以测量
+
与业务相关
```

例如：

| Category      | Metric                       |
| ------------- | ---------------------------- |
| Availability  | 99.9%                        |
| Performance   | 95% ≤ 4 sec                  |
| Reliability   | Successful Transaction ≥ 99% |
| Support       | P1 Restore ≤ 30 min          |
| Experience    | CSAT ≥ 4.5                   |
| Communication | P1 Update every 30 min       |

---

# Chapter 28：常见错误

## 错误 1

只测：

```text
Server Uptime
```

却没有测：

```text
Service Availability
```

---

## 错误 2

所有东西都是：

```text
99.9%
```

却不知道业务需不需要。

---

## 错误 3

SLA 有：

```text
50 个 KPI
```

结果没有人看。

---

## 错误 4

只在 SLA Breach 才讨论服务。

---

## 错误 5

只看：

```text
Average
```

导致严重的少数用户问题被隐藏。

---

## 错误 6

IT 自己定义 SLA。

没有 Business。

---

## 错误 7

把 SLA 当作：

```text
Punishment Tool
```

而不是：

```text
Communication
+
Expectation Management
+
Improvement Tool
```

---

# Chapter 29：Service Level Management 与其他 ITIL Practice

SLM 并不是单独运行。

它与很多 Practice 有关系。

```text
Service Level Management
        ↓
Incident Management
Problem Management
Monitoring and Event Management
Availability Management
Capacity and Performance Management
Supplier Management
Relationship Management
Continual Improvement
Service Desk
```

---

例如：

### Incident Management

回答：

```text
发生故障后
多久恢复？
```

---

### Problem Management

回答：

```text
为什么一直发生？
```

---

### Monitoring and Event Management

回答：

```text
怎么发现异常？
```

---

### Supplier Management

回答：

```text
Vendor 能不能支持 SLA？
```

---

### Continual Improvement

回答：

```text
服务如何越来越好？
```

---

# Chapter 30：最终成果

六个月以后。

FreshGo 的 Dashboard 不再只是：

```text
CPU
Memory
Server
Database
```

而是：

```text
Customer Checkout Success

Payment Response Time

Payment Availability

Failed Transactions

Customer Complaints

Service SLA

Business Revenue Impact
```

星期五晚上再次出现 Payment Gateway 延迟。

Monitoring 在客户投诉以前发现：

```text
Payment Latency
↑
```

系统自动：

```text
Gateway A
↓
Gateway B
```

Payment Service 恢复。

整个过程：

```text
2 minutes
```

Customer Service：

```text
0 complaint
```

Alice问：

> 「今天系统有问题吗？」

Ken笑着回答：

> 「Infrastructure 有问题。」

> 「Service 没有问题。」

David补充：

> 「这才是我们真正需要管理的东西。」

---

# 最终重点

Service Level Management 并不是：

```text
写 SLA
```

而是：

```text
理解业务
↓
理解客户
↓
定义服务体验
↓
设定合理目标
↓
持续测量
↓
沟通结果
↓
改善服务
```

真正的核心思想是：

> **不要问 Server 有没有正常运行。**

而要问：

> **客户能不能成功完成他想完成的事情？**

---

# 考试记忆版

如果考试问：

## Service Level Management 的目的是什么？

记：

```text
Business-based targets
+
Clear expectations
+
Monitoring
+
Review
+
Improvement
```

---

## SLA

```text
Service Provider
↔
Customer
```

---

## OLA

```text
Internal Team
↔
Internal Team
```

---

## Supplier Contract

```text
Organization
↔
External Supplier
```

最终三者必须：

```text
OLA
+
Supplier Contract
        ↓
Support
        ↓
Customer SLA
```

---

# 一句话总结

> **Service Level Management 的重点不是让 SLA 变绿，而是让业务真正得到它需要的服务。**
