# Lesson 03: Quality Attributes (Non-Functional Requirements)

## 🎯 Learning Objectives

By the end of this lesson, you will:

- Understand what quality attributes (NFRs) are and why they matter
- Identify and prioritize key quality attributes for different systems
- Learn how to measure and specify quality attributes
- Understand trade-offs between competing quality attributes
- Apply quality attributes to real-world architectural decisions

---

## 📚 Part 1: What are Quality Attributes?

### Functional vs Non-Functional Requirements

**Functional Requirements** (What the system DOES):

- User can create an account
- System processes payments
- App sends notifications
- Database stores transactions

**Non-Functional Requirements / Quality Attributes** (How WELL the system does it):

- System responds in < 200ms (Performance)
- Handles 10,000 concurrent users (Scalability)
- Available 99.9% of the time (Reliability)
- Data is encrypted (Security)
- Code is easy to modify (Maintainability)

### Why Quality Attributes Matter

**Example: E-commerce Checkout**

**Functional**: "User can complete purchase"

**Quality Attributes determine success:**

- ⚡ **Performance**: Checkout completes in 2 seconds → ✅ High conversion
- 🐌 **Performance**: Checkout takes 10 seconds → ❌ Abandoned carts
- 🔒 **Security**: Payment data encrypted → ✅ Customer trust
- 🔓 **Security**: Data breach → ❌ Company bankruptcy

**Quality attributes often determine if a system succeeds or fails!**

---

## 📚 Part 2: Core Quality Attributes

### 1. Performance ⚡

**Definition**: How fast the system responds to requests

**Measures:**

- **Latency**: Time to respond to a request (ms)
- **Throughput**: Requests handled per second (req/s)
- **Response time**: Total time from request to complete response

**Examples:**

- Web search: < 100ms
- Page load: < 2 seconds
- Real-time gaming: < 50ms
- Batch processing: Hours is acceptable

**Trade-offs:**

- ✅ Fast performance
- ❌ Higher cost (more servers, optimization time)
- ❌ More complexity (caching, CDNs)

**When it's critical:**

- Real-time applications (gaming, trading)
- User-facing web apps
- APIs with high traffic

---

### 2. Scalability 📈

**Definition**: System's ability to handle growth

**Types:**

**Vertical Scaling (Scale Up)**

- Add more power to existing server
- More CPU, RAM, SSD
- **Limit**: Single machine ceiling
- **Cost**: Exponentially expensive

**Horizontal Scaling (Scale Out)**

- Add more servers
- Distribute load across machines
- **Limit**: Complexity of coordination
- **Cost**: Linear growth

**Measures:**

- Users supported: 100 → 1,000 → 1,000,000
- Requests per second: 10 → 100 → 10,000
- Data volume: GB → TB → PB

**Examples:**

- Instagram: 3 users → 1 billion users
- Netflix: 1 region → global
- Database: 1 server → 100 sharded servers

**Trade-offs:**

- ✅ Handles growth
- ❌ More complex architecture
- ❌ Higher operational cost
- ❌ Harder to debug

**When it's critical:**

- Growing startups
- Viral applications
- Enterprise systems
- SaaS products

---

### 3. Availability 🟢

**Definition**: Percentage of time system is operational

**Measures (The "Nines"):**

- **99%** (Two nines): 3.65 days downtime/year
- **99.9%** (Three nines): 8.76 hours downtime/year
- **99.99%** (Four nines): 52.56 minutes downtime/year
- **99.999%** (Five nines): 5.26 minutes downtime/year

**Techniques:**

- Redundancy (multiple servers)
- Load balancers
- Failover mechanisms
- Health checks
- Multi-region deployment

**Examples:**

- Banking: 99.99%+ required
- Social media: 99.9% acceptable
- Internal tools: 99% often sufficient

**Trade-offs:**

- ✅ Always accessible
- ❌ High cost (redundancy)
- ❌ Complex infrastructure
- ❌ May sacrifice consistency

**When it's critical:**

- Financial systems
- Healthcare
- Emergency services
- E-commerce

