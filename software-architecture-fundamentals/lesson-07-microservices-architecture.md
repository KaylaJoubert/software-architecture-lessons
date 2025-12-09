# Lesson 07: Microservices Architecture

## Overview

Microservices architecture is an approach to building software systems as a suite of small, independently deployable services, each running in its own process and communicating via lightweight mechanisms (often HTTP APIs or messaging).

---

## What is Microservices Architecture?

- Each microservice is focused on a single business capability (e.g., user management, payments, catalog).
- Services are loosely coupled, independently deployable, and can be developed by small, autonomous teams.
- Each service owns its own data and state, and communicates with others via APIs or events.

---

## Microservices vs. Component-Based Architecture

| Aspect               | Component-Based Architecture       | Microservices Architecture            |
| -------------------- | ---------------------------------- | ------------------------------------- |
| Deployment           | Components often deployed together | Each service deployed independently   |
| Process Isolation    | Usually in-process                 | Each service runs in its own process  |
| Communication        | In-process calls                   | Network calls (HTTP, gRPC, messaging) |
| Data Ownership       | Often shared database              | Each service owns its own database    |
| Team Autonomy        | Moderate                           | High                                  |
| Scaling              | Scale whole app or component       | Scale services independently          |
| Technology Diversity | Usually one stack                  | Polyglot possible (different stacks)  |

---

## Key Benefits

- **Independent Deployment:** Teams can release features and fixes without coordinating with others.
- **Scalability:** Scale only the services that need it.
- **Resilience:** Failure in one service doesn't bring down the whole system.
- **Technology Diversity:** Teams can use the best tool for each job.
- **Faster Innovation:** Small, focused teams can move quickly.

---

## Key Challenges

- **Operational Complexity:** More services = more deployments, monitoring, and debugging.
- **Distributed Data Management:** Data consistency and transactions are harder.
- **Network Latency & Failures:** Calls between services can fail or be slow.
- **Testing:** End-to-end testing is more complex.
- **DevOps Maturity Required:** Automation, CI/CD, and monitoring are essential.

---

## Real-World Examples

- Netflix, Amazon, Uber, Spotify, and many large-scale SaaS platforms.
- E-commerce: separate services for catalog, cart, checkout, payments, recommendations.

---

## When to Use Microservices

- Large, complex systems with many business domains.
- Multiple teams working in parallel.
- Need for independent scaling or technology diversity.
- Organization has DevOps maturity.

## When Not to Use

- Small teams or simple applications.
- When operational overhead outweighs benefits.
- If you lack automation, monitoring, or deployment maturity.

---

## Hands-On Example: E-Commerce Checkout

**Services:**

- Cart Service
- Order Service
- Payment Service
- Inventory Service

**Interaction Diagram:**

```
User → Cart Service → Order Service → Payment Service
                        ↓
                  Inventory Service
```

- Each service has its own codebase, database, and deployment pipeline.
- Services communicate via REST APIs or events (e.g., orderPlaced, paymentConfirmed).

---

## Microservices Anti-Patterns

- **Distributed Monolith:** Services are tightly coupled and must be deployed together.
- **Too Many Services Too Soon:** Prematurely splitting a simple app into many services.
- **Shared Database:** Multiple services writing to the same database schema.
- **Lack of Automation:** Manual deployments and no monitoring.

---

## Summary Table: Component vs. Microservices

| Criteria        | Component-Based        | Microservices          |
| --------------- | ---------------------- | ---------------------- |
| Deployment Unit | Library/module         | Service/process        |
| Communication   | In-process             | Network/API            |
| Data Ownership  | Shared                 | Isolated               |
| Team Structure  | Feature or layer teams | Cross-functional teams |

---

## Further Reading

- Martin Fowler: Microservices
- Sam Newman: Building Microservices
- ThoughtWorks Technology Radar

---

_Next: Compare with your previous architecture, or try designing a microservice for a familiar domain!_
