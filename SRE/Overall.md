# 《凌晨 3:17：SRE 不只是救火》

## Site Reliability Engineer 案例式漫画大纲

> **漫画定位：**
> 以一名刚加入科技公司的 Junior SRE 为主角。每个 Chapter 都从一个真实感强烈的 Production Incident 开始，不先讲理论。
> 读者先跟着角色经历「出事 → 判断 → 决策 → 处理 → 复盘」，故事结束后才揭晓这一章对应的 SRE 概念与实际操作流程。
>
> **核心原则：Case First, Theory Later。**

---

# 故事开始前：人物 Background

## 主角：林凯 Kai

**职位：** Junior Site Reliability Engineer
**年龄：** 26 岁
**经验：** 2 年 Software Engineer，刚转职成为 SRE
**擅长：** Linux、Python、Docker
**弱点：** Production Troubleshooting、Kubernetes、Incident Management
**性格：** 喜欢解决问题，但遇到 Production Alert 时容易紧张。

Kai 原本是一名 Backend Developer。

他一直认为：

> 「只要 Code 没 Bug，System 就不会有问题。」

直到加入 **NovaCloud**。

NovaCloud 是一家提供 SaaS 服务的科技公司。

每天：

* 约 200 万用户访问
* 数百个 Microservices
* Kubernetes 承载主要 Production Workload
* 每天 Deployment 数十次
* 系统要求 24×7 Availability

Kai 入职第一天，SRE Lead 只对他说了一句话：

> **「Developer 负责让系统跑起来。」**
>
> **「SRE 负责让系统在最糟糕的时候，依然跑得下去。」**

Kai 当时并没有真正理解这句话。

直到——

**凌晨 3:17。**

手机响了。

`P1 ALERT — Checkout API Error Rate > 35%`

这也是 Kai 的第一次 On-call。

---

# Chapter 1 — 凌晨 3:17

## Case：Production 突然大量 500 Error

凌晨 3:17。

Kai 被 Pager 吵醒。

```text
CRITICAL ALERT

Service: checkout-api
Error Rate: 37%
Latency P99: 8.4s
Region: ap-southeast
```

Slack 的 Incident Channel 已经开始疯狂跳通知。

Customer Support：

> 「用户无法付款。」

Business Team：

> 「Checkout conversion 正在下降。」

Engineering Manager：

> 「发生什么事？」

Kai 第一反应：

> 「Restart Server？」

Senior SRE Maya 阻止了他。

> 「先不要动 Production。」
>
> 「先回答三个问题。」
>
> **What changed?**
>
> **What is broken?**
>
> **How big is the blast radius?**

两人开始调查。

Dashboard 显示：

```text
CPU          Normal
Memory       Normal
Network      Normal
DB Latency   ↑↑↑
```

Kai：

> 「Database？」

但 Maya 打开 Deployment Timeline。

**02:58 — payment-service v2.8.1 deployed**

Kai愣了一下。

> 「Alert 是 3:17。」
>
> 「Deployment 是 2:58……」

Maya：

> 「Correlation isn't causation。」
>
> 「但它值得调查。」

最终发现：

新版本增加了一条 SQL Query。

在高流量下造成大量 Table Scan。

Database Connection Pool 被耗尽。

Checkout API 开始 Timeout。

团队决定 Rollback。

五分钟后：

```text
Error Rate
37% → 12% → 3% → 0.4%
```

Production 恢复。

Kai松了一口气。

Maya却说：

> 「Incident 还没有结束。」

Kai：

> 「不是恢复了吗？」

Maya：

> 「恢复 Service，只完成了一半。」
>
> 「另一半，是确保它不会再发生。」

---

## Case结束后：这一章其实在学什么？

### SRE Concept

* Monitoring
* Alerting
* Incident Response
* Triage
* Blast Radius
* Mitigation
* Rollback
* Mean Time To Recovery（MTTR）

### 实际操作过程

```text
Alert Triggered
      ↓
Acknowledge Incident
      ↓
Check User Impact
      ↓
Check Metrics / Logs / Traces
      ↓
Check Recent Changes
      ↓
Form Hypothesis
      ↓
Mitigate First
      ↓
Rollback / Failover / Scale
      ↓
Verify Recovery
      ↓
Postmortem
```

### Kai 学到的第一条 SRE 原则

