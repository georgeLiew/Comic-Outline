# Why Am I Even Busier Now That I Don’t Write Code Anymore?

## A Practical Comic Course for Software Development Managers

---

# Chapter 1: Monday Morning — Everything Is a Priority

## Case

Monday, 9:05 AM.

Alex has just sat down when more than a dozen messages appear in Teams.

**Product Owner:**

> “The customer wants this feature. It must go live this month.”

**Sales:**

> “This customer is very important. Can we prioritize this first?”

**Operations:**

> “Production had another issue yesterday.”

**Developer:**

> “Last week’s requirement still hasn’t been confirmed.”

**Boss:**

> “Alex, why is the Q3 roadmap delayed?”

Alex opens Jira.

He discovers that the team is working on all of these at the same time:

- 3 Projects
- 8 Features
- 12 Bugs
- 4 Production Issues
- 2 Technical Debt items

Everyone says their work is the most important.

Alex suddenly realizes:

The first job of a Software Development Manager is not to **“push developers to work faster.”**

It is to:

**Decide where the team should spend its time.**

## How Alex Handles It

He does not immediately ask:

> “Who is available to do this?”

Instead, he first categorizes all incoming work:

| Type | Example |
|---|---|
| Production | Payment Failure |
| Committed Delivery | Customer Project |
| Product Feature | New Promotion Module |
| Technical Debt | Upgrade .NET |
| Improvement | CI/CD Enhancement |

Then he establishes a priority rule:

**P0 — Production Critical**

↓

**P1 — Contract / Committed Delivery**

↓

**P2 — Business Value Feature**

↓

**P3 — Improvement**

↓

**P4 — Technical Debt**

Finally, he tells the stakeholders:

> “It’s not that we won’t do it. We need to decide what we are choosing to do first.”

## Only at the End of the Chapter: Priority Management

A manager does not simply manage tasks.

What a manager really manages is:

**Capacity × Priority × Business Value × Risk**

The process:

**Business Request**

↓

**Understand Business Impact**

↓

**Estimate Effort**

↓

**Identify Dependencies**

↓

**Identify Risks**

↓

**Compare Priorities**

↓

**Allocate Team Capacity**

↓

**Commit to Delivery**

---

# Chapter 2: Business Doesn’t Even Have Requirements Yet, but They Ask, “How Many Months?”

## Case

Sales is preparing for a tender.

The tender requires the development of a new Transport Management System.

Sales asks:

> “Alex, how long will this system take?”

Alex:

> “Where are the requirements?”

Sales:

> “We don’t have them yet.”

Alex:

> “Business flow?”

Sales:

> “The customer hasn’t provided it.”

Alex:

> “Integrations?”

Sales:

> “Not sure.”

Then Sales asks:

> “So... can you give us the mandays?”

The first time this happens, Alex estimates:

**120 mandays.**

Sales uses that number for the quotation.

Two months later, the customer’s actual requirements arrive:

- Mobile App
- Payment Gateway
- ERP Integration
- Reporting
- Offline Mode
- Approval Workflow
- Notifications
- Role Permissions

The developers re-estimate the project:

**280 mandays.**

Alex’s boss asks:

> “Why is the difference so huge?”

## Alex Learns an Important Principle

**Unknown Requirements ≠ Detailed Estimation**

But during a tender, you also cannot simply answer:

> “I don’t know.”

So Alex switches to a:

### ROM Estimate

**Rough Order of Magnitude**

For example:

**Estimated Delivery: 6–9 months**

And he clearly states the assumptions:

- Web System
- 1 Mobile App
- Existing Payment Gateway
- Maximum 3 External Integrations
- Standard Reporting
- No Offline Capability
- Existing Infrastructure

He also states:

**Estimate Confidence: ±40%**

As the requirements become clearer:

**Tender**

→ **ROM Estimate**

→ **Discovery**

→ **High-Level Design**

→ **Feature Breakdown**

→ **Detailed Estimate**

→ **Delivery Baseline**

## Only at the End of the Chapter: Estimation Management

A Software Development Manager is not responsible for **“guessing a date.”**

The manager is responsible for managing:

**Estimate Confidence**

The process:

**Scope**

↓

**Assumptions**

↓

**Dependencies**

↓

**Complexity**

↓

**Risk**

↓

**Historical Velocity**

↓

**Buffer**

↓

**Estimate Range**

Do not say:

> “It will take six months.”

Say:

> “Based on our current assumptions, we estimate 6–9 months. After Discovery, we should be able to narrow the estimate to approximately ±15%.”

---

# Chapter 3: The Developer Says, “The Requirement Isn’t Clear”

## Case

The PO creates a User Story:

> **As a user, I want to cancel a booking.**

Developer:

> “Do we refund the customer after cancellation?”

PO:

> “Probably.”

Developer:

> “What about partial refunds?”

PO:

> “I need to ask Business.”

Developer:

> “What if the Payment Gateway has already settled the transaction?”

PO:

> “Not sure.”

Developer:

> “Can Admin override it?”

PO:

> “Probably.”

The Sprint started three days ago.

The developer still has not started coding.

Management asks:

> “Why is Development so slow?”

## Alex Does Not Tell the Developer to “Just Start First”

He pauses development.

He calls a **Refinement session**.

The requirement is broken down into:

### Business Rules

- Under what conditions can a booking be cancelled?
- How long before departure can it be cancelled?
- Who is allowed to cancel it?

### Financial Rules

- Full Refund?
- Partial Refund?
- Cancellation Fee?

### Exceptions

- Payment Settled
- Trip Started
- Voucher Used
- Promo Code
- Partial Payment

### Permissions

- Customer
- Counter
- Admin
- Supervisor

Finally, Alex defines the:

**Definition of Ready**

A Story cannot enter a Sprint unless it has:

- Business Flow
- Acceptance Criteria
- Business Rules
- Exception Cases
- Dependencies
- UI/UX
- API Impact

---

# Chapter 4: The Project Manager Says, “It Must Go Live This Month”

## Case

PM:

> “Management already promised the customer that we’ll go live on the 30th.”

Alex:

> “Development estimates six weeks.”

PM:

> “But the customer wants it in four.”

Alex:

> “Then we reduce the scope.”

PM:

> “We can’t reduce the scope.”

Alex:

> “Add developers?”

PM:

> “There’s no additional budget.”

Finally, the PM asks:

> “Can the developers just work overtime?”

Alex realizes they have encountered a classic project management problem:

**Scope is fixed.**

**Time is fixed.**

**Resources are fixed.**

Yet everyone expects:

**Quality to remain unchanged.**

## Alex Draws Four Variables

**Scope**

**Time**

**Cost / Resources**

**Quality / Risk**

He tells the stakeholders:

> “We can go live on the 30th, but we need to choose a trade-off.”

### Option A

Go live on the 30th

→ Reduce Scope

### Option B

Full Scope

→ Extend Timeline

### Option C

Full Scope + Go Live on the 30th

→ Add Resources / Cost

Instead of quietly turning:

**Quality**

into the thing that gets sacrificed.

---

# Chapter 5: The Developer Worked for Two Weeks — Then We Realized the Architecture Was Wrong

## Case

The team needs to develop a Notification System.

The developer designs:

**Booking System**

→ Direct Call to Email API

Later, Business says:

> “We also need SMS.”

The developer adds SMS.

Then:

> “We need WhatsApp too.”

Later:

> “Marketing will need to use this in the future as well.”

Slowly, the system becomes:

**Booking**

→ **Email → SMS → WhatsApp → Push Notification**

Every module starts implementing its own notification logic.

Alex realizes:

**The developer is solving today’s ticket.**

But the manager must think about:

**What will this system look like six months from now?**

## Alex Requires Major Features to Go Through a Technical Design Review

The developer proposes:

**Booking**

↓

**Event**

↓

**Message Queue**

↓

**Notification Service**

↓

**Email / SMS / WhatsApp / Push**

The team reviews:

- Scalability
- Failure Handling
- Retry
- Logging
- Security
- Cost
- Dependencies
- Maintainability

---

# Chapter 6: The Code Review Passed — Production Still Exploded

## Case

Friday, 5:00 PM.

A new version is deployed.

5:30 PM.

Operations:

> “All payments are failing!”

Developer:

> “It works on my local machine.”

QA:

> “It worked in Staging too.”

Eventually, they discover the Production environment variable:

```text
PAYMENT_API_V2=false
```

But the developer’s new code assumes:

```text
PAYMENT_API_V2=true
```

## Alex Starts Asking Questions

The question is not:

> “Who deployed it?”

The question is:

> “Why did our process allow this mistake to happen?”

So Alex establishes:

**Code**

