# DEVELOPMENT RULES

## 1. Purpose

This document defines the general engineering rules used across all projects.

Project-specific requirements must be defined in `PROJECT_SPEC.md`.

Technology-specific decisions must be defined in `ARCHITECTURE.md`.

---

## 2. Core Engineering Principles

All code must prioritize:

1. Correctness
2. Security
3. Maintainability
4. Scalability
5. Performance
6. Accessibility
7. Testability
8. Simplicity

Do not sacrifice correctness for implementation speed.

Avoid unnecessary complexity.

---

## 3. Understand Before Changing

Before modifying existing code:

* Inspect the relevant files.
* Understand the existing architecture.
* Identify reusable components and utilities.
* Check existing API and database contracts.
* Check existing tests.
* Follow existing project conventions.

Do not rewrite working systems without a technical reason.

---

## 4. Component-First Development

For frontend development:

* Reuse existing components whenever possible.
* Extend an existing component when the interaction is substantially similar.
* Create a new component only when the behavior or responsibility is genuinely different.
* Avoid duplicated UI implementations.
* Keep components focused on a clear responsibility.
* Separate reusable UI from business logic.

Do not create page-specific copies of reusable components without justification.

---

## 5. Separation of Responsibilities

Keep responsibilities separated.

### UI

Responsible for:

* Presentation
* User interaction
* UI state
* Displaying loading/error/empty states

### Business Logic

Responsible for:

* Business rules
* Calculations
* Workflows
* Validation logic where appropriate

### API

Responsible for:

* Request/response contracts
* Authentication
* Authorization
* Input validation
* Error responses

### Database

Responsible for:

* Persistence
* Data integrity
* Indexing
* Transactions
* Data relationships

Do not place the entire application logic inside UI components.

---

## 6. Type Safety

When TypeScript is used:

* Prefer strict typing.
* Avoid `any`.
* Define explicit interfaces/types for important data structures.
* Keep API request and response types synchronized.
* Do not bypass the type system without a documented reason.
* Validate external data at runtime.

TypeScript types alone do not replace runtime validation.

---

## 7. Naming

Use clear and consistent naming.

### Components

Use PascalCase:

```text
ProductCard.tsx
CheckoutForm.tsx
UserTable.tsx
```

### Functions and variables

Use camelCase:

```text
calculateTotal()
getUserOrders()
isAuthenticated
```

### Constants

Use project-consistent naming, normally:

```text
MAX_RETRY_COUNT
API_BASE_URL
```

Names must describe purpose, not implementation details.

Avoid unclear names such as:

```text
data
temp
thing
stuff
x
foo
```

when a meaningful name is possible.

---

## 8. File and Folder Structure

Organize code by responsibility and project architecture.

Avoid:

* Extremely large files.
* Unrelated functionality in the same file.
* Deeply nested folders without purpose.
* Random file placement.

Follow the structure defined in `ARCHITECTURE.md`.

Do not introduce a new architectural pattern without justification.

---

## 9. State Management

Use the simplest state-management solution that correctly solves the problem.

Rules:

* Keep local state local when possible.
* Do not create global state unnecessarily.
* Do not duplicate the same source of truth.
* Server state and UI state should be treated separately.
* Persistent data should have a clear authoritative source.

Avoid unnecessary state synchronization.

---

## 10. API Development

All APIs must have explicit contracts.

Define:

* Endpoint
* HTTP method
* Request format
* Response format
* Authentication requirements
* Authorization requirements
* Validation rules
* Error responses

Frontend must not assume an API exists without verifying its contract.

Do not create frontend-only fake APIs for production functionality.

---

## 11. Backend Development

Backend code must:

* Validate incoming data.
* Authenticate users where required.
* Authorize actions server-side.
* Handle errors consistently.
* Avoid exposing sensitive information.
* Use proper logging.
* Keep business logic organized.
* Use the database correctly.
* Avoid trusting client-provided permissions.

Security decisions must never depend only on frontend checks.

---

## 12. Database

Database design must be intentional.

Before implementing persistent functionality:

* Define the data model.
* Define required fields.
* Define relationships.
* Define indexes where required.
* Define constraints and validation.
* Consider transactions for multi-step updates.
* Consider data consistency and concurrency.

Do not use temporary in-memory storage for production persistence unless explicitly required by the project architecture.

---

## 13. Error Handling

Every important operation must consider failure.

Handle:

* Network errors
* Validation errors
* Authentication errors
* Authorization errors
* Database errors
* Unexpected server errors
* Empty states
* Timeout/retry scenarios where appropriate

Never silently swallow errors.

Do not use empty `catch` blocks.

User-facing errors must be understandable without exposing sensitive technical information.

---

## 14. Loading and Empty States

Data-driven interfaces must define appropriate:

* Loading states
* Empty states
* Error states
* Success states

Do not leave users with blank screens while operations are running.

---

## 15. Security

Security must be considered during implementation, not added afterward.

Minimum principles:

* Validate all untrusted input.
* Sanitize where required.
* Enforce authorization server-side.
* Never expose secrets in frontend code.
* Never commit credentials or private keys.
* Use secure authentication/session handling.
* Follow least-privilege principles.
* Do not trust client-provided roles or permissions.
* Protect sensitive endpoints.

Follow `SECURITY_RULES.md` for detailed security requirements.

---

## 16. Dependencies

Before adding a dependency:

1. Check whether the project already provides the functionality.
2. Check whether an existing dependency can solve it.
3. Consider maintenance and security.
4. Avoid unnecessary packages.

Do not add dependencies only for trivial functionality that can be implemented safely with existing tools.

---

## 17. Performance

Performance should be considered during implementation.

Avoid:

* Unnecessary renders.
* Unnecessary API requests.
* Unoptimized database queries.
* Large unnecessary client bundles.
* Repeated expensive calculations.
* Loading resources that are not needed.

Do not prematurely optimize without evidence.

---

## 18. Accessibility

Interfaces must support accessible usage.

Consider:

* Keyboard navigation
* Focus management
* Semantic structure
* Labels
* Accessible names
* Contrast
* Touch targets
* Screen-reader compatibility

Follow `UX_RULES.md` and `DESIGN_SYSTEM.md`.

---

## 19. Responsive Development

Responsive behavior is part of implementation, not a final adjustment.

Verify required layouts on:

* Mobile
* Tablet
* Desktop

Do not simply shrink the desktop layout.

Mobile-specific UX should be implemented where necessary.

---

## 20. Testing

Important functionality must be tested at the appropriate level.

Use:

* Unit tests
* Integration tests
* API tests
* End-to-end tests

as required by the feature.

A feature is not complete because the UI renders successfully.

Follow `TESTING_RULES.md`.

---

## 21. No Fake Completion

The following do NOT count as completed functionality:

* Static UI without required backend integration.
* Mock data replacing required database functionality.
* API endpoints that do not persist required data.
* Database models without working application integration.
* Buttons without implemented actions.
* Forms without validation/submission handling.
* Features that only work on the happy path.
* Desktop-only implementation when mobile is required.

---

## 22. Refactoring

Refactor when it improves:

* Readability
* Reusability
* Maintainability
* Performance
* Architecture
* Security

Avoid unnecessary rewrites.

Do not refactor unrelated areas while implementing a focused feature unless required.

---

## 23. Git and Changes

Keep changes focused.

Each change should have a clear purpose.

Avoid mixing:

* Feature development
* Unrelated refactoring
* Large formatting changes
* Dependency changes

unless they are genuinely related.

Before committing, verify that the project still builds and relevant tests pass.

---

## 24. Documentation

Important architectural or behavioral decisions must be documented.

If implementation differs from the specification:

* Identify the difference.
* Explain why.
* Update the appropriate documentation when approved.

Documentation must reflect the actual system.

---

## 25. Completion Rule

Before declaring a task complete:

* Requirements are satisfied.
* Code builds successfully.
* Relevant tests pass.
* API integration works.
* Database integration works when required.
* Security requirements are satisfied.
* UX requirements are satisfied.
* Responsive behavior is verified.
* No known critical blocker remains.

If any required item is incomplete, report the task as incomplete.
