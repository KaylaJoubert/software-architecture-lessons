---
# Lesson 05: Layered Architecture

## 🎯 Overview

Layered Architecture is one of the most widely used architectural patterns in software development. It organizes code into logical layers, each with a distinct responsibility, making systems easier to understand, maintain, and evolve.

### What is Layered Architecture?

Layered architecture divides an application into horizontal layers, where each layer only interacts with the layer directly below or above it. This separation of concerns helps manage complexity and enables teams to work independently on different parts of the system.

**Typical Layers:**
1. **Presentation Layer (UI):** Handles user interaction and displays data
2. **Application Layer (Service):** Coordinates application activities, business logic
3. **Domain Layer (Business):** Core business rules and domain logic
4. **Persistence Layer (Data):** Manages data access, storage, and retrieval

**Example (Web App):**
```
┌─────────────────────────────┐
│   Presentation Layer (UI)   │
│   (React, Angular, Vue)     │
└─────────────┬───────────────┘
			  │
┌─────────────▼───────────────┐
│   Application Layer         │
│   (Controllers, Services)   │
└─────────────┬───────────────┘
			  │
┌─────────────▼───────────────┐
│   Domain Layer              │
│   (Business Logic, Models)  │
└─────────────┬───────────────┘
			  │
┌─────────────▼───────────────┐
│   Persistence Layer         │
│   (Database, ORM)           │
└─────────────────────────────┘
```

### Key Benefits
- **Separation of concerns:** Each layer has a clear responsibility
- **Maintainability:** Easier to update or replace parts of the system
- **Testability:** Layers can be tested independently
- **Scalability:** Layers can be scaled or distributed as needed

### Real-World Examples
- Most web apps (Django, Spring, ASP.NET)
- Enterprise systems (banking, insurance)
- Mobile apps (Android, iOS)

---

---

## 🔍 Layer Breakdown

### 1. Presentation Layer (UI)

**Role:**

- Handles all user interactions
- Displays data to users
- Sends user input to the application layer

**Examples:**

- Web: React, Angular, Vue
- Mobile: Swift (iOS), Kotlin (Android)
- Desktop: Electron, WPF

**Typical Responsibilities:**

- Render screens, forms, dashboards
- Validate user input (basic checks)
- Show error/success messages

---

### 2. Application Layer (Service)

**Role:**

- Coordinates application activities
- Implements business use cases
- Orchestrates calls to domain and persistence layers

**Examples:**

- Controllers in Django, Spring, Express
- Service classes in .NET, Java

**Typical Responsibilities:**

- Handle requests from UI
- Manage workflows (e.g., "transfer money")
- Enforce application-level rules

---

### 3. Domain Layer (Business)

**Role:**

- Contains core business logic and rules
- Models real-world entities (e.g., Account, Transaction)
- Independent of UI and data storage

**Examples:**

- Domain models in DDD (Domain-Driven Design)
- Business logic classes (e.g., Order, Invoice)

**Typical Responsibilities:**

- Validate business rules (e.g., "no overdraft allowed")
- Calculate values (e.g., interest, totals)
- Encapsulate domain knowledge

---

### 4. Persistence Layer (Data)

**Role:**

- Manages data access, storage, and retrieval
- Translates domain objects to database records
- Isolates data logic from business logic

**Examples:**

- Repositories in Spring, Django ORM, SQLAlchemy
- Data access objects (DAOs)

**Typical Responsibilities:**

- CRUD operations (Create, Read, Update, Delete)
- Query optimization
- Transaction management

---

## 🔗 How Layers Interact

**Flow Example (User creates a transaction):**

1. User enters transaction in UI (Presentation Layer)
2. UI sends request to Application Layer (e.g., REST API controller)
3. Application Layer calls Domain Layer to validate and process transaction
4. Domain Layer applies business rules, creates domain object
5. Application Layer calls Persistence Layer to save transaction
6. Persistence Layer writes to database
7. Application Layer returns result to UI
8. UI displays confirmation to user

---

## 🏗️ Layered Architecture in Practice

**Most real-world apps use this pattern!**

- Web: Django (views → services → models → ORM)
- Java: Spring Boot (controllers → services → domain → repositories)
- .NET: ASP.NET MVC (views → controllers → models → EF Core)

**Benefits:**

- Easy to test business logic without UI or database
- Can swap out layers (e.g., change database, update UI framework)
- Clear structure for teams

**Drawbacks:**

- Can become "too layered" (boilerplate, slow development)
- Sometimes layers are bypassed for performance (with care)

---

## Next: We'll look at a hands-on example and discuss common anti-patterns!

## 🛠️ Hands-On Example: Bank Account Withdrawal

Let's see how the layers interact in a simple bank account withdrawal use case:

**Domain Layer (Account domain object):**

```python
class Account:
		def __init__(self, id, balance):
				self.id = id
				self.balance = balance

		def can_withdraw(self, amount):
				return self.balance >= amount

		def withdraw(self, amount):
				if not self.can_withdraw(amount):
						raise Exception("Insufficient funds")
				self.balance -= amount
```

**Persistence Layer (AccountRepository/DAO):**

```python
class AccountRepository:
		def get_account_by_id(self, account_id):
				# Fetch from DB (pseudo-code)
				data = db.fetch("SELECT id, balance FROM accounts WHERE id = ?", account_id)
				return Account(id=data['id'], balance=data['balance'])

		def save_account(self, account):
				db.execute("UPDATE accounts SET balance = ? WHERE id = ?", account.balance, account.id)
```

**Application Layer (AccountService):**

```python
class AccountService:
		def __init__(self, account_repository):
				self.account_repository = account_repository

		def process_withdrawal(self, account_id, amount):
				account = self.account_repository.get_account_by_id(account_id)
				account.withdraw(amount)  # Calls domain method
				self.account_repository.save_account(account)
				return account.balance
```

**Presentation Layer:**

- Calls `AccountService.process_withdrawal()` when user requests a withdrawal.
- Displays result or error to the user.

**Flow Recap:**

1. UI calls Application Layer with withdrawal request.
2. Application Layer fetches domain object from Persistence Layer.
3. Application Layer calls domain object's business method.
4. Application Layer saves updated domain object via Persistence Layer.
5. UI displays result.

---

## 🚩 Common Anti-Patterns in Layered Architecture

**1. Logic Leakage:** - Business logic ends up in the Application or Persistence Layer instead of the Domain Layer. - Fix: Keep business rules in domain objects.

**2. Anemic Domain Model:** - Domain objects are just data containers with no behavior. - Fix: Put business methods and rules in domain objects, not just data.

**3. Layer Bypassing:** - UI or Application Layer talks directly to the database, skipping domain or persistence layers. - Fix: Always go through the proper layers.

**4. Tight Coupling:** - Layers depend on concrete implementations instead of interfaces/abstractions. - Fix: Use interfaces or abstract classes for dependencies between layers.

**5. Over-Engineering:** - Too many layers or unnecessary abstractions for simple apps. - Fix: Use as much layering as needed, but not more.

---

**Next:** Try sketching out your own layered design for a simple app, or let me know if you want to explore another architectural pattern!
