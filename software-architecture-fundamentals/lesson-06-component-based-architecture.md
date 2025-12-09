# Lesson 06: Component-Based Architecture

## Overview

Component-Based Architecture is a design paradigm that structures a system as a set of loosely coupled, independently deployable components. Each component encapsulates its behavior and communicates with others through well-defined interfaces.

## Learning Objectives

- Understand the principles of component-based architecture
- Identify the benefits and challenges of using components
- Learn how to design and document component-based systems

## Key Concepts

- **Component**: A modular, replaceable, and reusable set of functionalities.
- **Interface**: Defines how components interact with each other.
- **Coupling and Cohesion**: Components should be highly cohesive and loosely coupled.
- **Reusability**: Components can be reused across different systems.

### How this differs from frontend UI components

- Frontend UI components are usually about **rendering and interaction** (buttons, cards, modals) and live in the presentation layer.
- Architectural components are **chunks of system capability** (auth, billing, catalog) that encapsulate logic, data access, and contracts; they may expose APIs, events, or SDKs.
- UI components are typically in-process, tightly scoped to UX; architectural components can be in-process libraries or out-of-process services.
- A frontend UI component (e.g., CheckoutForm) might call an architectural component (e.g., CheckoutService API) to perform work.

## Benefits

- Improved maintainability
- Enhanced reusability
- Easier testing and deployment
- Scalability

**When is it most useful?**

Component-based architecture is especially valuable for larger systems or teams (e.g., 10+ components or multiple teams). It enables parallel development, clear ownership, and easier scaling. For small apps or teams, the overhead may not be justified, but for complex systems, it brings much-needed structure and agility.

## Challenges

- Managing dependencies between components
- Versioning and compatibility
- Performance overhead due to abstraction

## Example

A web application might have components for authentication, user management, and payment processing. Each can be developed, tested, and deployed independently.

### Game-Oriented Example: Components as Systems

In a game, you might have these components:

- **Inventory Component**: Manages player inventory, exposes API (add/remove/list items), emits events (itemAdded, itemRemoved).
- **Player Component**: Manages player state (health, position), calls Inventory API, subscribes to inventory events.
- **Game State Component**: Tracks overall game progress, coordinates between Player and Inventory.
- **UI/Rendering**: Uses APIs/events from other components to display state, but does not reach into their internals.

**Interaction Diagram:**

```
┌──────────────┐      addItem()      ┌──────────────┐
│  Player      │ ────────────────▶   │  Inventory   │
│  Component   │                    │  Component   │
└─────┬────────┘   itemAdded event   └─────┬────────┘
	│   ◀───────────────────────────────┘
	│
	▼
┌──────────────┐
│  UI Layer    │
└──────────────┘
```

This separation allows you to evolve, test, or swap out components independently, as long as their APIs/events remain consistent.

## Exercise

1. Identify three components in a system you use daily (e.g., email, banking app).
2. Describe their responsibilities and interfaces.
3. Discuss how these components might interact.

---

_Next: Lesson 07 - Microservices Architecture_