> **Production 出问题时，第一目标不是找到完美答案。**
>
> **第一目标是恢复服务。**

---

# Chapter 2 — 「CPU 只有 40%，为什么网站还是这么慢？」

## Case：Dashboard 看起来一切正常

星期一早上。

Customer Support 收到大量投诉：

> 「Website 很慢。」

Kai打开 Infrastructure Dashboard。

```text
CPU       42%
Memory    61%
Disk      38%
```

全部正常。

Kai：

> 「Infrastructure 没问题啊。」

Maya：

> 「用户说慢。」
>
> 「你的 Dashboard 说正常。」
>
> 「你相信谁？」

Kai沉默。

Maya：

> 「相信用户。」

他们开始查看 Application Metrics。

发现：

```text
Average Latency = 320ms
```

看起来也不错。

但 Maya 切换到：

```text
P50 = 180ms
P95 = 1.8s
P99 = 7.2s
```

Kai：

> 「原来 Average 把问题藏起来了。」

继续 Trace 后发现：

```text
Frontend
   ↓
API Gateway
   ↓
Order Service
   ↓
Recommendation Service
   ↓
External API
        ↑
     6 seconds
```

真正的问题不是 CPU。

而是一个 External API 偶发 Timeout。

---

## Case结束后：这一章其实在学什么？

### SRE Concept

这一章介绍 SRE 最重要的 Observability 思维：

**Metrics + Logs + Traces**

同时引入：

### Golden Signals

* Latency
* Traffic
* Errors
* Saturation

### 实际操作过程

```text
User Complaint
      ↓
Check Service-Level Metrics
      ↓
Latency / Traffic / Errors / Saturation
      ↓
Identify Abnormal Service
      ↓
Trace Request Path
      ↓
Inspect Logs
      ↓
Locate Dependency
      ↓
Mitigate
```

### Kai 的第二条笔记

> **Server Healthy ≠ Service Healthy。**
>
> SRE 观察的不是 Server。
>
> SRE 观察的是 **User Experience**。

---

# Chapter 3 — 99.9% 到底是什么意思？

## Case：老板要求「100% Uptime」

季度会议。

CEO 问：

> 「为什么我们的 Availability 只有 99.9%？」
>
> 「为什么不能做到 100%？」

Product Manager：

> 「Competitor 写 99.99%。」
>
> 「我们也应该 99.99%。」

Kai第一次参与 Reliability Meeting。

他以为 SRE Lead 会回答：

> 「没问题。」

结果 Maya 说：

> 「可以。」
>
> 「但你愿意付多少钱？」

会议室突然安静。

Maya在白板写下：

```text
99%      ≈ 7h 18m downtime / month
99.9%    ≈ 43m downtime / month
99.99%   ≈ 4m 23s downtime / month
99.999%  ≈ 26s downtime / month
```

然后问 Product Team：

> 「Checkout 和 Profile Picture，需要一样的 Reliability 吗？」

大家开始意识到：

不是所有 Service 都需要相同 Availability。

最终团队决定：

```text
Checkout API
SLI: Successful requests
SLO: 99.95%

Profile Service
SLI: Successful requests
SLO: 99.9%
```

Kai第一次理解：

**Reliability 不是越高越好。**

Reliability 是 Business Decision。

---

## Case结束后：这一章其实在学什么？

### SRE Concept

* SLA
* SLO
* SLI
* Availability
* Reliability Target

关系可以理解成：

```text
SLI
↓
我们如何测量？

SLO
↓
我们的目标是什么？

SLA
↓
如果没有达到，对客户承诺什么？
```

### 实际操作过程

```text
Identify Critical User Journey
      ↓
Define SLI
      ↓
Set SLO
      ↓
Measure Reliability
      ↓
Compare Actual vs Target
      ↓
Review Regularly
```

---

# Chapter 4 — Error Budget 用完了

## Case：Developer 还想 Deploy

星期五下午。

Developer：

> 「我们要 Release Recommendation v4。」

SRE Dashboard：

```text
Monthly SLO: 99.9%

Error Budget Remaining:

████░░░░░░  8%
```

这个月已经发生三次 Incident。

Kai：

> 「只剩 8%。」

Developer：

> 「可是这个 Feature Marketing 已经宣布了。」

Product Manager：

> 「必须上线。」

SRE：

