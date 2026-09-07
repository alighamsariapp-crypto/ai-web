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
2. `AGENTS.md`
3. `DEVELOPMENT_RULES.md`
4. `ARCHITECTURE.md`
5. `DESIGN_SYSTEM.md`
6. `UX_RULES.md`
7. `SECURITY_RULES.md`
8. `DATABASE_RULES.md`
9. `API_RULES.md`
10. `CODING_RULES.md`
11. `TESTING_RULES.md`
12. Approved Feature Specification
13. Existing verified project behavior

When relevant, the following rules also apply:

* `SEO_RULES.md`
* `PERFORMANCE_RULES.md`
* `DEPLOYMENT_RULES.md`
* `FIREBASE_RULES.md`
* `AI_SECURITY_RULES.md`
* `CONTENT_RULES.md`
* `COST_AND_QUOTA_RULES.md`
* `OBSERVABILITY_RULES.md`
* `PRIVACY_RULES.md`

When sources conflict, AI MUST stop and report the conflict instead of silently choosing an interpretation.

---

# 2. Feature-Bound Execution

Google AI Studio MUST work on one defined Feature at a time.

AI MUST NOT:

* generate the entire application in one operation
* rewrite unrelated Features
* perform broad architectural rewrites without approval
* replace existing working functionality unnecessarily
* modify unrelated files
* create speculative Features
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
INTEGRATE
  ↓
VERIFY
  ↓
AUDIT
  ↓
REPORT
```

Skipping a relevant stage is not allowed.

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
* relevant configuration
* relevant design references

AI MUST understand existing dependencies before changing shared code.

AI MUST NOT assume that a file, component, endpoint, database collection, or service does not exist without inspecting the relevant project structure.

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
* SEO impact when applicable
* performance impact
* deployment impact
* regression risk
* migration requirements

Shared components, authentication, authorization, database schemas, API contracts, design tokens, and deployment configuration require particular caution.

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

A Feature MAY use a shorter path when some layers are genuinely not required.

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
* maintain type safety
* implement required loading, error, empty, disabled, and success states
* preserve accessibility requirements

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

When Firebase is used, AI MUST follow `FIREBASE_RULES.md`.

However, AI MUST NOT silently:

* replace the project's database architecture
* introduce a different backend architecture
* change authentication strategy
* change production infrastructure
* create unrestricted database access
* expose secrets
* change security boundaries
* switch production and development environments

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

AI MUST follow the project's security and deployment rules for secret management.

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
* SEO verification
* performance verification

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

AI MUST NOT disable tests, validation, security controls, or type checking simply to obtain a passing result.

---

# 13. Existing Code Protection

Before modifying a shared component, API contract, database model, authentication flow, authorization logic, design token, or deployment configuration, AI MUST inspect its known consumers.

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
* discard existing user changes without authorization

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

Mobile behavior MUST be intentionally implemented according to the project's responsive rules.

---

# 17. Component Reuse

Before creating a new component, AI MUST inspect existing reusable components.

Preferred order:

```text
Existing Component
      ↓
Reuse
      ↓
Extend
      ↓
Create New Only If Interaction Is Genuinely Different
```

AI MUST NOT unnecessarily create duplicate:

* Buttons
* Inputs
* Selects
* Cards
* Modals
* Drawers
* Tables
* Tabs
* Dropdowns
* Headers
* Navigation
* Form controls

---

# 18. Major Workflow Protection

Major workflows MUST follow the page-first principle defined by the Design System and UX Rules.

Examples include:

* checkout
* order management
* product creation
* product editing
* complex admin workflows
* multi-step forms
* large data-management screens

These MUST NOT be implemented as small centered modals.

Preferred model:

```text
Simple Action
→ Modal

Medium Workflow
→ Drawer / Side Panel

Complex Workflow
→ Dedicated Page