---

### 4. Reliability 🛡️

**Definition**: System works correctly under stated conditions

**Aspects:**

- **Fault tolerance**: Continues working despite failures
- **Error handling**: Graceful degradation
- **Data integrity**: No corruption or loss
- **Predictability**: Consistent behavior

**Measures:**

- Mean Time Between Failures (MTBF)
- Mean Time To Recovery (MTTR)
- Error rate per 1000 requests

**Examples:**

- Aircraft systems: Extremely high
- Banking transactions: Very high
- Social media posts: Moderate
- Analytics: Lower (eventual consistency ok)

**Techniques:**

- Circuit breakers
- Retry mechanisms
- Backups and replication
- Transaction management (ACID)

**Trade-offs:**

- ✅ System works correctly
- ❌ Slower (more checks/validations)
- ❌ More complex code
- ❌ Higher development cost

**When it's critical:**

- Financial transactions
- Medical records
- Critical infrastructure
- Data storage

---

### 5. Security 🔒

**Definition**: Protecting system from unauthorized access and attacks

**Aspects:**

- **Authentication**: Verifying identity
- **Authorization**: Controlling access
- **Encryption**: Protecting data in transit and at rest
- **Audit**: Tracking access and changes

**Measures:**

- Time to detect breach
- Number of vulnerabilities
- Compliance certifications (SOC2, ISO27001)

**Techniques:**

- HTTPS/TLS
- OAuth/JWT
- Input validation
- Rate limiting
- Security audits

**Examples:**

- Banking: Maximum security
- Healthcare: HIPAA compliance
- E-commerce: PCI DSS for payments
- Public blog: Basic security

**Trade-offs:**

- ✅ Data protected
- ❌ Slower (encryption overhead)
- ❌ Less convenient (2FA, password rules)
- ❌ Higher development cost

**When it's critical:**

- Financial services
- Healthcare
- Any system with personal data
- Government systems

---

### 6. Maintainability 🔧

**Definition**: Ease of modifying and updating the system

**Aspects:**

- **Modularity**: Clear separation of concerns
- **Readability**: Code is understandable
- **Testability**: Easy to write tests
- **Documentation**: Clear explanations

**Measures:**

- Time to fix bugs
- Time to add features
- Onboarding time for new developers
- Test coverage percentage

**Techniques:**

- Clean code practices
- Design patterns
- Automated testing
- CI/CD pipelines
- Good documentation

**Examples:**

- Startups: Very important (rapid changes)
- Legacy systems: Often poor (technical debt)
- Open source: Critical (community contributions)

**Trade-offs:**

- ✅ Easy to change
- ❌ More upfront design time
- ❌ Abstraction can reduce performance
- ❌ May be over-engineered initially

**When it's critical:**

- Long-lived systems
- Systems with frequent changes
- Multiple developers
- Open source projects

---

### 7. Usability 👤

**Definition**: How easy it is for users to accomplish tasks

**Aspects:**

- **Intuitiveness**: Self-explanatory interface
- **Efficiency**: Quick task completion
- **Error prevention**: Reduce user mistakes
- **Accessibility**: Usable by people with disabilities

**Measures:**

- Time to complete task
- Error rate
- User satisfaction scores
- Accessibility compliance (WCAG)

**Examples:**

- Consumer apps: Critical (iPhone, Gmail)
- Developer tools: Important (VS Code)
- Internal enterprise: Often neglected
- Command-line tools: Different paradigm

**Trade-offs:**

- ✅ Better user experience
- ❌ More design/testing time
- ❌ May sacrifice features for simplicity
- ❌ Accessibility adds development cost

**When it's critical:**

- Consumer-facing applications
- Apps with non-technical users
- Competitive markets
- Public services

---

### 8. Consistency 🎯

**Definition**: All users see the same data at the same time

**Levels:**

**Strong Consistency:**

- All reads see latest write immediately
- Example: Bank balance (must be accurate!)

**Eventual Consistency:**

- Reads may be stale temporarily
- Eventually all nodes converge
- Example: Social media likes (364 or 365 likes? Who cares!)

