# 《IT部今天又出事了！》

## ——用故事学会 ITIL 4

### 漫画整体设定

故事发生在一家快速成长的公司：

**公司：NovaTech 新星科技**

公司最近业务增长很快，但是 IT 部门越来越混乱：

* 系统经常突然不能用
* 用户直接 WhatsApp IT 人员报问题
* 同一个问题重复发生
* 系统修改没有记录
* 新系统上线后才发现没人会用
* IT 部门认为自己很忙，业务部门却认为 IT 什么都没做好
* 老板开始问：“我们每年花这么多钱在 IT，到底创造了什么价值？”

于是，公司请来一位新的 **IT Service Manager——Alex**。

Alex 没有一开始就给大家上 ITIL 课程。

他说：

**“我们先解决问题。”**

故事也从这里开始。

---

# Chapter 1：IT 到底在做什么？

## 主题：Service Management & Value

### 案例：《打印机修好了，为什么老板还是生气？》

星期一早上。

Finance Department：

“IT！打印机坏了！”

IT Technician 小明马上冲过去。

检查网络、重新安装 Driver、Restart Printer。

20分钟后：

“好了！”

小明非常开心。

> “Ticket solved！”

但是 Finance Manager 却非常生气：

> “我们的 Invoice 已经迟了两个小时！”

小明很困惑。

“可是打印机已经修好了啊？”

Alex 问他：

> “你的目标是修打印机，还是让 Finance 可以完成工作？”

小明第一次意识到：

**IT Service 的价值，不是设备正常，而是帮助业务获得结果。**

### 本章冲突

IT认为：

> “技术恢复 = 工作完成。”

Business认为：

> “业务恢复 = 工作完成。”

### 本章最后才解释 ITIL

**Service Management**

IT Service Management 的目标并不是单纯管理电脑、服务器和软件，而是通过服务帮助客户获得价值。

核心概念：

**Value = Outcomes + Experience**

因此处理 IT 工作时，第一个问题不应该只是：

> “什么坏了？”

还应该问：

> “它影响了什么业务？”

---

# Chapter 2：网站突然挂了！

## 主题：Incident Management

### 案例：《星期五下午的灾难》

星期五下午 4:45。

Sales：

> “Website 打不开！”

Marketing：

> “客户正在投诉！”

CEO：

> “发生什么事情？”

IT Department 瞬间混乱。

Network Team：

> “不是 Network。”

Server Team：

> “Server CPU 正常。”

Application Team：

> “可能是 Database。”

Database Team：

> “为什么什么事情都是 Database？”

五个人同时调查，却没有一个人负责协调。

15分钟过去。

30分钟过去。

老板不断问：

> “什么时候恢复？”

没人知道。

Alex走进办公室：

> “现在谁是 Incident Owner？”

所有人安静。

### Alex开始重新组织

第一步：

记录 Incident。

第二步：

判断 Impact 和 Urgency。

第三步：

由于整个公司网站无法使用：

**Priority = P1 Critical Incident**

第四步：

指定 Incident Coordinator。

第五步：

技术团队调查。

第六步：

定时向 Business Update。

最后发现：

Web Server Connection Pool 满了。

重新启动相关服务后：

网站恢复。

### 本章最后解释操作过程

**Incident Management**

目标：

> 尽快恢复正常服务。

标准流程：

**User Report → Log → Categorize → Prioritize → Diagnose → Escalate → Resolve → Confirm → Close**

Priority 通常由两个因素决定：

**Impact × Urgency**

例如：

| Impact | Urgency | Priority |
| ------ | ------- | -------- |
| High   | High    | P1       |
| High   | Medium  | P2       |
| Medium | Medium  | P3       |
| Low    | Low     | P4       |

关键思想：

**Incident Management 不一定寻找根本原因。**

它首先解决：

> “怎样最快恢复服务？”

---

# Chapter 3：为什么每个星期都坏一次？

## 主题：Problem Management

### 案例：《神秘的星期一故障》

连续四个星期。

每到星期一上午：

ERP System 都会变得非常慢。

IT 每次的解决方式都一样：

> “Restart Server。”

Restart之后恢复正常。

Ticket Closed。

第五个星期。

又发生了。

Finance Manager终于忍不住：

> “你们到底修了什么？”

IT Technician回答：

> “每一次都有恢复啊。”

Alex拿出过去一个月的 Incident Records。

四次 Incident：

**INC001**
ERP Slow

**INC017**
ERP Slow

**INC035**
ERP Slow

**INC052**
ERP Slow

Alex：

> “这不是四个不同的问题。”

> “这是一个 Problem。”

调查后发现：

