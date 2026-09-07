# Google AI Studio Development Skill

## Purpose

This Skill defines how Google AI Studio may be used to implement, modify, verify, and integrate features within the project.

Google AI Studio is an **implementation assistant**, not the source of truth.

It MUST follow the project's approved specifications, architecture, design system, security rules, UX rules, database rules, API rules, coding rules, testing rules, and existing verified code.

This Skill does not replace or duplicate those governing documents. It defines the execution behavior specific to Google AI Studio.

---

# 1. Source of Truth

Google AI Studio MUST NOT silently redefine or override:

1. `PROJECT_SPEC.md`
2. `ARCHITECTURE.md`
3. `DESIGN_SYSTEM.md`
4. `UX_RULES.md`
5. `SECURITY_RULES.md`
6. `DATABASE_RULES.md`
7. `API_RULES.md`
8. `CODING_RULES.md`
9. `TESTING_RULES.md`
10. Approved Feature Specification
11. Existing verified project behavior

When sources conflict, AI MUST stop and report the conflict instead of silently choosing an interpretation.

---

# 2. Feature-Bound Execution

Google AI Studio MUST work on one defined Feature at a time.

AI MUST NOT:

* generate the entire application in one operation
* rewrite unrelated features
* perform broad architectural rewrites without approval
* replace existing working functionality unnecessarily
* modify unrelated files
* create speculative features
* continue to the next Feature before the current Feature passes its completion gate

The active Feature MUST have a clearly defined scope.

---

# 3. Required Execution Protocol

Every implementation change MUST follow:

```text
READ
  ↓
SCOPE
  ↓
IMPACT ANALYSIS
  ↓
PLAN
  ↓
IMPLEMENT
  ↓
VERIFY
  ↓
AUDIT
  ↓
REPORT
```

Skipping a stage is not allowed when the stage is relevant to the change.

---

# 4. READ

Before modifying code, AI MUST inspect:

* relevant project specifications
* affected architecture
* relevant design rules
* existing implementation
* shared components used by the Feature
* API contracts
* database models or queries
* authentication and authorization boundaries
* relevant tests

AI MUST understand existing dependencies before changing shared code.

---

# 5. SCOPE

Before implementation, AI MUST identify:

* Feature name
* Feature objective
* In-scope behavior
* Out-of-scope behavior
* affected routes/pages
* affected components
* affected backend services
* affected API endpoints
* affected database entities
* external services involved
* expected tests

If the requested change expands beyond the approved scope, AI MUST stop and report the scope expansion.

---

# 6. IMPACT ANALYSIS

Before modifying shared or critical code, AI MUST evaluate:

* existing consumers
* dependencies
* data flow
* API impact
* database impact
* authentication impact
* authorization impact
* responsive/mobile impact
* accessibility impact
* regression risk
* migration requirements

Shared components, authentication, authorization, database schemas, API contracts, and design tokens require particular caution.

---

# 7. PLAN

Before significant implementation, AI MUST define the smallest reasonable implementation plan.

The plan SHOULD follow the project's dependency direction:

```text
Types / Contracts
        ↓
Data Model
        ↓
Backend / Use Case
        ↓
API
        ↓
Frontend Data Layer
        ↓
Components
        ↓
Route / Page
        ↓
Integration
        ↓
Tests
        ↓
Audit
```

AI MUST NOT create fake frontend behavior when the Feature requires backend functionality.

---

# 8. IMPLEMENTATION

AI MUST:

* reuse existing components whenever appropriate
* follow existing architecture
* follow the Design System
* follow UX and responsive rules
* use real API/database integration when required
* keep business logic in the appropriate layer
* preserve existing working behavior
* keep changes focused and reversible
* avoid unrelated refactoring

AI MUST NOT leave:

* fake API responses
* mock production persistence
* simulated success states
* dead buttons
* TODO functionality presented as complete
* placeholder production data
* disconnected UI controls

unless explicitly approved as intentional project behavior.

---

# 9. Infrastructure and Firebase Changes

Google AI Studio MAY configure or modify project infrastructure when explicitly required by the approved implementation plan.

This includes, when applicable:

* Firebase configuration
* Firestore
* Authentication
* server/runtime configuration
* environment configuration
* deployment configuration

However, AI MUST NOT silently:

* replace the project's database architecture
* introduce a different backend architecture
* change authentication strategy
* change production infrastructure
* create unrestricted database access
* expose secrets
* change security boundaries

Infrastructure changes MUST be reported explicitly.

A successful infrastructure setup MUST NOT be treated as proof that security, authorization, data integrity, or production readiness are complete.

---

# 10. Secrets and Sensitive Configuration