> 「继续 Deploy，可能违反 SLO。」

会议变成争论。

最后 Maya 问：

> 「这个月我们已经花掉多少 Reliability？」

答案：

**92%。**

团队最终决定：

暂停高风险 Release。

优先处理 Reliability Issues。

---

## Case结束后：这一章其实在学什么？

### SRE Concept

**Error Budget**

```text
Error Budget = 100% - SLO
```

如果：

```text
SLO = 99.9%
```

那么：

```text
Error Budget = 0.1%
```

Error Budget 让 Developer 和 SRE 不再争论：

> 「要 Stability 还是 Feature？」

而是讨论：

> **「我们还有多少风险可以承担？」**

### 实际操作过程

```text
Define SLO
      ↓
Calculate Error Budget
      ↓
Track Consumption
      ↓
Budget Healthy?
   ↙       ↘
 YES       NO
 ↓          ↓
Deploy    Reduce Risk
Feature   Fix Reliability
```

---

# Chapter 5 — Kubernetes Pod 一直死

## Case：Restart 了 17 次

凌晨。

Alert：

```text
Pod CrashLoopBackOff
```

Kai：

```bash
kubectl get pods
```

看到：

```text
payment-api-78d9f   0/1   CrashLoopBackOff   17
```

他的第一反应：

```bash
kubectl delete pod payment-api-78d9f
```

新的 Pod 出现。

然后——

又 Crash。

Kai再 Delete。

又 Crash。

Maya：

> 「你是在修问题。」
>
> 「还是在重置问题？」

Kai开始检查：

```bash
kubectl describe pod
kubectl logs
```

最终发现：

```text
OOMKilled
```

Application 新版本 Memory Usage 暴涨。

Memory Limit：

```text
512Mi
```

实际需要：

```text
~780Mi
```

---

## Case结束后：这一章其实在学什么？

### SRE Concept

* Kubernetes Troubleshooting
* Pod Lifecycle
* Resource Requests
* Resource Limits
* OOMKilled
* CrashLoopBackOff

### 实际操作过程

```bash
kubectl get pods

kubectl describe pod <pod>

kubectl logs <pod>

kubectl logs <pod> --previous

kubectl top pod
```

判断路径：

```text
Pod Failed
   ↓
Check Status
   ↓
Check Events
   ↓
Check Logs
   ↓
CPU / Memory?
   ↓
Config?
   ↓
Dependency?
   ↓
Application Error?
```

### Kai 的笔记

> **Restart 是 Mitigation。**
>
> **Root Cause 才决定问题会不会回来。**

---

# Chapter 6 — Database 快撑爆了

## Case：流量突然增长 300%

Marketing Campaign 上线。

Traffic：

```text
10K req/s
↓
31K req/s
```

Application Pods 自动 Scale。

```text
20 Pods → 60 Pods
```

大家以为系统成功撑住了。

突然 Database Alert：

```text
DB Connections: 94%
CPU: 91%
Query Latency: 4.2s
```

Kai发现一个危险事实：

Application 可以 Horizontal Scale。

Database 不一定可以。

Pod 越多：

```text
More Pods
   ↓
More Connections
   ↓
More Queries
   ↓
Database Saturation
```

Auto Scaling 反而正在加速 Database 崩溃。

---

## Case结束后：这一章其实在学什么？

### SRE Concept

* Capacity Planning
* Scaling
* Bottleneck
* Connection Pool
* Database Saturation
* Load Testing

### 实际操作过程

```text
Measure Current Traffic
      ↓
Understand Resource Usage
      ↓
Identify Bottleneck
      ↓
Estimate Growth
      ↓
Load Test
      ↓
Define Scaling Strategy
      ↓
Set Capacity Alerts
```

---

# Chapter 7 — Deploy 完，Production 爆炸

## Case：一个「很小的改动」

Developer：

> 「只是一个小 Change。」

PR：

```text
+12 lines
-4 lines
```

Deployment 成功。

CI/CD 全绿。

十分钟后：

```text
Error Rate: 0.2% → 18%
```

原因：

新版改变了 Cache Key Format。

导致 Cache Miss 大幅增加。

Database Traffic 瞬间暴涨。

团队立即 Rollback。

---

## Case结束后：这一章其实在学什么？

### SRE Concept

