# 《系统明明在 Cloud，为什么还是半夜 3 点叫我起床？》

## Senior Cloud Engineer 实战漫画课程

> **课程方式：案例先行 → 系统出事 → Senior Engineer 判断 → 做 Architecture Decision → 解决问题 → 最后才解释 Cloud 原理与实际操作。**
>
> 所有第一次出现的缩写都会附上 Full Term，例如：
>
> * VNet（Virtual Network）
> * NSG（Network Security Group）
> * IaC（Infrastructure as Code）
> * RTO（Recovery Time Objective）
> * RPO（Recovery Point Objective）

---

# 人物 Background

## 主角：Alex

Alex 做了 10 年 Software Engineering。

他的技术背景不错：

* C# / .NET
* SQL Server
* REST API（Representational State Transfer Application Programming Interface）
* Azure App Service
* Azure SQL Database
* Docker
* CI/CD（Continuous Integration / Continuous Delivery）

以前 Alex 是 Tech Lead。

他的思维通常是：

> 「Application 有问题，我去看 Code。」

后来公司把他升成：

# Senior Cloud Engineer

老板告诉他：

> 「以后你不只是负责 Application。」
>
> 「你要确保整个 Cloud Platform 可以稳定地跑。」

Alex 很开心。

他心想：

> 「Cloud 不就是开几个 App Service、Database、Storage Account 吗？」

直到上班第一周。

---

# 故事背景：GoGo Transport

Alex 加入一家交通科技公司：

**GoGo Transport**

公司提供：

* Bus Ticket
* Train Ticket
* Airport Transfer
* Taxi Booking

每天大约：

**300,000 Transactions**

系统主要运行在 Microsoft Azure。

目前 Architecture：

```text
Internet
   │
   ▼
Azure Application Gateway
   │
   ▼
Azure App Service
   │
   ├── Booking API
   ├── Payment API
   └── Ticket API
   │
   ▼
Azure SQL Database
```

Alex 原本觉得：

> 「Architecture 很简单啊。」

三个月后，他发现 Senior Cloud Engineer 真正面对的是：

```text
Availability
Security
Networking
Identity
Scalability
Cost
Deployment
Monitoring
Disaster Recovery
Governance
Automation
Architecture
```

而且最恐怖的是：

> **这些问题通常不会一个一个来。**

它们会一起发生。

---

# Chapter 1：凌晨 3 点，Production 全部死掉了

## 案例：Server 没坏，为什么 Customer 全部进不来？

星期六凌晨 3:17 AM。

Alex 电话响了。

Operation：

> 「Production Down！」

Alex 打开 Azure Portal。

奇怪。

App Service：

```text
Running
```

Database：

```text
Online
```

CPU：

```text
42%
```

Memory：

```text
58%
```

Alex：

> 「全部都是 Green，哪里 Down？」

Operation：

> 「Customer 全部 Timeout。」

Alex开始调查整个 Request Path。

```text
Customer
   │
   ▼
DNS（Domain Name System）
   │
   ▼
Application Gateway
   │
   ▼
NSG（Network Security Group）
   │
   ▼
App Service
   │
   ▼
SQL Database
```

最后发现：

Application Gateway Backend Health：

```text
UNHEALTHY
```

原因：

Health Probe 配错。

Application 本身没有 Down。

但是入口认为 Backend 已经死亡。

于是：

```text
Customer
   ↓
Application Gateway
   ↓
X Backend Unhealthy
```

Traffic 根本没有进入 Application。

---

## Alex 学到第一课

Cloud Engineer 不能只问：

> 「Server 有没有 Running？」

而应该问：

> 「Request 从 Customer 到 Database，中间经过什么？」

Senior Cloud Engineer 必须能够画出：

# End-to-End Request Flow

---

## Chapter 1 最后才解释：Cloud Troubleshooting

调查顺序：

### Step 1：检查 DNS（Domain Name System）

```bash
nslookup api.company.com
```

确认：

```text
Domain
↓
Correct IP / Endpoint
```