**Measures:**

- Staleness window (seconds of delay)
- Conflict rate

**Trade-offs:**

- ✅ Strong: Data always correct
- ❌ Strong: Slower, less available
- ✅ Eventual: Fast, always available
- ❌ Eventual: May show stale data

**When strong consistency is critical:**

- Financial transactions
- Inventory management
- Booking systems (hotel rooms, seats)

**When eventual consistency is acceptable:**

- Social media feeds
- Analytics dashboards
- Comment counts
- View counts

---

## 📚 Part 3: Prioritizing Quality Attributes

### You Can't Optimize for Everything!

**The Reality:**

- Finite budget
- Limited time
- Technical constraints
- **Must choose priorities**

### Quality Attribute Prioritization Framework

**Step 1: Identify Stakeholder Needs**

**Questions to ask:**

- What does success look like?
- What would cause failure?
- What do users care about most?
- What are regulatory requirements?

**Step 2: Rank Attributes**

Use categories:

- 🔴 **Critical**: System fails without this
- 🟡 **Important**: Significantly impacts success
- 🟢 **Nice to have**: Improves experience but not essential

**Step 3: Accept Trade-offs**

Can't be excellent at everything!

---

### Example: Different Systems, Different Priorities

#### Banking App 🏦

**Priorities:**

1. 🔴 **Security**: Must protect money
2. 🔴 **Reliability**: Transactions must be correct
3. 🔴 **Consistency**: Balance must be accurate
4. 🟡 **Availability**: 99.99% uptime
5. 🟡 **Performance**: < 2 seconds acceptable
6. 🟢 **Scalability**: Predictable growth

**Trade-offs accepted:**

- Slower performance for security checks ✅
- Complex architecture for reliability ✅
- Higher costs for consistency ✅

---

#### Social Media App 📱

**Priorities:**

1. 🔴 **Performance**: Must be fast (< 200ms)
2. 🔴 **Scalability**: Handle viral growth
3. 🔴 **Availability**: Always accessible
4. 🟡 **Usability**: Great UX
5. 🟡 **Security**: Protect user data
6. 🟢 **Consistency**: Eventual consistency ok

**Trade-offs accepted:**

- Eventual consistency (like counts may be stale) ✅
- Complex scaling infrastructure ✅
- Lower consistency for higher availability ✅

---

#### Internal Business Tool 💼

**Priorities:**

1. 🔴 **Maintainability**: Easy to change
2. 🔴 **Reliability**: Must work correctly
3. 🟡 **Usability**: Efficient for employees
4. 🟡 **Security**: Protect company data
5. 🟢 **Performance**: < 5 seconds ok
6. 🟢 **Scalability**: Fixed user base

**Trade-offs accepted:**

- Simpler architecture over performance ✅
- Monolith over microservices ✅
- Lower availability (99% ok) ✅

---

#### Real-Time Trading Platform 📊

**Priorities:**

1. 🔴 **Performance**: < 10ms latency
2. 🔴 **Reliability**: No errors
3. 🔴 **Consistency**: Strong consistency
4. 🔴 **Security**: Regulatory compliance
5. 🟡 **Availability**: Very high
6. 🟡 **Scalability**: Handle market spikes

**Trade-offs accepted:**

- Extremely high costs ✅
- Complex infrastructure ✅
- Specialized hardware ✅

---

## 📚 Part 4: Measuring Quality Attributes

### How to Specify Quality Attributes

**❌ Bad (Vague):**

- "System should be fast"
- "App must be secure"
- "System should scale"

**✅ Good (Measurable):**

- "95th percentile response time < 200ms"
- "99.9% availability (< 9 hours downtime/year)"
- "Support 10,000 concurrent users"
- "Encrypt all data at rest and in transit"

---

### Example Specifications

#### E-Commerce Website

