# Lesson 04: Architecture Documentation

## 🎯 Learning Objectives

By the end of this lesson, you will:

- Understand why architecture documentation matters
- Learn the C4 model for visualizing architecture
- Create effective architecture diagrams
- Write Architecture Decision Records (ADRs)
- Know what to document and what to skip
- Apply documentation practices to real projects

---

## 📚 Part 1: Why Document Architecture?

### The Problem

**6 months later:**

- "Why did we choose MongoDB over PostgreSQL?"
- "What was the reasoning behind microservices?"
- "Why is authentication handled this way?"
- "What constraints led to this design?"

**Without documentation:** 🤷 Nobody remembers!

### The Value

**Good documentation provides:**

- 📖 **Onboarding**: New team members understand the system quickly
- 🧠 **Knowledge preservation**: Decisions and rationale are captured
- 🔄 **Decision review**: Can revisit choices when context changes
- 💬 **Communication**: Shared understanding across teams
- 🎯 **Alignment**: Everyone knows the direction

---

## 📚 Part 2: What to Document (and What NOT to)

### ✅ DO Document

**1. Architectural Decisions**

- What was chosen and why
- Alternatives considered
- Trade-offs accepted
- Example: "Why PostgreSQL over MongoDB"

**2. System Structure**

- Major components
- How they interact
- Data flow
- Example: Architecture diagrams

**3. Quality Attributes**

- Performance requirements
- Security constraints
- Scalability needs
- Example: Your priority specifications

**4. Constraints**

- Technology limitations
- Budget restrictions
- Team skills
- Example: "Must use existing AWS infrastructure"

**5. Key Patterns**

- Architectural patterns used
- Design patterns applied
- Example: "Using layered architecture"

---

### ❌ DON'T Document

**1. Implementation Details**

- Specific code syntax
- Variable names
- Algorithm details
- **Why**: Changes too frequently, belongs in code comments

**2. Obvious Information**

- "The database stores data"
- "Users can log in"
- **Why**: Wastes time, adds noise

**3. Outdated Information**

- Better to delete than keep stale docs
- **Why**: Misleading is worse than missing

**4. Everything**

- Over-documentation is as bad as under-documentation
- **Why**: Nobody reads 100-page docs

---

### The Golden Rule

> **"Document decisions and structure, not implementation."**

**Good balance:**

- Architecture diagrams: Yes ✅
- Key decisions: Yes ✅
- Code-level details: No ❌
- Every single class: No ❌

---

## 📚 Part 3: The C4 Model for Architecture Diagrams

### What is C4?

**C4 = Context, Containers, Components, Code**

A hierarchical way to visualize architecture at different levels of zoom.

Created by Simon Brown, it's like Google Maps for software:

- **Context**: World view (where is the system?)
- **Containers**: Country view (what are the major parts?)
- **Components**: City view (what's inside each part?)
- **Code**: Street view (classes and code - usually skip this)

---

### Level 1: Context Diagram

**Purpose**: Show the system in its environment

**Shows:**

- Your system (one box)
- Users/actors (people)
- External systems (APIs, databases, services)
- Relationships between them

**Example: Personal Finance App**

```
┌─────────────┐
│   Family    │ (Users)
│   Members   │
└──────┬──────┘
       │ Uses
       ↓
┌─────────────────────────┐
│  Personal Finance App   │ (Your System)
└───┬─────────────────┬───┘
    │                 │
    │ Sends           │ Integrates
    │ emails          │ with
    ↓                 ↓
┌─────────┐     ┌──────────────┐
│  Email  │     │ Bank API     │
│ Service │     │ (Optional)   │
└─────────┘     └──────────────┘
```

**Who it's for**: Everyone (executives, non-technical stakeholders)

**Keep it simple**: Big picture only!

---

### Level 2: Container Diagram

**Purpose**: Show the high-level technology choices

**Container** = Deployable/runnable unit (NOT Docker containers!)

- Web application
- Mobile app
- Database
- API server

**Example: Personal Finance App**

```
┌─────────────┐
│   Family    │
│   Members   │
└──────┬──────┘
       │ HTTPS
       ↓
┌──────────────────────┐
│   Web Application    │
│   (React/Vue)        │
└──────┬───────────────┘
       │ REST API
       │ (JSON/HTTPS)
       ↓
┌──────────────────────┐
│   API Server         │
│   (Node.js/Python)   │
└──────┬───────────────┘
       │ SQL
       ↓
┌──────────────────────┐
│   PostgreSQL         │
│   (Database)         │
└──────────────────────┘
```

**Who it's for**: Technical team, architects

**Shows**: Technology stack and deployment units

---

### Level 3: Component Diagram

**Purpose**: Show internal structure of a container

**Component** = Logical grouping of related functionality

- Authentication module
- Payment processor
- Report generator

**Example: API Server Components**

```
┌─────────────────────────────────────┐
│         API Server                  │
│                                     │
│  ┌──────────────┐  ┌─────────────┐ │
│  │     Auth     │  │   Users     │ │
│  │  Component   │  │  Component  │ │
│  └──────────────┘  └─────────────┘ │
│                                     │
│  ┌──────────────┐  ┌─────────────┐ │
│  │ Transaction  │  │   Reports   │ │
│  │  Component   │  │  Component  │ │
│  └──────────────┘  └─────────────┘ │
│                                     │
│  ┌──────────────┐                  │
│  │  Category    │                  │
│  │  Component   │                  │
│  └──────────────┘                  │
└─────────────────────────────────────┘
```

**Who it's for**: Developers working on the system

**Shows**: Internal organization and responsibilities

---

### Level 4: Code Diagram

**Purpose**: Show classes and code structure

**Usually skip this!**

- Too detailed
- Changes frequently
- Better in code itself
- IDEs can generate this

**When to use**: Very complex algorithms or critical components

---

## 📚 Part 4: Creating Effective Diagrams

### Best Practices

#### 1. **Use Simple Shapes**

- Boxes for components/systems
- Lines for relationships
- Labels for clarity
- Don't make it artistic!

#### 2. **Include a Legend**

```
Legend:
□ = System/Component
○ = Person/User
→ = Data flow
-- = Uses/Depends on
```

#### 3. **Show Technology Choices**

```
Instead of: "Database"
Write: "PostgreSQL Database"

Instead of: "API"
Write: "REST API (JSON/HTTPS)"
```

#### 4. **Keep it Current**

- Update when architecture changes
- Delete outdated diagrams
- Date your diagrams

#### 5. **One Diagram = One Purpose**

- Don't cram everything into one diagram
- Create multiple focused diagrams
- Each diagram tells a story

---

### Common Mistakes

❌ **Too much detail**

- Showing every class
- Including implementation details
- Result: Unreadable mess

❌ **Too vague**

- Just boxes with no labels
- No technology information
- Result: Not useful

❌ **Outdated**

- Diagram shows old architecture
- Result: Misleading (worse than nothing!)

❌ **No context**

- Diagram without explanation
- No legend
- Result: Confusing

---

## 📚 Part 5: Architecture Decision Records (ADRs)

### What is an ADR?

**A lightweight document capturing ONE architectural decision.**

**Format:**

```markdown
# ADR-[NUMBER]: [Short Title]

**Status**: Proposed | Accepted | Deprecated | Superseded
**Date**: YYYY-MM-DD
**Deciders**: [Who made the decision]

## Context

[What's the situation? What problem are we solving?]

## Decision

[What did we decide?]

## Consequences

[What are the results? Good and bad.]
```

---

### Real Example: Your Finance App

```markdown
# ADR-001: Use PostgreSQL for Data Storage

**Status**: Accepted
**Date**: 2025-11-27
**Deciders**: Kayla (Developer/Architect)

## Context

Personal finance app for family use (max 10 users). Need to
store transactions, categories, and account balances.

Key requirements:

- Data consistency critical (financial data)
- Strong reliability (no transaction loss)
- Accurate balances (no duplicates)
- Simple maintenance (solo developer)

Considered alternatives: MongoDB, SQLite

## Decision

Use PostgreSQL as the primary database.

## Consequences

### Positive

- ACID guarantees ensure data consistency
- Strong reliability for transactions
- Familiar to team (easier maintenance)
- Powerful querying for reports
- Can easily handle 10 users
- Low hosting cost ($10-20/month)

### Negative

- Schema migrations required for changes
  (Mitigation: Use migration tools like Alembic/Flyway)
- Vertical scaling limits at very large scale
  (Acceptable: Not planning for millions of users)
- Need separate database server
  (Acceptable: Part of standard deployment)

## Alternatives Considered

### MongoDB

- Pros: Flexible schema, horizontal scaling
- Cons: Weaker consistency, team learning curve
- Rejected: Consistency more important than flexibility

### SQLite

- Pros: Zero configuration, embedded
- Cons: Single-user only, no remote access
- Rejected: Need multi-user support for family
```

---

### Why ADRs Work

**Benefits:**

1. ✅ **Captures rationale**: "Why PostgreSQL?" → Answered forever
2. ✅ **Quick to write**: 10-15 minutes per decision
3. ✅ **Easy to review**: New team members can read history
4. ✅ **Living documentation**: Update status as context changes
5. ✅ **Lightweight**: Not a huge formal document

**When to write an ADR:**

- Choosing database technology
- Selecting architecture pattern (monolith vs microservices)
- Major technology choices (framework, language)
- Security approach
- Deployment strategy

**When NOT to write an ADR:**

- Naming a variable
- Choosing a UI library (too low-level)
- Temporary decisions
- Obvious choices

---

## 📚 Part 6: Documentation Tools

### For Diagrams

**Simple (Recommended for starting):**

- **Draw.io / Diagrams.net**: Free, web-based
- **Excalidraw**: Simple sketching
- **Google Slides/PowerPoint**: Everyone has it
- **Mermaid**: Text-based diagrams in markdown

**Advanced:**

- **Structurizr**: C4 model specific
- **PlantUML**: Code-based diagrams
- **Lucidchart**: Professional diagramming

### For ADRs

**Simple (Recommended):**

- **Markdown files in Git**: `/docs/adr/`
- Easy to version control
- Review in pull requests
- Free

**Tools:**

- **adr-tools**: CLI for managing ADRs
- **Log4brains**: Web UI for ADRs
- **GitHub/GitLab Wiki**: Built-in documentation

---

## 📚 Part 7: Documentation in Practice

### Recommended Documentation Set

**For a small project (like your finance app):**

1. **README.md**

   - What the system does
   - How to run it locally
   - Basic architecture overview

2. **Architecture Diagram** (C4 Level 2)

   - Container diagram showing tech stack
   - Keep it simple!

3. **3-5 ADRs**

   - Database choice
   - Authentication approach
   - Deployment strategy
   - Major technology decisions

4. **Quality Attributes**
   - Security requirements
   - Performance specifications
   - Your priority list from Lesson 03!

**Total time**: 2-4 hours
**Value**: Immense (especially 6 months later)

---

### Documentation Workflow

**When making a decision:**

1. Discuss options (mental or with team)
2. Make decision
3. Write ADR (15 minutes)
4. Update diagram if structure changed (15 minutes)
5. Commit to Git with code

**Regular maintenance:**

- Review ADRs quarterly
- Update diagrams when architecture changes
- Delete outdated docs
- Keep it current or delete it!

---

## 🎓 Knowledge Check

### Question 1: C4 Model Levels

**Which C4 level would you use to show "User → Web App → API → Database"?**

a) Context Diagram (Level 1)
b) Container Diagram (Level 2)
c) Component Diagram (Level 3)
d) Code Diagram (Level 4)