### Step 2：检查 Load Balancer / Application Gateway

检查：

```text
Listener
Backend Pool
Health Probe
Routing Rule
```

### Step 3：检查 Network

包括：

* VNet（Virtual Network）
* Subnet
* NSG（Network Security Group）
* Route Table
* Firewall

### Step 4：检查 Application

包括：

```text
CPU
Memory
HTTP Error
Application Log
Dependency
```

### Step 5：检查 Database

包括：

```text
Connection
DTU（Database Transaction Unit）
vCore（Virtual Core）
Blocking
Deadlock
Connection Pool
```

Senior Cloud Engineer 的 Troubleshooting 思维变成：

```text
User
 ↓
DNS
 ↓
Edge
 ↓
Load Balancer
 ↓
Network
 ↓
Compute
 ↓
Application
 ↓
Database
 ↓
External Dependency
```

---

# Chapter 2：老板说「系统很慢」，但 CPU 只有 30%

## 案例：到底要不要 Scale Up？

星期一早上。

老板：

> 「Customer 投诉 Booking 很慢。」
>
> 「加 Server。」

Developer：

> 「CPU 才 30%。」

老板：

> 「那为什么慢？」

Alex 打开 Azure Monitor。

发现：

```text
CPU                 30%
Memory              55%
Request Duration    8 seconds
SQL Duration        6.5 seconds
```

真正问题不是 App Service。

而是 SQL Query。

一个新的 Report API 正在执行：

```sql
SELECT *
FROM Booking
JOIN Payment
JOIN Ticket
...
```

扫描几千万条 Record。

如果 Alex直接 Scale App Service：

```text
2 Instances
     ↓
4 Instances
     ↓
8 Instances
```

结果可能只是：

> **更多 Application Instance 一起攻击同一个 Database。**

---

## Alex 开始学习 Bottleneck Thinking

Performance 不等于 CPU。

真正应该分析：

```text
Request Duration
      │
      ├── Application
      ├── Database
      ├── Cache
      ├── Network
      └── External API
```

---

## Chapter 2 最后才解释：Vertical Scaling vs Horizontal Scaling

### Vertical Scaling

```text
4 CPU / 8 GB RAM
        ↓
8 CPU / 16 GB RAM
```

也叫：

**Scale Up**

适合：

* 单机资源不足
* Memory 不够
* CPU 长期高

### Horizontal Scaling

```text
Instance 1
Instance 2
Instance 3
Instance 4
```

也叫：

**Scale Out**

适合：

* Web Application
* Stateless API
* Traffic Spike

但是：

> Scaling 不能解决所有 Performance Problem。

先找：

# Bottleneck

再决定：

```text
Optimize
Cache
Scale Up
Scale Out
Queue
Partition
```

---

# Chapter 3：Marketing 做 Promotion，系统直接爆掉

## 案例：平时 500 TPS，今天突然 5,000 TPS

TPS（Transactions Per Second）

Marketing 做：

> 「RM1 Bus Ticket Promotion」

10:00 AM 开始。

9:59 AM：

```text
500 TPS
```

10:01 AM：

```text
5,000 TPS
```

App Service 自动 Scale Out。

```text
4 Instances
↓
8 Instances
↓
16 Instances
```

Alex松了一口气。

然后……

Database Connection：

```text
MAX
```

Payment API：

```text
Timeout
```

Ticket API：

```text
Timeout
```

整个系统还是倒了。

---

## Alex 发现一个重要问题

Cloud 的 Scaling 不只是：

```text
Web Server Scaling
```

而是：

```text
Web
 ↓
API
 ↓
Cache
 ↓
Queue
 ↓
Database
 ↓
External System
```

任何一个 Component 都可能成为 Bottleneck。

---

## 解决 Architecture

Alex加入：

Redis Cache

以及：

Queue。

Architecture 变成：

```text
Customer
   │
   ▼
API
   │
   ├──── Redis Cache
   │
   ▼
Queue
   │
   ▼
Worker
   │
   ▼
Database
```