* Deployment Strategy
* Canary Deployment
* Blue-Green Deployment
* Rollback
* Change Failure Rate

### 更安全的 Release

```text
New Version
     ↓
Deploy 1%
     ↓
Observe Metrics
     ↓
Deploy 10%
     ↓
Observe
     ↓
Deploy 50%
     ↓
Deploy 100%
```

而不是：

```text
New Version
     ↓
YOLO
     ↓
100% Production
```

---

# Chapter 8 — 「是谁搞坏 Production？」

## Case：Postmortem Meeting

重大 Incident 后。

Manager 问：

> 「是谁 Deploy 的？」

会议室瞬间安静。

Kai知道是谁。

那位 Developer 就坐在旁边。

Maya却回答：

> 「这个问题不重要。」

Manager：

> 「为什么？」

Maya：

> 「因为如果一个 Engineer 按一次按钮就能毁掉 Production——」
>
> 「那问题不是 Engineer。」
>
> 「问题是我们的 System 允许这件事发生。」

于是会议的问题从：

```text
WHO caused it?
```

变成：

```text
WHY could this happen?
```

最终发现：

* 没有 Canary
* 没有 Automated Rollback
* Staging Traffic 不真实
* Alert 太慢
* Runbook 不完整

---

## Case结束后：这一章其实在学什么？

### SRE Concept

**Blameless Postmortem**

Postmortem：

```text
Incident Summary

Impact

Timeline

Root Cause

Contributing Factors

What Went Well

What Went Wrong

Action Items
```

重点不是：

> Who broke Production?

而是：

> **How do we make the system safer?**

---

# Chapter 9 — Alert 太多，反而没人看

## Case：一晚 237 个 Alerts

Kai On-call 一周。

手机不断响。

```text
CPU > 70%
Disk > 60%
Pod Restart
Memory > 75%
Latency > 500ms
...
```

一晚上：

**237 Alerts。**

真正影响 Customer 的 Alert：

只有 **2 个**。

第三天凌晨。

手机再次响起。

Kai看了一眼：

> 「应该又是 Noise。」

他继续睡。

20分钟后：

**P1 Incident。**

---

## Case结束后：这一章其实在学什么？

### SRE Concept

* Alert Fatigue
* Actionable Alerts
* Symptom-based Alerting
* SLO-based Alerting

好的 Alert 应该回答：

```text
What happened?

Who is affected?

How severe?

What should I do?
```

SRE 的目标不是：

> **More Alerts**

而是：

> **Better Alerts**

---

# Chapter 10 — Disaster Day

## Case：整个 Region 消失

下午 2:14。

Monitoring 突然显示：

```text
Region AP-SOUTHEAST

UNREACHABLE
```

不是一个 Pod。

不是一个 Server。

不是一个 Database。

而是：

**整个 Region。**

Management：

> 「多久可以恢复？」

Kai打开 Runbook。

```text
Regional Disaster Recovery
```

Traffic 开始切换：

```text
Singapore
     X
     ↓
Failover
     ↓
Tokyo
```

Database Replica Promotion。

DNS Traffic Shift。

Critical Services 恢复。

---

## Case结束后：这一章其实在学什么？

### SRE Concept

* Disaster Recovery
* High Availability
* Multi-Region Architecture
* Failover
* RTO
* RPO

### 两个关键问题

**RTO**

> System 最多可以 Down 多久？

**RPO**

> 最多可以接受损失多少 Data？

### Disaster Recovery Process

```text
Disaster Detected
      ↓
Declare Incident
      ↓
Assess Region
      ↓
Activate DR
      ↓
Failover Traffic
      ↓
Promote Database
      ↓
Validate Critical Services
      ↓
Monitor
      ↓
Recover Primary Region
```

---

# Chapter 11 — SRE 最大的敌人不是 Incident

## Case：每天都在做同一件事

Kai工作半年后发现：

每天早上：

```text
Check Disk
Check Backup
Restart Job
Check Certificate
Generate Report
Clean Logs
```

一天可能只需要两小时。

但一年：

```text
2 hours × 250 working days
= 500 hours
```

Kai：

> 「这些都是 SRE 工作吧？」

Maya：

> 「不。」
>
> 「这些叫 Toil。」

她问：

> 「如果一个工作每天都要重复，而且机器可以完成——」
>
> 「为什么还要人做？」

Kai开始写 Automation。