<details>
<summary>Click to reveal answer</summary>

**Answer: b) Container Diagram (Level 2)**

**Why?**

- Shows deployable units (Web App, API, Database)
- Shows technology choices
- Shows how they connect

**Not the others:**

- Context: Too high-level (just "Your System")
- Component: Too detailed (internal structure)
- Code: Way too detailed (classes)

</details>

---

### Question 2: ADR Usage

**Which decision should you write an ADR for?**

a) Naming a CSS class "button-primary"
b) Choosing between PostgreSQL and MongoDB
c) Deciding to use a for-loop instead of while-loop
d) Picking a blue color for the header

<details>
<summary>Click to reveal answer</summary>

**Answer: b) Choosing between PostgreSQL and MongoDB**

**Why?**

- ✅ Architectural decision (affects whole system)
- ✅ Hard to change later
- ✅ Has significant trade-offs
- ✅ Future team will want to know why

**Not the others:**

- CSS class name: Too low-level, changes easily
- Loop type: Implementation detail
- Color choice: UI design, not architecture

**Rule of thumb**: If it's hard to change and affects the system broadly → Write an ADR

</details>

---

### Question 3: Documentation Balance

**Your teammate wants to document every function, every class, and every variable in a 500-page architecture document. What's wrong with this?**

a) Nothing, more documentation is always better
b) Over-documentation is as bad as under-documentation
c) Should only document functions, not variables
d) 500 pages is too short