Sudden Traffic 不再直接打 Database。

---

## Chapter 3 最后才解释：Elasticity

Cloud 的核心能力之一：

**Elasticity**

也就是：

```text
Demand ↑
Resource ↑

Demand ↓
Resource ↓
```

常见 Scaling Metric：

* CPU
* Memory
* Request Count
* Queue Length
* Response Time

Senior Engineer 不应该只配置：

```text
CPU > 70%
→ Scale Out
```

还应该考虑：

```text
Cooldown
Minimum Instance
Maximum Instance
Database Capacity
External API Limit
```

---

# Chapter 4：Security Team 问：「为什么 Database 有 Public IP？」

会议室突然安静。

Security Engineer：

> 「为什么 Production SQL 可以从 Internet Access？」

Developer：

> 「因为比较方便。」

Alex：

> 「……」

Security：

> 「方便谁？」

Developer：

> 「我们。」

---

## Alex 开始重新设计 Network

以前：

```text
Internet
   │
   ├── App Service
   │
   └── SQL Database
```

很多 Resource 都有 Public Endpoint。

Alex 改成：

```text
Internet
   │
   ▼
WAF（Web Application Firewall）
   │
   ▼
Application Gateway
   │
   ▼
App Service
   │
   ▼
Private Endpoint
   │
   ▼
SQL Database
```

Database 不再直接暴露 Internet。

---

## Chapter 4 最后才解释：Cloud Network

核心 Component：

### VNet（Virtual Network）

Cloud 内部 Private Network。

```text
10.0.0.0/16
```

里面再分：

```text
10.0.1.0/24 Web
10.0.2.0/24 Application
10.0.3.0/24 Database
```

### NSG（Network Security Group）

控制：

```text
Who
Can Talk
To Who
On Which Port
```

例如：

```text
App Subnet
   ↓ TCP 1433
Database
```

但是：

```text
Internet
   ↓
Database
```

拒绝。

---

# Chapter 5：Developer 说：「给我 Production Owner 权限」

## 案例：权限越来越乱

新 Developer：

> 「Alex，我需要 Production Access。」

Alex：

> 「需要什么权限？」

Developer：

> 「Owner。」

Alex：

> 「为什么？」

Developer：

> 「不然以后需要东西很麻烦。」

Alex打开 IAM（Identity and Access Management）。

发现：

```text
Developer A → Owner
Developer B → Contributor
Vendor → Contributor
Intern → Contributor
Old Employee → Still Active
```

Alex：

> 「这不是 Access Control。」
>
> 「这是抽奖。」

---

## Chapter 5 最后才解释：IAM（Identity and Access Management）

Senior Cloud Engineer 要理解：

### RBAC（Role-Based Access Control）

不要直接：

```text
User
→ Permission
```

而是：

```text
User
 ↓
Group
 ↓
Role
 ↓
Resource
```

例如：

```text
Developer
→ Dev-Team Group
→ App Service Contributor
→ Development Subscription
```

遵守：

# Least Privilege

也就是：

> 只给完成工作真正需要的权限。

---

# Chapter 6：Secret 被 Developer 放进 GitHub

## 案例：Connection String 出现在 Source Code

Security Scanner 突然 Alert。

发现：

```text
Server=production;
User=admin;
Password=P@ssw0rd123;
```

直接写在：

```text
appsettings.json
```

而且已经 Commit。

Alex：

> 「这个 Password 用多久了？」

Developer：

> 「大概……三年？」

Alex：

> 「……」

---

## Alex 改成 Secret Management

Architecture：

```text
Application
     │
     ▼
Managed Identity
     │
     ▼
Key Vault
     │
     ▼
Secret
```

Application 不需要保存 Password。

---

## Chapter 6 最后才解释

使用：

* Managed Identity
* Azure Key Vault
* Secret Rotation
* Certificate Management

目标是：

```text
No Password in Code
No Password in Git
No Password in Pipeline
```

---

# Chapter 7：每个人手动开 Azure Resource，半年后没人知道谁开的