```text
Manual
↓
Script
↓
Scheduled Job
↓
Monitoring
↓
Self-Healing
```

三个月后：

原本每天两小时的工作：

**变成每天五分钟。**

---

## Case结束后：这一章其实在学什么？

### SRE Concept

* Toil
* Automation
* Infrastructure as Code
* Self-Healing
* Operational Efficiency

SRE 不应该成为：

> **高级人工 Restart Engineer。**

SRE 应该不断把重复工作：

```text
Human Work
      ↓
Automation
      ↓
Platform
```

---

# Final Chapter — 又是凌晨 3:17

一年后。

Kai已经成为 SRE。

凌晨 3:17。

Pager 再次响起。

```text
P1 ALERT

Checkout Error Rate > 20%
```

旁边的新 Junior SRE 紧张地问：

> 「要不要 Restart？」

Kai看着 Dashboard。

想起一年前的自己。

他说：

> 「先不要动 Production。」

然后在白板写下：

```text
1. What changed?

2. What is broken?

3. What is the blast radius?
```

Junior：

> 「然后呢？」

Kai打开 Incident Channel。

微笑着说：

> 「然后，我们开始调查。」

画面拉远。

屏幕上出现：

```text
INCIDENT #2841
STATUS: INVESTIGATING
```

**完。**

---

# Epilogue — 原来这就是 SRE

经历所有 Incident 后，Kai 才真正理解 SRE。

SRE 并不是一个单纯负责：

```text
Linux
Kubernetes
Cloud
Monitoring
CI/CD
```

的职位。

这些只是工具。

真正的 SRE 思维是：

```text
             Reliability
                  │
       ┌──────────┼──────────┐
       │          │          │
 Observability  Automation  Engineering
       │          │          │
       └──────────┼──────────┘
                  │
            Incident Response
                  │
                  ▼
          Reliable Systems
```

最终，Kai 在自己的 SRE Notebook 最后一页写下：

> **「SRE 的价值，不是系统从来不会坏。」**
>
> **「而是当系统一定会坏的时候，我们知道如何发现它、控制它、恢复它，并让同样的问题越来越难再次发生。」**

---

# 全漫画 Chapter Map

| Chapter | Case                        | SRE 核心能力                   |
| ------- | --------------------------- | -------------------------- |
| 01      | Checkout 大量 500             | Incident Response          |
| 02      | CPU 正常但网站很慢                 | Observability              |
| 03      | 老板要求 100% Uptime            | SLI / SLO / SLA            |
| 04      | Error Budget 用完             | Error Budget               |
| 05      | Kubernetes Pod 不断 Crash     | Kubernetes Troubleshooting |
| 06      | Traffic 暴涨 300%             | Capacity Planning          |
| 07      | Deployment 导致 Production 故障 | Safe Deployment            |
| 08      | 谁搞坏 Production？             | Blameless Postmortem       |
| 09      | 一晚 237 个 Alerts             | Alert Engineering          |
| 10      | 整个 Region Down              | Disaster Recovery          |
| 11      | 每天重复 Operation              | Toil & Automation          |
| Final   | 再次凌晨 3:17                   | SRE Mindset                |

## 整体学习路线

```text
             第一次 Production Incident
                       │
                       ▼
               Incident Response
                       │
                       ▼
                 Observability
                       │
                       ▼
                SLI / SLO / SLA
                       │
                       ▼
                 Error Budget
                       │
                       ▼
          Kubernetes Troubleshooting
                       │
                       ▼
              Capacity Planning
                       │
                       ▼
                Safe Deployment
                       │
                       ▼
             Blameless Postmortem
                       │
                       ▼
               Alert Engineering
                       │
                       ▼
              Disaster Recovery
                       │
                       ▼
              Toil & Automation
                       │
                       ▼
                  SRE Mindset
```

**整个漫画最重要的叙事规则：**

每一章都不要以：

> 「今天我们来学习 SLO。」

作为开场。

而应该以：

> **「Production 出事了。」**

作为开场。

先让读者面对问题、跟着 Kai 做错误判断、看到线索、参与 Troubleshooting 和决策；等 Incident 解决以后，再告诉读者：

> **「你刚才经历的，其实就是 SRE 的这个概念。」**

这样技术知识不是被“教”出来的，而是从故事里的问题自然产生。