<details>
<summary>Click to reveal answer</summary>

**Answer: b) Over-documentation is as bad as under-documentation**

**Why?**

**Problems with over-documentation:**

- ❌ Nobody reads it (too long)
- ❌ Gets outdated quickly (too much to maintain)
- ❌ Hides important information in noise
- ❌ Wastes time creating it

**Better approach:**

- ✅ Document decisions and structure
- ✅ Let code document implementation
- ✅ Keep it concise and current
- ✅ 10 useful pages > 500 unused pages

**Golden rule**: "Document enough to understand the system, not every detail."

</details>

---

## 💡 Key Takeaways

1. **Documentation preserves knowledge** - Captures "why" decisions were made

2. **C4 model provides structure** - Context → Containers → Components (skip Code)

3. **ADRs are lightweight and powerful** - 15 minutes to capture a decision forever

4. **Balance is key** - Too much = nobody reads; too little = nobody understands

5. **Keep it current** - Outdated docs are worse than no docs

6. **Document decisions, not implementation** - Architecture not code details

7. **Use simple tools** - Markdown + diagrams in Git works great

---

## 🚀 Practical Exercise

### Document Your Finance App

Create documentation for your personal finance app:

**Task 1: Create a Container Diagram (C4 Level 2)**

Show:

- Users (family members)
- Web frontend
- API backend
- Database
- Any external services

**Task 2: Write 2 ADRs**

Choose from:

- ADR-001: Database choice (PostgreSQL)
- ADR-002: Authentication approach
- ADR-003: Monolith vs microservices
- ADR-004: Deployment strategy

**Task 3: Document Quality Attributes**

Take your priorities from Lesson 03 and create a simple markdown doc:

```markdown
# Quality Attributes

## Critical

- Security: [Your specs]
- Reliability: [Your specs]
- Consistency: [Your specs]

## Important

- Usability: [Your specs]
- Maintainability: [Your specs]

## Acceptable Trade-offs

- Performance: [What you're willing to accept]
- Scalability: [Why it's not a priority]
```

---

**Would you like to work through this exercise, or shall we move on to Lesson 05 (Architectural Patterns)?**

---

## 📖 Recommended Reading

**Articles:**

- "The C4 Model" by Simon Brown (c4model.com)
- "Documenting Software Architectures" by SEI
- "ADR GitHub Organization" (adr.github.io)

**Books:**

- "Software Architecture for Developers" by Simon Brown
- "Documenting Software Architectures" by Clements et al.

**Tools:**

- Draw.io: https://draw.io
- Mermaid: https://mermaid.js.org
- ADR Tools: https://github.com/npryce/adr-tools

---

## ✅ Lesson Complete!

You've learned:

- ✅ Why architecture documentation matters
- ✅ What to document (and what not to)
- ✅ The C4 model for visualizing architecture
- ✅ How to write effective ADRs
- ✅ Tools and best practices
- ✅ Documentation workflow

**Next Lesson**: Lesson 05 - Layered Architecture (First architectural pattern!)

---

**Completion Date**: _To be filled upon completion_
**Questions/Notes**: _Add your thoughts here_