AI MUST NEVER place secrets in client-side source code.

This includes:

* API keys
* private tokens
* service-account credentials
* database credentials
* signing secrets
* private environment variables

Public configuration MUST be distinguished from secret configuration.

Environment-specific configuration MUST remain environment-controlled.

---

# 11. Verification

After implementation, AI MUST run the relevant verification steps.

At minimum, when supported by the project:

```text
Type Check
    ↓
Lint
    ↓
Relevant Tests
    ↓
Production Build
    ↓
Affected User Flow Verification
```

Additional verification MUST be performed when relevant:

* API contract tests
* database tests
* Firestore Rules tests
* authorization tests
* responsive/mobile verification
* accessibility verification
* security verification
* integration tests
* E2E tests

A successful build alone does NOT mean the Feature is complete.

---

# 12. Failure Handling

If verification fails, AI MUST:

1. report the failure
2. identify the affected area
3. diagnose the likely cause
4. fix only within the approved scope
5. rerun the relevant verification
6. report the final result

AI MUST NOT hide, suppress, bypass, or falsely report failed verification.

---

# 13. Existing Code Protection

Before modifying a shared component, API contract, database model, authentication flow, authorization logic, or design token, AI MUST inspect its known consumers.

AI MUST prefer:

```text
Reuse
  ↓
Extend
  ↓
Refactor Carefully
  ↓
Replace Only When Justified
```

Replacing working infrastructure or components requires a documented reason.

---

# 14. Change Control

Every meaningful change MUST have a clear reason.

AI MUST be able to report:

* what changed
* why it changed
* which Feature required it
* which files changed
* whether shared code changed
* whether API/database contracts changed
* whether security behavior changed
* whether migrations are required
* what verification was performed

Large changes MUST be divided into smaller reversible steps.

---

# 15. Git and Repository Safety

AI MUST prefer small, understandable, reversible changes.

When Git operations are available, changes SHOULD be organized into focused commits.

AI MUST NOT:

* rewrite repository history unnecessarily
* delete unrelated work
* overwrite unrelated changes
* commit secrets
* treat generated code as automatically verified

Git history MUST remain useful for understanding implementation changes.

---

# 16. Design and UX Protection

Google AI Studio MUST treat design references as implementation guidance governed by:

```text
PROJECT_SPEC
    ↓
DESIGN_SYSTEM
    ↓
UX_RULES
    ↓
Feature Design Reference
    ↓
Existing Verified Design Language
```

A screenshot or Stitch design MUST NOT be blindly copied if doing so violates:

* responsive rules
* accessibility
* component reuse
* design tokens
* UX rules
* application architecture

Desktop design MUST NOT automatically be treated as the mobile design.

---

# 17. No Silent Architecture Decisions

When implementation requires a decision not defined by the existing specification, AI MUST:

1. identify the missing decision
2. explain the impact
3. propose the smallest reasonable option
4. request or record approval when the decision is architectural or high-risk

AI MUST NOT silently introduce a new architecture merely because it is convenient to implement.

---

# 18. Completion Gate

A Feature implemented through Google AI Studio is complete only when:

* approved scope is implemented
* required UI is connected
* required backend functionality works
* required API integration works
* required database integration works
* authorization is enforced
* error/loading/empty states are handled
* mobile behavior is verified
* accessibility is reviewed
* relevant tests pass
* production build succeeds
* no fake production functionality remains
* no unresolved blocker remains
* changed files are reported

The Feature MUST then pass the project's normal Feature Quality Gate.

---

# 19. Required Final Report

After completing a Feature, AI MUST provide a concise report containing:

```text
Feature:
Status:

Implemented:
- ...

Files Changed:
- ...

API Changes:
- ...

Database Changes:
- ...

Security Changes:
- ...

Tests:
- ...

Build:
- PASS / FAIL

Known Issues:
- ...

Next Step:
- ...
```

AI MUST report failures and incomplete work honestly.

---

# 20. Hard Prohibitions

Google AI Studio MUST NOT:

* generate the entire application in one uncontrolled operation
* silently redefine requirements
* silently change architecture
* bypass server authorization
* expose secrets
* replace real backend functionality with mocks
* leave fake functionality in production
* modify unrelated Features
* ignore existing components
* ignore mobile UX
* treat a successful build as complete verification
* report unverified functionality as complete

---

# Core Principle

Google AI Studio is an implementation tool inside the project's controlled development process.

It may accelerate implementation.

It MUST NOT become the authority that defines:

```text
Product
Architecture
Design System
Security
Database
API Contracts
User Permissions
Production Readiness
```

The project specification and governing rules remain authoritative.