星期日晚上的 Backup Job 与星期一早上的 ERP Batch Job 同时大量占用 Database Resources。

### 临时解决方案

调整 Restart Procedure。

记录：

**Known Error + Workaround**

### 永久解决方案

重新设计 Backup Schedule。

### 本章最后解释

Incident问：

> “怎样恢复？”

Problem问：

> “为什么发生？”

Problem Management流程：

**Detect → Log → Analyze → Root Cause → Workaround → Known Error → Permanent Fix**

关键概念：

**Incident ≠ Problem**

一个 Problem 可以产生很多 Incidents。

---

# Chapter 4：只是改一个 Firewall Rule 而已

## 主题：Change Enablement

### 案例：《五分钟的修改，五小时的灾难》

Engineer：

> “只是加一个 Firewall Rule。”

同事：

> “有 Change Request 吗？”

Engineer：

> “这么小的事情不用啦。”

晚上 8 点。

Engineer修改 Firewall。

晚上 8:05。

ERP Offline。

CRM Offline。

VPN Offline。

老板：

> “发生什么事？！”

Engineer：

> “我只是改了一条 Rule……”

Alex：

> “有 Rollback Plan 吗？”

Engineer：

> “……”

### 第二天

Alex没有禁止所有 Change。

反而告诉团队：

> “ITIL不是为了阻止 Change。”

> “是为了让 Change 的风险可以被控制。”

### 本章最后解释

Change Enablement：

目标是：

**最大化成功 Change，同时控制风险。**

Change分为：

**Standard Change**
低风险、重复、预先批准。

例如：

建立标准 User Account。

**Normal Change**
需要评估和授权。

例如：

修改 Production Firewall。

**Emergency Change**
必须紧急实施。

例如：

修复严重 Security Vulnerability。

流程：

**Request → Assess Risk → Authorize → Schedule → Implement → Validate → Review**

每一个重要 Change 至少应该考虑：

* 为什么要改？
* 风险是什么？
* 谁批准？
* 什么时候实施？
* 如何测试？
* 如果失败，如何 Rollback？

---

# Chapter 5：星期一上线，星期一爆炸

## 主题：Release & Deployment Management

### 案例：《ERP 2.0》

Project Team开发了六个月的新 ERP。

Developer：

> “Testing passed！”

Project Manager：

> “Monday Go Live！”

星期一上午。

ERP 2.0正式上线。

10分钟后：

Finance：

> “按钮在哪里？”

Warehouse：

> “Scanner不能用了！”

Sales：

> “Customer data不见了！”

IT：

> “我们测试过啊！”

Alex：

> “你们测试了 Software。”

> “但有没有测试 Service？”

大家沉默。

### 调查发现

Application正常。

但：

* User Training 没完成
* Scanner Compatibility 没测试
* Support Team 不知道新系统功能
* Knowledge Article 没准备
* Rollback Plan 不完整

### 本章最后解释

Release Management关注：

> “什么时候以及以什么方式发布新的服务或功能？”

Deployment Management关注：

> “怎样把组件部署到目标环境？”

成功上线不能只问：

> “Software works?”

还要问：

> “Service ready?”

Checklist：

**Build → Test → Release Planning → Communication → Training → Deployment → Validation → Early Life Support**

---

# Chapter 6：我只是要一个新账号

## 主题：Service Request Management

### 案例：《一个账号等了七天》

新员工 Sarah 第一天上班。

Manager：

> “帮她开 Email、VPN 和 CRM Account。”

IT：

> “Send email。”

Manager发送Email。

三天后。

没人回复。

Manager再发：

> “Any update?”

IT Technician A：

> “我以为 B 在做。”

B：

> “我以为是 Infrastructure Team。”

第七天，Sarah仍然没有 CRM。

Sarah：

> “所以……我今天继续看公司介绍？”

### Alex设计 Service Catalog

用户以后不再写：

> “Hi IT, please help.”

而是选择：

**New Employee IT Setup**

自动包含：

* Email Account
* Laptop
* VPN
* CRM
* Required Software
* Access Approval

并设定 SLA。

### 本章最后解释

Service Request 通常是：

**预定义、重复、低风险的用户需求。**

例如：

* Password Reset
* Software Installation
* Access Request
* New Account
* Laptop Request
* Information Request

流程：

**Submit → Validate → Approve → Fulfil → Confirm → Close**

重点：

Incident 是：

> “Something is broken.”

Service Request 是：

> “I need something.”

---

# Chapter 7：到底是谁负责？

## 主题：Service Desk

### 案例：《用户的IT联系人名单》

员工桌上贴着一张纸：