## 案例：Production 和 UAT 完全不同

Developer：

> 「UAT（User Acceptance Testing）可以。」

Production：

> 「不能。」

Alex比较环境。

发现：

```text
UAT
App Service P1v3

Production
App Service S2
```

还有：

```text
Different NSG
Different App Settings
Different Firewall Rule
Different Runtime
```

原因：

> 所有人都在 Azure Portal 手动 Click。

---

## Alex 决定使用 IaC（Infrastructure as Code）

Infrastructure 变成 Code。

例如：

```text
Terraform
   │
   ├── Network
   ├── App Service
   ├── Database
   ├── Storage
   └── Monitoring
```

Deployment：

```text
Git
 ↓
Pull Request
 ↓
Review
 ↓
Pipeline
 ↓
Terraform Plan
 ↓
Terraform Apply
 ↓
Azure
```

---

## Chapter 7 最后才解释：IaC（Infrastructure as Code）

IaC 解决：

```text
Repeatability
Consistency
Version Control
Auditability
Automation
```

Senior Cloud Engineer 不应该问：

> 「谁记得 Production 当初怎样 Configure？」

应该可以直接：

```text
git checkout production
```

看到 Infrastructure Definition。

---

# Chapter 8：Deployment 星期五下午把 Production 炸掉

## 案例：Deploy 成功，但系统失败

Pipeline：

```text
BUILD SUCCESS
DEPLOY SUCCESS
```

五分钟后：

```text
500 Error
500 Error
500 Error
```

Developer：

> 「Pipeline 明明 Green。」

Alex：

> 「Pipeline Green 不代表 Customer Green。」

---

## Alex重新设计 Deployment

以前：

```text
Build
 ↓
Deploy Production
```

现在：

```text
Build
 ↓
Unit Test
 ↓
Security Scan
 ↓
Artifact
 ↓
Deploy Staging
 ↓
Smoke Test
 ↓
Approval
 ↓
Production
 ↓
Health Check
```

---

## Chapter 8 最后才解释：CI/CD

CI（Continuous Integration）

负责：

```text
Code
↓
Build
↓
Test
↓
Artifact
```

CD（Continuous Delivery / Continuous Deployment）

负责：

```text
Artifact
↓
Environment
↓
Validation
↓
Production
```

高级 Deployment Strategy：

* Blue-Green Deployment
* Canary Deployment
* Deployment Slot
* Rolling Deployment

目标不是：

> Deploy 快。

而是：

> **Deploy 可以安全失败。**

---

# Chapter 9：Monitoring 全部 Green，但 Customer 已经骂了半小时

## 案例：Infrastructure Monitoring 不够

Dashboard：

```text
CPU       Green
Memory    Green
Disk      Green
```

Customer：

> 「Payment 不能用！」

Alex调查发现：

Payment Provider API Response：

```text
12 seconds
```

Infrastructure 完全正常。

但是 Business Transaction 已经失败。

---

## Chapter 9 最后才解释：Observability

Senior Cloud Engineer 不只看 Infrastructure Metric。

需要：

### Metrics

例如：

```text
CPU
Memory
Request/sec
Latency
Error Rate
```

### Logs

例如：

```text
Application Log
Security Log
Access Log
Database Log
```

### Traces

追踪：

```text
Booking API
 ↓
Payment API
 ↓
Bank API
 ↓
Ticket API
```

最终形成：

# Observability

而不是单纯 Monitoring。

---

# Chapter 10：Azure Bill 突然从 RM30k 变 RM80k

## 案例：Cloud 很方便，所以大家一直开

Finance：

> 「Alex，为什么 Azure Bill 多了 RM50,000？」

Alex：

> 「……」

调查发现：

```text
Unused VM（Virtual Machine）
Old Snapshot
Premium Disk
Over-sized Database
Idle App Service Plan
Forgotten Public IP
Development Kubernetes Cluster
```

Developer：

> 「那个 VM 应该没有人用了。」

Alex：

> 「应该？」