```
Quality Attribute Specifications:

PERFORMANCE:
- Page load time: < 2 seconds (95th percentile)
- API response: < 200ms (99th percentile)
- Search results: < 500ms

SCALABILITY:
- Support 100,000 concurrent users
- Handle 1,000 orders per minute during peak
- Support 10M products in catalog

AVAILABILITY:
- 99.9% uptime (< 9 hours downtime/year)
- Planned maintenance < 2 hours/month
- Zero downtime deployments

SECURITY:
- PCI DSS compliant for payments
- HTTPS only (TLS 1.3)
- Rate limiting: 100 requests/min per user
- Data at rest: AES-256 encryption

RELIABILITY:
- Zero data loss for transactions
- Automated backups every hour
- < 1 error per 1000 transactions

MAINTAINABILITY:
- 80%+ test coverage
- Deploy new features weekly
- Onboard new developer in < 1 week
```

---

## 📚 Part 5: Quality Attributes in Practice

### Scenario 1: Startup MVP

**Context:**

- 2 developers
- 3 months to launch
- Budget: $10,000
- Expected: 100-1000 users

**Priority Matrix:**

| Attribute           | Priority        | Specification     | Rationale            |
| ------------------- | --------------- | ----------------- | -------------------- |
| **Maintainability** | 🔴 Critical     | Clean code, tests | Will change rapidly  |
| **Reliability**     | 🔴 Critical     | 99% uptime        | Must work correctly  |
| **Security**        | 🟡 Important    | HTTPS, basic auth | Protect user data    |
| **Performance**     | 🟡 Important    | < 2 seconds       | Good enough          |
| **Scalability**     | 🟢 Nice to have | 1000 users        | Optimize when needed |
| **Availability**    | 🟢 Nice to have | 99% ok            | Not 24/7 critical    |

**Architectural Decisions:**

- ✅ Monolith (maintainability)
- ✅ Simple deployment (Heroku)
- ✅ PostgreSQL (reliability)
- ✅ Auth0 (security without complexity)
- ❌ No complex scaling infrastructure yet

---

### Scenario 2: Healthcare System

**Context:**

- Critical patient data
- HIPAA compliance required
- Multiple hospitals
- 50,000 users

**Priority Matrix:**

| Attribute           | Priority     | Specification      | Rationale               |
| ------------------- | ------------ | ------------------ | ----------------------- |
| **Security**        | 🔴 Critical  | HIPAA compliant    | Legal requirement       |
| **Reliability**     | 🔴 Critical  | 99.99% uptime      | Lives depend on it      |
| **Consistency**     | 🔴 Critical  | Strong consistency | Data must be accurate   |
| **Availability**    | 🔴 Critical  | 24/7 operation     | Emergency access        |
| **Maintainability** | 🟡 Important | Well documented    | Long-lived system       |
| **Performance**     | 🟡 Important | < 1 second         | Fast enough for doctors |

**Architectural Decisions:**

- ✅ Multi-region deployment (availability)
- ✅ ACID database (consistency + reliability)
- ✅ Encryption everywhere (security)
- ✅ Audit logging (compliance)
- ✅ High cost accepted (lives > money)

---

## 🎓 Knowledge Check

### Question 1: Quality Attribute Identification

**Scenario:** "Users complain that when they submit a form, they wait 10 seconds and sometimes it times out."

**Which quality attribute is the problem?**

a) Security
b) Performance
c) Maintainability
d) Scalability

<details>
<summary>Click to reveal answer</summary>

**Answer: b) Performance**

**Why?**

- **Symptom**: Long wait time (10 seconds)
- **Quality attribute**: Response time
- **Performance issue**: System is too slow

**Not the others:**

- Security: No mention of unauthorized access
- Maintainability: Not about code changes
- Scalability: Could be performance or scalability, but the symptom (slow response) indicates performance

**Solution approaches:**

- Optimize database queries
- Add caching
- Reduce API calls
- If ALL users experience this → performance
- If only during peak times → might be scalability too

</details>

---

### Question 2: Trade-offs

**Your team is building a personal todo app (single user, local storage).**

**Which quality attributes matter LEAST?**

a) Usability (easy to use)
b) Maintainability (easy to modify)
c) Scalability (handle millions of users)
d) Reliability (saves todos correctly)