Network问题 → 找David
ERP问题 → 找Jason
Laptop问题 → 找小明
Password问题 → 找Sarah
不知道什么问题 → 群里问

结果：

David休假。

用户：

> “那我怎么办？”

Alex把纸撕下来。

换成：

**Contact IT Service Desk**

### 新模式

用户不需要知道后台谁负责。

Service Desk负责：

* 接收
* 记录
* 分类
* 初步处理
* 沟通
* Escalation
* Follow-up

用户只需要知道：

> “有问题，找 Service Desk。”

### 本章最后解释

Service Desk 是：

**Single Point of Contact (SPOC)**

它不是单纯的“接电话部门”。

Service Desk代表的是：

**User ↔ Service Provider**

之间统一的沟通入口。

---

# Chapter 8：老板说IT太慢

## 主题：Service Level Management

### 案例：《“尽快”到底是多久？》

CEO：

> “IT处理问题太慢。”

IT Manager：

> “我们已经很快了。”

CEO：

> “多快？”

IT Manager：

> “通常很快。”

CEO：

> “……”

Alex问：

> “P1 Incident多久应该恢复？”

没人知道。

> “New User Account多久完成？”

没人知道。

> “Email问题多久回应？”

还是没人知道。

原来大家一直在使用一个非常危险的服务标准：

**ASAP。**

### Alex开始定义服务目标

例如：

P1：

Response：15分钟
Target Restore：2小时

P2：

Response：30分钟
Target Restore：4小时

P3：

Response：4小时
Target Restore：2个工作日

### 本章最后解释

Service Level Management的目的：

建立 Business 与 IT 对服务质量的共同理解。

常见指标：

* Availability
* Response Time
* Resolution Time
* Customer Satisfaction
* Service Performance

重点不是：

> “IT觉得自己表现不错。”

而是：

> “IT与Business是否对‘好服务’有共同定义？”

---

# Chapter 9：服务器99.9%正常，为什么客户还是投诉？

## 主题：Monitoring & Event Management

### 案例：《绿色Dashboard的谎言》

IT Dashboard：

Server：GREEN
Network：GREEN
Database：GREEN

IT Manager：

> “Everything healthy。”

Customer Service：

> “客户全部在投诉 Checkout 很慢。”

IT：

> “不可能，Dashboard全部绿色。”

Alex打开网站。

点击：

**Checkout**

等待。

10秒。

20秒。

30秒。

Alex：

> “Server活着。”

> “但是Service不好用。”

### 本章最后解释

Monitoring不能只监控 Infrastructure。

应该从：

**Component → Application → Service → Business Experience**

逐层监控。

Event可能包括：

**Informational Event**

例如 Backup Completed。

**Warning Event**

例如 Disk Usage 80%。

**Exception Event**

例如 Database Connection Failed。

真正有价值的Monitoring应该帮助IT：

> 在用户报问题之前发现问题。

---

# Chapter 10：IT到底花钱买了什么？

## 主题：IT Asset Management & Service Configuration Management

### 案例：《消失的50台Laptop》

Finance：

> “我们去年买了500台Laptop。”

IT Asset List：

> “系统里面只有450台。”

Finance：

> “另外50台呢？”

IT：

> “可能在员工那里。”

Finance：

> “哪些员工？”

IT：

> “……”

与此同时：

某Production Server发生故障。

Engineer：

> “这台Server跑什么系统？”

没人知道。

Engineer：

> “如果Restart会影响什么？”

还是没人知道。

### Alex提出两个问题

第一：

> “我们拥有什么？”

第二：

> “这些东西之间是什么关系？”

### 本章最后解释

IT Asset Management关注：

**资产的生命周期、成本、责任和价值。**

例如：

Laptop
Server
Software License
Mobile Device

Service Configuration Management关注：

**Configuration Items（CI）以及它们之间的关系。**

例如：

Customer Portal
↓
Web Server
↓
Application Server
↓
Database
↓
Storage

当Database出现问题时，就能判断：

> 哪些Services可能受到影响？

---

# Chapter 11：Knowledge只存在Jason脑里

## 主题：Knowledge Management

### 案例：《Jason去旅行了》

星期一。

ERP出现问题。

Technician：

> “这个Jason会修。”

同事：

> “Jason在哪里？”

> “Japan。”

大家开始找以前的WhatsApp。

终于找到Jason六个月前的一句话：

> “Restart那个service就可以。”

但是：

哪个Service？

没人知道。

### Jason回来以后

Alex：

> “从今天开始，你脑里的东西属于公司。”

Jason：

> “啊？”

Alex建立 Knowledge Base。

每一次重要解决方案记录：

* Symptoms
* Cause
* Resolution
* Workaround
* Owner
* Last Updated

