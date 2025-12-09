# Lesson 08: Hexagonal/Clean Architecture

## Overview

Hexagonal Architecture (also known as Ports and Adapters) and Clean Architecture are patterns that emphasize separation of concerns, testability, and independence from frameworks, databases, and external systems. They help you build systems that are easy to adapt, test, and maintain.

---

## Key Concepts

- **Core Domain Logic:** The heart of your application, independent of external technologies.
- **Ports:** Interfaces that define how the core interacts with the outside world (e.g., APIs, events, CLI).
- **Adapters:** Implementations of ports for specific technologies (e.g., REST controllers, database repositories).
- **Dependency Rule:** Dependencies always point inward, toward the core domain logic.
- **Boundaries:** Clear separation between business logic and infrastructure.

---

## Benefits

- **Testability:** Core logic can be tested without external dependencies.
- **Flexibility:** Swap out adapters (e.g., change database, UI, or API) without changing core logic.
- **Maintainability:** Clear boundaries make code easier to understand and evolve.
- **Framework Independence:** Business logic is not tied to any specific technology.

---

## Challenges

- **Initial Complexity:** More interfaces and abstractions to set up.
- **Learning Curve:** Requires discipline and understanding of boundaries.
- **Overhead:** May be overkill for simple apps or small teams.

---

## Practical Example: Bank Transfer

**Core Domain Logic:**

```python
class BankAccount:
    def __init__(self, id, balance):
        self.id = id
        self.balance = balance
    def transfer(self, target_account, amount):
        if self.balance < amount:
            raise Exception("Insufficient funds")
        self.balance -= amount
        target_account.balance += amount
```

**Port (Interface):**

```python
class AccountRepositoryPort:
    def get_account(self, account_id):
        pass
    def save_account(self, account):
        pass
```

**Adapter (Database):**

```python
class SqlAccountRepository(AccountRepositoryPort):
    def get_account(self, account_id):
        # fetch from SQL DB
        pass
    def save_account(self, account):
        # save to SQL DB
        pass
```

**Adapter (REST API):**

```python
class AccountController:
    def __init__(self, account_repo):
        self.account_repo = account_repo
    def transfer(self, from_id, to_id, amount):
        from_acct = self.account_repo.get_account(from_id)
        to_acct = self.account_repo.get_account(to_id)
        from_acct.transfer(to_acct, amount)
        self.account_repo.save_account(from_acct)
        self.account_repo.save_account(to_acct)
```

---

## Diagram

```
┌─────────────┐      ┌─────────────┐      ┌─────────────┐
│  REST API   │◀────▶│   PORT      │◀────▶│  DOMAIN     │
│ (Adapter)   │      │ (Interface) │      │  LOGIC      │
└─────────────┘      └─────────────┘      └─────────────┘
      ▲                    ▲                    ▲
      │                    │                    │
┌─────────────┐      ┌─────────────┐      ┌─────────────┐
│ Database    │◀────▶│   PORT      │◀────▶│  DOMAIN     │
│ (Adapter)   │      │ (Interface) │      │  LOGIC      │
└─────────────┘      └─────────────┘      └─────────────┘
```

---

## When to Use

- Complex business logic that must be independent of frameworks or infrastructure.
- Need for high testability and flexibility.
- Large teams or long-lived systems.

## When Not to Use

- Simple CRUD apps or prototypes.
- Small teams or short-lived projects.

---

## Further Reading

- Alistair Cockburn: Hexagonal Architecture
- Robert C. Martin: Clean Architecture
- "Ports and Adapters" pattern

---

_Next: Try refactoring a simple app to use ports and adapters, or sketch your own hexagonal architecture diagram!_