---

## Chapter 10 最后才解释：FinOps

FinOps（Financial Operations）

Senior Cloud Engineer 也需要管理：

```text
Cost
Usage
Performance
Business Value
```

常见方法：

```text
Tagging
Budget
Cost Alert
Rightsizing
Reserved Instance
Savings Plan
Auto Shutdown
Resource Cleanup
```

Cloud Architecture 不只是：

> 「能不能跑？」

还要问：

> 「值不值得花这个钱跑？」

---

# Chapter 11：整个 Azure Region 出问题，老板问：「我们的 DR 在哪里？」

## 案例：Backup 有，不代表 Disaster Recovery 有

老板：

> 「我们每天都有 Backup，对吗？」

Alex：

> 「有。」

老板：

> 「那为什么系统还不能恢复？」

因为：

```text
Backup ≠ Disaster Recovery
```

Backup 只是 Data。

完整系统还有：

```text
Network
Application
Configuration
Certificate
DNS
Database
Storage
Identity
Secret
```

---

## Alex设计 DR（Disaster Recovery）

Primary：

```text
Malaysia West
```

Secondary：

```text
Southeast Asia
```

Architecture：

```text
               Traffic Manager
                    │
          ┌─────────┴─────────┐
          ▼                   ▼
     Primary Region      DR Region
          │                   │
      Application         Application
          │                   │
      Database ───────► Replica
```

---

## Chapter 11 最后才解释：RTO 与 RPO

### RTO（Recovery Time Objective）

问：

> 系统最多可以 Down 多久？

例如：

```text
RTO = 1 hour
```

代表：

> Disaster 后 1 小时内必须恢复。

### RPO（Recovery Point Objective）

问：

> 最多可以接受损失多少 Data？

例如：

```text
RPO = 5 minutes
```

代表最多接受：

```text
5 minutes data loss
```

这两个数字会直接影响 DR Architecture 和 Cost。

---

# Chapter 12：公司有 200 个 Azure Resource，开始失控

## 案例：每个 Team 都有自己的玩法

Team A：

```text
Production
```

Team B：

```text
prod
```

Team C：

```text
PRD
```

Resource Name：

```text
app1
test-new
server-final
server-final2
dont-delete
```

Alex看到：

> 「dont-delete 是什么？」

Developer：

> 「不知道，但以前的人说不能 Delete。」

---

## Chapter 12 最后才解释：Cloud Governance

需要建立：

```text
Management Group
Subscription
Resource Group
Naming Convention
Tagging
Policy
RBAC
Budget
Security Baseline
```

例如：

```text
Management Group
│
├── Production
│   ├── Transport Subscription
│   └── Payment Subscription
│
└── Non-Production
    ├── Development
    └── UAT
```

使用 Azure Policy 强制：

```text
Required Tags
Allowed Regions
Allowed VM Sizes
No Public Database
Encryption Required
```

---

# Chapter 13：老板问：「我们到底应该用 App Service、Container 还是 Kubernetes？」

## 案例：不要看到 Kubernetes 就兴奋

Developer：

> 「我们应该全部 Migration 去 AKS。」

AKS（Azure Kubernetes Service）

老板：

> 「为什么？」

Developer：

> 「因为 Kubernetes 是 Enterprise。」

Alex：

> 「这不是理由。」

---

Alex开始比较：

```text
Requirement
    │
    ├── Simple Web/API
    │       ↓
    │   App Service
    │
    ├── Container + Simple Scaling
    │       ↓
    │   Container Apps
    │
    └── Complex Microservices
            ↓
           AKS
```

---

## Chapter 13 最后才解释：Compute Decision

Senior Cloud Engineer 不应该：

> 先选 Technology，再找理由。

而应该：

```text
Business Requirement
       ↓
Technical Requirement
       ↓
Operational Complexity
       ↓
Cost
       ↓
Platform Decision
```

例如：