Critical / Multi-Step Workflow
→ Full Page / Flow
```

Nested modals MUST NOT be introduced.

---

# 19. No Silent Architecture Decisions

When implementation requires a decision not defined by the existing specification, AI MUST:

1. identify the missing decision
2. explain the impact
3. propose the smallest reasonable option
4. request or record approval when the decision is architectural or high-risk

AI MUST NOT silently introduce a new architecture merely because it is convenient to implement.

---

# 20. API and Backend Integrity

When a Feature requires backend behavior, AI MUST implement the complete path:

```text
UI
↓
Frontend Data Layer
↓
API
↓
Authentication
↓
Authorization
↓
Validation
↓
Business Logic
↓
Database / External Service
↓
Response
↓
UI State
```

The Feature MUST NOT be marked complete if a required boundary is disconnected.

AI MUST follow `API_RULES.md` and `DATABASE_RULES.md`.

---

# 21. Authentication and Authorization

AI MUST NOT rely on frontend checks for security.

Required security decisions MUST happen server-side.

AI MUST preserve:

* authentication
* role checks
* permission checks
* ownership checks
* object-level authorization
* server-authoritative business rules

A hidden or disabled button is NOT authorization.

---

# 22. AI Security

If the Feature itself uses AI, AI MUST additionally follow:

`AI_SECURITY_RULES.md`

AI-generated output MUST be treated as untrusted unless explicitly validated.

AI MUST NOT allow an AI feature to bypass:

* authentication
* authorization
* validation
* business rules
* data-access boundaries
* tool permissions

High-risk AI actions MUST use the project's approved authorization and approval flow.

---

# 23. Performance

AI MUST consider applicable performance impact, including:

* unnecessary rendering
* network requests
* bundle size
* image loading
* code splitting
* data fetching
* database reads
* mobile performance
* third-party dependencies

AI MUST follow `PERFORMANCE_RULES.md`.

Performance changes MUST be verified rather than assumed.

---

# 24. SEO

For public Features where SEO applies, AI MUST consider:

* metadata
* canonical URLs
* indexing
* sitemap
* robots
* structured data
* internal links
* rendering strategy
* localization

AI MUST follow `SEO_RULES.md`.

SEO MUST NOT be implemented in a way that violates application architecture or UX requirements.

---

# 25. Observability

For backend and production Features, AI MUST consider applicable:

* error logging
* request identification
* important event logging
* metrics
* health information
* failure visibility

AI MUST follow `OBSERVABILITY_RULES.md`.

Logs MUST NOT expose secrets or unnecessary sensitive data.

---

# 26. Cost and Quota Awareness

When a Feature uses:

* AI APIs
* Firebase
* Firestore
* Storage
* serverless functions
* external APIs
* high-frequency background operations

AI MUST consider:

* request volume
* read/write amplification
* token usage
* storage usage
* bandwidth
* quotas
* rate limits
* expected cost

AI MUST NOT introduce uncontrolled polling, repeated requests, unbounded AI calls, or unnecessary database reads.

AI MUST follow `COST_AND_QUOTA_RULES.md` when present.

---

# 27. Deployment Protection

AI MUST NOT treat a successful local build as a production deployment.

Production deployment MUST follow:

`DEPLOYMENT_RULES.md`

AI MUST NOT:

* deploy to production without authorization
* bypass deployment checks
* switch production environments silently
* perform destructive production migrations without approval
* claim production readiness without required verification

---

# 28. Testing Before Completion

A Feature MUST NOT be marked complete until relevant tests pass.

Testing MUST cover both:

```text
Expected Behavior
```

and:

```text
Failure / Abuse Behavior
```

Where relevant, verify:

* authorization
* data isolation
* responsive behavior
* accessibility
* API contracts
* database behavior
* error handling
* concurrency
* idempotency
* third-party failures

---

# 29. Audit

After implementation, the Feature SHOULD pass a focused audit covering:

* requirement completeness
* design compliance
* responsive UX
* accessibility
* API integration
* database integration
* authorization
* security
* tests
* performance
* SEO when applicable
* regressions

Critical findings MUST block Feature completion.

---

# 30. Completion Gate

A Feature implemented through Google AI Studio is complete only when:

```text
Approved Scope
    ↓
Requirements PASS
    ↓
Design PASS
    ↓
Implementation PASS
    ↓
API / Backend PASS or N/A
    ↓
Database PASS or N/A
    ↓
Authentication PASS or N/A
    ↓
Authorization PASS
    ↓
Integration PASS
    ↓
Error / Loading / Empty States PASS
    ↓
Responsive UX PASS
    ↓
Accessibility PASS
    ↓
Security PASS
    ↓
Tests PASS
    ↓
Build PASS
    ↓
Audit PASS
```

No unresolved blocker may remain.

---

# 31. Required Final Report

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

Firebase / Infrastructure Changes:
- ...

Tests:
- ...

Build:
- PASS / FAIL

Audit:
- PASS / BLOCKED

Known Issues:
- ...

Next Step:
- ...
```

AI MUST report failures and incomplete work honestly.

---

# 32. Hard Prohibitions

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
* disable tests to make the project pass
* weaken security controls to make implementation easier
* silently switch environments
* perform destructive production operations without authorization

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

The objective is NOT:

> Generate as much code as possible.

The objective is:

> Make the smallest correct, secure, tested, integrated, maintainable change that satisfies the Feature requirements and all project rules.

AI MUST optimize for correctness, traceability, and convergence — not code volume.