↓

**Pull Request**

↓

**Automated Tests**

↓

**Build Artifact**

↓

**Deploy to Staging**

↓

**Integration Test**

↓

**Approval**

↓

**Production**

↓

**Smoke Test**

↓

**Monitoring**

And adds:

- Environment Configuration Validation
- Deployment Checklist
- Rollback Plan
- Database Migration Check
- Feature Flags

---

# Chapter 7: Production Is Down — Everyone Is Looking for Someone to Blame

## Case

1:00 AM.

Payment Service Error Rate:

**47%**

Boss:

> “Who deployed this?”

PM:

> “Is this a Developer issue?”

Developer:

> “QA tested it.”

QA:

> “That’s what the requirement said.”

Everyone starts defending themselves.

Alex says:

> “We are not discussing who is at fault right now.”

The first priority is:

**Restore Service**

## Incident Handling

**Detect**

↓

**Assess Severity**

↓

**Assign Incident Commander**

↓

**Mitigate**

↓

**Rollback / Fix**

↓

**Verify**

↓

**Communicate**

↓

**Postmortem**

↓

**Corrective Action**

Only after the service is restored do they perform:

### Root Cause Analysis

Why did Payment fail?

Because of a timeout.

Why did it time out?

The database query was slow.

Why was the query slow?

Missing Index.

Why wasn’t it discovered earlier?

The Staging dataset was too small.

Why was the Staging dataset too small?

There was no Performance Test Dataset.

The real root cause was not:

> “The developer forgot to create an index.”

It was:

**The Delivery Process had no Performance Validation.**

---

# Chapter 8: Your Best Developer Says, “I’m Resigning”

## Case

Senior Developer:

> “Alex, I’m planning to resign.”

Alex is shocked.

> “Is it because of salary?”

Developer:

> “No.”

> “Every Production Issue comes to me.”

> “Whenever the Juniors don’t know something, they come to me.”

> “I handle the Architecture.”

> “I handle the Code Reviews.”

> “If I take one day of leave, everyone contacts me.”

Alex finally realizes:

This developer is not merely the team’s most important asset.

He has become a:

**Single Point of Failure.**

## Alex Starts Changing the Team Structure

Before:

**Senior Developer**

↓ ↓ ↓ ↓ ↓

**Everyone**

After:

**Tech Lead**

↓

**Senior A / Senior B**

↓

**Developers**

And he introduces:

- Documentation
- Pair Programming
- Knowledge Sharing
- Rotation
- Secondary Owners
- Runbooks

A manager’s goal is not:

**To find a Superman.**

The goal is:

**To build a team that can still operate without Superman.**

---

# Chapter 9: The Junior Developer Keeps Underperforming

## Case

Alex notices that a Junior Developer is delayed in every Sprint.

His first reaction:

**Poor performance.**

But during a 1-on-1, he discovers something else.

Junior:

> “Actually, I don’t understand the Business Flow for many of the tickets.”

Alex:

> “Why didn’t you ask?”

Junior:

> “The Seniors are always busy. I’m afraid of disturbing them.”

Alex realizes the problem may not be skill.

It could be:

- Knowledge
- Guidance
- Confidence
- Requirements
- Workload
- Tooling

## Alex Creates a Developer Growth Plan

**Junior**

→ Coding Fundamentals

→ Debugging

→ Business Understanding

→ Independent Feature Delivery

→ System Design

→ Mentoring

→ Technical Leadership

Every month, their 1-on-1 covers:

- **Performance**
- **Growth**
- **Blockers**
- **Career**

Instead of waiting for the annual Performance Review to say:

> “Your performance isn’t good enough.”

---

# Chapter 10: The Boss Asks, “Why Do We Have More Developers but Delivery Isn’t Getting Faster?”

## Case

Before:

**5 Developers**

→ **20 Features / Quarter**

Later:

**10 Developers**

→ **27 Features / Quarter**

Boss:

> “We doubled the headcount. Why aren’t we delivering 40 features?”

Alex starts analyzing how developers actually spend their day:

- Meetings: 2 hours
- Production Support: 1 hour
- Requirement Clarification: 1 hour
- Waiting for Environment: 0.5 hours
- Coding: 3.5 hours

The real problem is not:

**Not enough developers.**

The real problem is:

**Low Flow Efficiency.**

## Alex Starts Looking at Engineering Metrics

Not just:

- ❌ Lines of Code
- ❌ Number of Tickets
- ❌ 100% Developer Utilization

Instead:

- Lead Time
- Cycle Time
- Deployment Frequency
- Change Failure Rate
- MTTR
- Escaped Defects
- Rework Rate
- Blocked Time

For example:

**Requirement**

→ 3 Days Waiting

**Development**

→ 2 Days

**QA**

→ 4 Days Waiting

**Testing**

→ 1 Day

Total Lead Time:

**10 Days**

Actual Coding:

**2 Days**

The problem is not that developers are slow.

The problem is:

**Eight days were spent waiting.**

---

# Chapter 11: Business Keeps Inserting “Urgent” Requests

## Case

The original Sprint contains:

- Feature A
- Feature B
- Feature C

Tuesday:

> “The CEO wants Feature D.”

Wednesday:

> “The customer wants Feature E.”

Thursday:

> “Operations needs Fix F.”

At the end of the Sprint:

- A: 70% completed
- B: 40% completed
- C: Not started

Management:

> “Why did we fail our commitment again?”

## Alex Establishes Change Control

Any Urgent Request entering an active Sprint must answer:

1. What is the Business Impact?
2. Why can’t the deadline change?
3. What happens if we don’t do it?
4. Which existing scope will be removed?

The new rule becomes:

**New Work In = Existing Work Out**

Not:

**New Work In = Developers Work Overtime**

---

# Chapter 12: Everyone Is Busy, but the Project Is Still Delayed

## Case

Backend:

> “Waiting for UI.”

Frontend:

> “Waiting for API.”

QA:

> “Waiting for Build.”

DevOps:

> “Waiting for Infrastructure Approval.”

Security:

> “Waiting for Architecture Diagram.”

Everyone’s utilization:

**90%**

Yet the project is still delayed.

Alex finally understands:

**100% Utilization ≠ High Productivity**

Because Software Delivery is a **flow**.

## Alex Draws the Value Stream

**Idea**

↓

**Requirement**

↓

**Refinement**

↓

**Design**

↓

**Development**

↓

**Code Review**

↓

**QA**

↓

**UAT**

↓

**Deployment**

↓

**Production**

Then he records for every stage:

**Working Time**

vs.

**Waiting Time**

This allows him to identify the real bottleneck.

---

# Chapter 13: Technical Debt Never Gets Prioritized

## Case

Developer:

> “We really need to refactor this module.”

Business:

> “The customer can’t see it. Why should we spend time on it?”

So every new Feature takes longer.

Previously:

**3 days**

Later:

**5 days**

Then:

**8 days**

More and more bugs appear.

Eventually, one simple change takes:

**Three weeks.**

Management asks:

> “Why is Development getting slower?”

## Alex Starts Translating Technical Debt into Business Language

Instead of saying:

> “The architecture is ugly.”

He says:

> “This module has caused 17 Production Incidents over the past six months.”

> “Average Feature Development time has increased from 3 days to 8 days.”

> “We estimate that this wastes approximately 40 mandays every quarter.”

Technical Debt is no longer:

**Developer Preference**

It becomes:

**Business Cost.**

---

# Chapter 14: Should a Manager Still Write Code?

## Case

Production has a complicated bug.

Alex looks at it for ten minutes.

> “I know how to fix this.”

He is about to open Visual Studio.

Then he notices:

- 3 Developers are waiting for an Architecture Decision
- PM is waiting for a Timeline
- PO is waiting for a Scope Decision
- Management is waiting for a Status Update
- Junior Developer is waiting for a Code Review

If Alex spends four hours fixing the bug:

He solves **one bug**.

If Alex spends four hours removing blockers:

He may enable **ten people to continue working.**

## The Manager’s New Leverage

A Developer’s Output:

**Their Own Work**

A Manager’s Output:

**The Entire Team’s Output**

A manager still needs strong Technical Knowledge.

But that knowledge is mainly used to:

- Challenge Designs
- Review Architecture
- Identify Risks
- Guide Developers
- Troubleshoot Critical Issues
- Make Technical Decisions

Not to take developers’ tickets and write them personally every day.

---

# Chapter 15: The Boss Asks, “Is the Development Team Actually Performing Well?”

## Case

Boss:

> “How did Development perform this quarter?”

Alex used to answer:

> “Everyone was very busy.”

Boss:

> “...So?”

Alex decides to build an **Engineering Dashboard**.