| Requirement           | Possible Choice               |
| --------------------- | ----------------------------- |
| 普通 Web Application    | App Service                   |
| Serverless Event      | Azure Functions               |
| Container Workload    | Azure Container Apps          |
| Complex Microservices | AKS（Azure Kubernetes Service） |
| Legacy Application    | VM（Virtual Machine）           |

---

# Chapter 14：Cloud Engineer 最难的工作，原来不是 Azure

半年后。

新的 Engineer 问 Alex：

> 「Senior Cloud Engineer 最重要是不是要记住所有 Azure Service？」

Alex摇头。

他说：

> 「Azure 有几百个 Service。」
>
> 「你不可能全部背。」

真正重要的是：

```text
Business Requirement
        ↓
Architecture
        ↓
Security
        ↓
Reliability
        ↓
Performance
        ↓
Operations
        ↓
Cost
```

例如老板说：

> 「我们需要 99.99% Availability。」

Junior Engineer 可能想：

> 「用什么 Azure Service？」

Senior Engineer 会先问：

```text
哪个 System？
哪个 Component？
Downtime 怎么计算？
Database 怎么 HA？
Region Failure 怎么办？
RTO 是多少？
RPO 是多少？
Budget 是多少？
```

---

# Chapter 14 最后才解释：Senior Cloud Engineer 的真正职责

Junior Cloud Engineer 经常关注：

```text
How to create?
```

例如：

> How to create App Service？

Mid-Level Engineer 开始关注：

```text
How to configure?
```

例如：

> App Service 怎样配置 Auto Scaling？

Senior Cloud Engineer 更关注：

```text
Why this architecture?
What can fail?
How do we detect it?
How do we recover?
How much does it cost?
How do we secure it?
How do we automate it?
```

最终思维从：

```text
Resource
```

升级成：

```text
System
```

再升级成：

```text
Platform
```

---

# 整套 Senior Cloud Engineer 漫画课程路线

```text
Chapter 1
Production Incident
        ↓
Troubleshooting

Chapter 2
System Slow
        ↓
Performance & Bottleneck

Chapter 3
Traffic Explosion
        ↓
Scalability & Elasticity

Chapter 4
Database Exposed
        ↓
Networking & Security

Chapter 5
Everyone Is Owner
        ↓
IAM（Identity and Access Management）

Chapter 6
Password in Git
        ↓
Secret Management

Chapter 7
Manual Azure Configuration
        ↓
IaC（Infrastructure as Code）

Chapter 8
Deployment Disaster
        ↓
CI/CD（Continuous Integration / Continuous Delivery）

Chapter 9
Everything Green, Customer Angry
        ↓
Observability

Chapter 10
Cloud Bill Explosion
        ↓
FinOps（Financial Operations）

Chapter 11
Region Failure
        ↓
DR（Disaster Recovery）

Chapter 12
200 Resources Out of Control
        ↓
Cloud Governance

Chapter 13
App Service vs Container vs Kubernetes
        ↓
Architecture Decision

Chapter 14
Why Senior Engineers Think Differently
        ↓
Senior Cloud Architecture Thinking
```

---

# 最终 Boss：Senior Cloud Engineer 的一天

早上 9:00：

```text
Production Incident
```

10:00：

```text
Security Review
```

11:00：

```text
Architecture Discussion
```

下午 2:00：

```text
Terraform Pull Request
```

3:00：

```text
Performance Investigation
```

4:00：

```text
Cost Review
```

5:00：

```text
DR Planning
```

5:30：

老板：

> 「Alex，还有一个小问题。」

Alex：

> 「什么？」

老板：

> 「明天 Marketing Promotion，Traffic 预计增加 10 倍。」

Alex沉默五秒。

然后打开 Architecture Diagram。

因为现在的他已经知道：

> **Senior Cloud Engineer 的工作，不是确保 Cloud 永远不会出问题。**
>
> **而是在问题发生之前知道哪里可能坏；问题发生时知道怎么看；问题解决之后确保同样的问题不会再发生。**

这就是从：

**「会用 Cloud」**

走向：

# 「会设计、保护、运营 Cloud Platform」。