### 本章最后解释

Knowledge Management的目标：

**让正确的信息，在正确的时间，提供给正确的人。**

成熟的IT组织不应该依赖：

> “那个谁知道。”

而应该做到：

> “组织知道。”

---

# Chapter 12：我们已经很忙了，为什么还要改进？

## 主题：Continual Improvement

### 案例：《1000张Ticket》

月底。

IT Team宣布：

> “这个月我们关闭了1000张Tickets！”

大家鼓掌。

Alex问：

> “上个月呢？”

“900。”

> “所以Ticket增加了？”

大家安静。

Alex继续问：

> “其中多少是重复问题？”

“300。”

> “多少是Password Reset？”

“250。”

> “为什么不Automation？”

没人回答。

### Alex写下三个问题

**我们现在在哪里？**

**我们想去哪里？**

**怎样到达那里？**

于是团队决定：

自动化 Password Reset。

下个月：

Password Tickets：

250 → 40。

### 本章最后解释

Continual Improvement不是一年一次的大Project。

而是持续寻找：

> “下一件值得改善的事情是什么？”

基本思路：

**Vision → Current State → Target State → Plan → Action → Measure → Sustain**

核心：

**Measure → Learn → Improve**

---

# Final Chapter：真正的ITIL

## 《原来ITIL不是流程大全》

半年以后。

NovaTech的IT部门已经完全不同。

Incident发生：

大家知道谁负责。

重复Incident：

自动进入Problem Investigation。

Production Change：

必须Risk Assessment。

New Employee：

直接使用Service Request。

用户：

只联系Service Desk。

Manager：

查看Service Level Dashboard。

Engineer：

使用Knowledge Base。

IT Manager：

每个月进行Continual Improvement Review。

CEO再次问Alex：

> “所以ITIL到底是什么？”

Alex没有拿出一本厚厚的书。

他在白板上写：

# VALUE

然后说：

> “ITIL不是为了让IT增加更多流程。”

> “流程只是工具。”

> “真正的问题永远是——”

> **“我们怎样和客户一起创造价值？”**

---

# 最终教学页：把整部漫画串起来

读完整个故事后，才向学习者正式展示：

**ITIL Service Value System（SVS）**

它把前面的所有故事连接起来。

### Guiding Principles

1. Focus on Value
2. Start Where You Are
3. Progress Iteratively with Feedback
4. Collaborate and Promote Visibility
5. Think and Work Holistically
6. Keep It Simple and Practical
7. Optimize and Automate

### Four Dimensions

每一个Service都应该从四个角度考虑：

**Organizations & People**

谁负责？需要什么Skills？

**Information & Technology**

需要什么系统、数据和技术？

**Partners & Suppliers**

是否依赖Vendor、Cloud Provider或Supplier？

**Value Streams & Processes**

工作怎样从Request一直流到Value？

---

# 漫画统一章节公式

为了让整套漫画有统一风格，每一个Chapter都不要用：

**Theory → Definition → Example**

而统一采用：

**Case → Chaos → Business Impact → Investigation → Decision → Solution → Result → ITIL Reveal**

也就是说：

### 第1–2页：正常工作

角色正在工作，让读者先理解业务环境。

### 第3–4页：事件发生

例如：

“Website down！”

### 第5–6页：错误处理

让角色按照常见但错误的方法处理。

重点是让读者产生：

> “我公司也是这样！”

### 第7–8页：后果出现

展示Business Impact，而不只是Technical Impact。

例如：

Lost Sales
Customer Complaints
Employee Downtime
SLA Breach

### 第9–10页：Alex介入

Alex不直接说：

> “According to ITIL……”

而是通过问题引导：

> “谁负责？”

> “影响多少用户？”

> “以前发生过吗？”

> “如果Change失败怎么办？”

### 第11–12页：团队解决问题

让读者看到正确做法产生结果。

### 第13页：ITIL Reveal

这时候才出现：

**“你刚刚看到的，其实就是 Incident Management。”**

### 第14页：操作流程

用简单流程图：

**Report → Log → Categorize → Prioritize → Investigate → Resolve → Close**

### 第15页：Key Takeaway

只留下3个重点。

例如 Incident Management：

**① Restore service quickly**

**② Prioritize based on business impact**

**③ Incident ≠ Problem**

### 第16页：下一章伏笔

例如：

网站恢复。

大家准备回家。

突然同一个Engineer说：

> “奇怪……这个月已经第三次发生了。”

Alex回头：

> “第三次？”

**To Be Continued → Chapter 3: Problem Management**

这样每一个ITIL知识点就不是独立教材，而会成为一部连续的“IT部门成长故事”。