<details>
<summary>Click to reveal answer</summary>

**Answer: c) Scalability**

**Why?**

- **Context**: Single user, local storage
- **Scalability is irrelevant**: Will never have millions of users!
- This is **over-engineering** territory

**What DOES matter:**

- ✅ Usability: Critical (personal productivity tool)
- ✅ Maintainability: Important (you'll add features)
- ✅ Reliability: Critical (can't lose todos)

**Key lesson:**
Don't optimize for problems you don't have!

**If the context changed (multi-user cloud todo app):**

- Then scalability would become important
- Context drives priorities!

</details>

---

### Question 3: Specification

**Which is the BEST specification for performance?**

a) "System should be really fast"
b) "System should respond quickly to user requests"
c) "API response time < 200ms for 95% of requests"
d) "System should have good performance"

<details>
<summary>Click to reveal answer</summary>

**Answer: c) "API response time < 200ms for 95% of requests"**

**Why?**

- ✅ **Measurable**: 200ms is a specific number
- ✅ **Testable**: Can measure and verify
- ✅ **Clear**: No ambiguity
- ✅ **Realistic**: 95th percentile allows for outliers

**The others are too vague:**

- "Really fast" - How fast? 1ms? 1 second?
- "Quickly" - Subjective
- "Good performance" - Meaningless without context

**Good specifications always include:**

- Specific metric (response time, uptime %)
- Specific threshold (200ms, 99.9%)
- Context (95th percentile, concurrent users)

</details>

---

## 💡 Key Takeaways

1. **Quality attributes determine system success** - Functional requirements say WHAT, quality attributes say HOW WELL

2. **You can't optimize everything** - Must prioritize based on context (banking ≠ social media)

3. **Context drives priorities** - Startup MVP ≠ Healthcare system ≠ Trading platform

4. **Make attributes measurable** - "< 200ms" beats "fast", "99.9%" beats "reliable"

5. **Quality attributes create trade-offs** - Fast vs cheap, consistent vs available, secure vs usable

6. **Don't optimize for problems you don't have** - Premature optimization wastes resources

7. **Different systems, different priorities** - No universal "correct" priority list

---

## 🚀 Practical Exercise

### Design Quality Attributes for YOUR System

**Pick a system to design:**

- Personal blog
- Team chat app (like Slack)
- Online learning platform
- Food ordering app

**Your Task:**

1. **Identify context:**

   - Who are the users?
   - How many users?
   - What's the budget?
   - What's critical for success?

2. **Prioritize quality attributes:**

   - List 6-8 quality attributes
   - Mark as Critical / Important / Nice-to-have
   - Explain WHY for each priority

3. **Create specifications:**

   - Write measurable specs for top 3 attributes
   - Example: "Performance: < 2s page load (95th percentile)"

4. **Identify trade-offs:**
   - What are you willing to sacrifice?
   - What constraints does this create?

---

**Would you like to work through this exercise together?**

Or are you ready to move on to the next lesson?

---

## 📖 Recommended Reading

**Books:**

- "Software Architecture in Practice" - Chapter on Quality Attributes
- "Designing Data-Intensive Applications" by Martin Kleppmann

**Articles:**

- ISO/IEC 25010 Quality Model
- "Quality Attributes" by SEI (Software Engineering Institute)

**Tools:**

- Performance testing: JMeter, k6
- Monitoring: Datadog, New Relic
- Security scanning: OWASP ZAP, Snyk

---

## ✅ Lesson Complete!

You've learned:

- ✅ What quality attributes (NFRs) are
- ✅ 8 core quality attributes and when each matters
- ✅ How to prioritize based on context
- ✅ How to create measurable specifications
- ✅ Trade-offs between competing attributes
- ✅ Real-world prioritization examples

**Next Lesson**: Lesson 04 - Architecture Documentation OR jump to Lesson 05 - Layered Architecture (patterns!)

---

**Completion Date**: _To be filled upon completion_
**Questions/Notes**: _Add your thoughts here_