## Delivery

### Commitment Reliability

Planned: 40

Delivered: 35

= **87.5%**

## Quality

- Production Defects
- Escaped Defects
- Change Failure Rate

## Speed

- Lead Time
- Cycle Time
- Deployment Frequency

## Stability

- Incident Count
- MTTR
- Availability

## Team

- Turnover
- Skill Coverage
- Bus Factor
- Capacity

Now Alex can tell Management:

- **Delivery: 87.5%**
- **Production Defects: ↓22%**
- **Cycle Time: 8.2 → 6.1 Days**
- **MTTR: 90 → 42 Minutes**

Now that is:

**Engineering Management.**

---

# Chapter 16: Alex Finally Understands What a Software Development Manager Actually Does Every Day

One year later.

A new Developer asks:

> “Alex, you hardly write code anymore. What exactly do you do all day?”

Alex opens his calendar.

### 9:00 AM — Engineering Standup

Check:

- Blockers
- Production
- Delivery Risks

### 10:00 AM — Product Refinement

Check:

- Requirements
- Acceptance Criteria
- Dependencies
- Technical Risks

### 11:00 AM — Architecture Review

Discuss:

- Scalability
- Security
- Integration
- Database
- Maintainability

### 2:00 PM — Project Review

Check:

- Scope
- Timeline
- Risks
- Dependencies

### 3:00 PM — 1-on-1

Discuss:

- Performance
- Career
- Workload
- Problems

### 4:00 PM — Management Update

Report:

- Delivery
- Risks
- Quality
- Capacity

### 5:00 PM — Engineering Improvement

Work on:

- CI/CD
- Technical Debt
- Processes
- Monitoring
- Automation

Alex finally says:

> “Developers are responsible for turning requirements into software.”

> “A Software Development Manager is responsible for building an environment where the team can continuously, reliably, and predictably turn requirements into software.”

---

# Final Chapter: The Software Development Manager Operating System

Only now do we organize the previous 16 stories into one complete operating model.

## ① Intake

**Business Request**

↓

**Clarify Problem**

↓

**Business Value**

↓

**Priority**

## ② Discovery

**Business Flow**

↓

**Requirements**

↓

**Technical Feasibility**

↓

**Dependencies**

↓

**Risks**

↓

**ROM Estimate**

## ③ Planning

**Feature Breakdown**

↓

**Estimate**

↓

**Capacity Planning**

↓

**Timeline**

↓

**Commitment**

## ④ Refinement

**User Story**

↓

**Acceptance Criteria**

↓

**Business Rules**

↓

**Exception Cases**

↓

**Dependencies**

↓

**Definition of Ready**

## ⑤ Technical Design

**Architecture**

↓

**API**

↓

**Database**

↓

**Integration**

↓

**Security**

↓

**Scalability**

↓

**Failure Handling**

## ⑥ Development

**Coding**

↓

**Unit Tests**

↓

**Code Review**

↓

**Static Analysis**

↓

**Build**

## ⑦ Quality

**Integration Testing**

↓

**Regression Testing**

↓

**Performance Testing**

↓

**Security Testing**

↓

**UAT**

## ⑧ Release

**Artifact**

↓

**Environment Configuration**

↓

**Database Migration**

↓

**Deployment**

↓

**Smoke Test**

↓

**Monitoring**

↓

**Rollback**

## ⑨ Operations

**Monitor**

↓

**Incident**

↓

**Mitigation**

↓

**Recovery**

↓

**RCA**

↓

**Corrective Action**

## ⑩ Engineering Improvement

**Metrics**

↓

**Bottlenecks**

↓

**Technical Debt**

↓

**Automation**

↓

**Process Improvement**

## ⑪ People Management

**1-on-1**

↓

**Performance**

↓

**Skill Gaps**

↓

**Coaching**

↓

**Career Path**

↓

**Succession**

## ⑫ Management

**Business**

↕

**Product**

↕

**Software Development Manager**

↕

**Tech Lead / Engineering Team**

↕

**QA / DevOps / Support**

A Software Development Manager is not really managing:

> **“Whether developers are working.”**

They are managing five things:

- **People**
- **Delivery**
- **Technology**
- **Quality**
- **Risk**

And the ultimate goal is not:

> **“Make developers busier.”**

It is:

> **Build an engineering organization that can continuously, reliably, predictably, and with high quality deliver software.**
