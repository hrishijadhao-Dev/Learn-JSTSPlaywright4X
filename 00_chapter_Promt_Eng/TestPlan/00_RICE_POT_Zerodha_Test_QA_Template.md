# QA Test Plan: Zerodha Kite Trading Application

**Status:** Draft for product, QA, and security review  
**Prepared:** 2026-10-19  
**Plan scope:** Kite web application, with authentication as the first module and broader user workflows included  
**Requirements status:** Sample acceptance criteria are proposals pending validation; no execution is claimed.

## R - Role

QA/SDET approach focused on risk-based functional, integration, security, accessibility, compatibility, regression, and performance testing. Product behavior, security policies, and acceptance thresholds must be confirmed from approved requirements or an authorized test environment; this plan does not treat assumptions as product facts.

## I - Instructions

### Objective

Define a traceable, risk-based test approach for the Zerodha Kite web application. Establish readiness, coverage, safety controls, evidence, and release exit criteria before execution.

### Scope

**In scope, subject to requirement and environment confirmation:**

- Authentication: valid and invalid login, required-field validation, any configured additional verification, session expiry, re-authentication, and logout.
- Post-login landing screen and access to protected areas.
- Instrument search, Market Watch add/remove and display, and instrument details.
- Order-entry form validation and safe order-flow checks in a simulation or explicitly authorized non-production environment.
- Order book status display, holdings, and positions, including empty and populated states where authorized data is available.
- Functional, negative, boundary, regression, UI/accessibility, compatibility, session/security, API/integration, and performance coverage where requirements and suitable environments exist.

**Initial target matrix proposed by the requester:** Chrome, Edge, and Firefox; desktop, mobile web, and tablet; standard, unauthenticated, and expired-session states. Exact browser versions, viewport sizes, supported roles, and app-versus-web boundaries remain TBD. Native Android and iOS apps are not included in this plan.

### Out of scope and safety constraints

- Production testing is prohibited by default unless a documented procedure and explicit authorization approve specific activities.
- Never use real customer accounts, real customer data, real funds, or place live orders for routine QA.
- Do not assert that an order was accepted or executed by an exchange. Use a simulator or controlled test environment for order lifecycle checks.
- Kite Connect sandbox/API availability and applicability are unverified. API and integration tests require approved interface documentation, credentials provisioned through secure channels, and an authorized environment.
- Do not perform load, stress, or security testing against production or third-party systems without written authorization and defined limits.

### Requirements and proposed acceptance criteria

The following are generic proposals supplied during planning, not confirmed Zerodha requirements. Keep them in **Draft / Pending Validation** until approved by the product and security owners.

| ID | Proposed behavior | Validation needed |
|---|---|---|
| AC-LOGIN-001 | Given a user has valid test credentials and completes required authentication, when they submit the login flow, then access is granted and the appropriate post-login screen is displayed. | Confirm credential fields, verification steps, and destination. |
| AC-LOGIN-002 | Given a user is on login, when they submit an incorrect password, then access is rejected and a safe error is shown without exposing sensitive information. | Confirm retry, lockout/rate-limit policy, and error behavior. |
| AC-LOGIN-003 | Given required login fields are empty, when the form is submitted, then submission is prevented or appropriate validation is shown. | Confirm required fields and client/server validation behavior. |
| AC-LOGIN-004 | Given a user is authenticated, when the configured session expires, then protected actions require re-authentication. | Confirm timeout duration, session invalidation, and re-authentication behavior. |

Additional module acceptance criteria must be derived from approved requirements; they are not specified in this draft.

### Test strategy

1. Review approved requirements, user journeys, policies, API contracts, and supported-platform declarations. Record ambiguities before test design.
2. Map each approved requirement to one or more test cases and identify risk, priority, test data, and environment dependencies.
3. Use equivalence partitioning, boundary analysis, state-transition testing, and negative testing for inputs and workflow states. Apply role/permission checks only to roles confirmed to exist.
4. Run functional and integration checks first in an authorized stable environment. Add regression, accessibility, compatibility, security/session, and performance checks as their criteria and tooling are approved.
5. Capture reproducible steps and non-sensitive evidence for failures. Redact account identifiers, tokens, personal information, and other sensitive values.
6. Report blocked tests as **Blocked**, not **Passed**. Do not claim execution until results and evidence exist.

### Test types and representative coverage

| Area | Representative coverage | Priority |
|---|---|---|
| Authentication | Valid/invalid credentials, empty fields, verification flow, error handling, session expiry, re-authentication, logout | Critical |
| Search and Market Watch | Matching/no-match search, adding/removing instruments, duplicate and boundary behavior, display after navigation or refresh where specified | High |
| Instrument details | Correct instrument selection and display of requirement-defined details; refresh/update behavior only against an approved expectation | High |
| Order entry | Required fields, invalid/boundary values, order-type-specific validation, review/confirmation flow in simulation only | Critical |
| Orders | Authorized test-order lifecycle and order-book status transitions in a controlled environment | Critical |
| Holdings and positions | Authorized access, populated and empty states, consistency with approved test data | High |
| Permissions and session | Unauthenticated and expired-session access to protected actions; unauthorized-role checks if such roles are confirmed | Critical |
| Accessibility and UI | Keyboard access, focus order, labels, error announcement, contrast and responsive layout against an agreed standard | Medium/High |
| Compatibility and regression | Agreed browser/device matrix; rerun impacted critical workflows after changes | High |
| API/integration | Contract, validation, authorization, and dependency behavior only when interfaces and test access are approved | High |
| Performance | Baseline and agreed service-level objectives in a controlled environment; thresholds are TBD | Medium/High |

### Environment and URL

- **Product URL supplied:** `https://zerodha.com/` (company/product site; not confirmed as the authorized Kite test base URL).
- **Authorized QA environment:** None supplied. Staging/sandbox URL, build/version, and access procedure are TBD.
- **Execution status:** Planning only. No application access or tests have been performed.
- **Environment gate:** Do not execute account, order, API, security, or performance tests until the environment owner confirms authorization, isolation, test data, and safe operational limits.

### Test data and accounts

- Use synthetic or explicitly provisioned test accounts and instruments only.
- Never place credentials, OTPs, recovery codes, API secrets, or real personal data in this plan, source control, logs, screenshots, or test reports.
- Required account states and data sets (valid, invalid, boundary, expired session, empty/populated holdings, and simulated order states) must be provisioned by the environment owner.
- Data reset, cleanup, and retention procedures are TBD.

### Tools and technology

No test framework, test-management system, CI/CD pipeline, API client, reporting tool, or browser versions were specified. Select and approve these before automation or execution. Playwright may be evaluated for browser automation, but it is not an agreed project dependency in this plan.

### Entry criteria

- Product owner approves the in-scope modules and provides current requirements and acceptance criteria.
- QA environment, target URL, build/version, and access authorization are documented.
- Test accounts, synthetic data, and simulated order capability are available and verified.
- Supported browsers/devices, security/session policies, and any API contracts are documented.
- Test cases, severity definitions, evidence handling, and defect workflow are reviewed by QA and relevant owners.

### Exit criteria (proposed; approval required)

- All approved in-scope acceptance criteria map to test cases and have a recorded execution status.
- 100% of planned critical tests are executed, or remaining tests are explicitly documented as blocked with owner and impact.
- All critical tests pass; proposed overall pass rate is at least 95% of executed tests.
- Zero open critical or high-severity defects affecting authentication, session security, protected account access, or safe order handling.
- No unresolved critical security findings; required security review is complete.
- Agreed regression checks pass, and failures have linked defects and evidence.
- QA lead and designated product/security owners approve any exceptions and provide release sign-off.

The 95% pass rate and defect thresholds are planning proposals, not existing service-level or release requirements. Product/QA/security owners must approve or replace them before execution.

### Risks and dependencies

| Risk/dependency | Impact | Mitigation / owner action |
|---|---|---|
| No authorized test environment or test accounts | Execution cannot safely begin | Environment owner supplies and documents an isolated environment and synthetic accounts. |
| Authentication and session policies are unknown | Expected results and security coverage may be incorrect | Product/security owners confirm the approved login flow, retry policy, timeout, and session invalidation. |
| No approved order simulator or safe order flow | Order testing could cause financial or customer impact | Block order submission tests until simulation or explicit written authorization is available. |
| API/sandbox scope is unverified | Integration coverage may be unavailable or target the wrong interface | Confirm current sandbox support, contracts, and permitted test operations with the service owner. |
| Market data may be delayed or environment-dependent | Results may be nondeterministic | Define test fixtures, data freshness expectations, and tolerances. |
| Browser/device support and performance objectives are unspecified | Compatibility/performance results lack a pass/fail basis | Product owner publishes supported matrix and measurable thresholds. |

### Roles and responsibilities

| Role | Responsibility | Assigned owner |
|---|---|---|
| Product owner / business analyst | Confirm scope, business rules, requirements, and acceptance criteria | TBD |
| QA lead / SDET | Own test design, traceability, execution, evidence, and reporting | TBD |
| Environment owner | Provision authorized environment, accounts, synthetic data, and reset procedures | TBD |
| Security owner | Approve security coverage, policies, test authorization, and findings disposition | TBD |
| API/integration owner | Provide interface contracts and permitted sandbox operations | TBD |

### Schedule and reporting

Schedule, staffing, and release dates are not provided. Plan execution by phase after entry criteria are met: requirements review, test design, environment/data readiness, smoke test, risk-based execution, regression, and sign-off. Owners and dates are TBD.

Report per agreed test cycle with scope/build/environment, planned and executed counts, pass/fail/blocked status, defects by severity, risks, evidence links, requirement coverage, and go/no-go recommendation. Reporting cadence and system of record are TBD.

## C - Context

- **Product:** Zerodha Kite trading application, as clarified during planning.
- **Feature/workflow:** Broad web application workflows, starting with login/authentication; search, Market Watch, instrument details, order entry, order book, holdings, positions, and logout are proposed in scope.
- **User types:** Standard, unauthenticated, and expired-session states proposed. Restricted/admin roles are not assumed to exist.
- **Business rules:** Not yet supplied. Authentication details, order rules, market-data expectations, permissions, and state transitions require approved specifications.
- **Known limitations:** No QA environment, build, accounts, confirmed sandbox, API contract, browser versions, schedule, or assigned owners were supplied.

## E - Example workflow

1. Open the authorized test environment.
2. Authenticate with a provisioned synthetic test account using the documented flow.
3. Verify access to the authorized landing screen and protected areas.
4. Search for an approved test instrument and add it to Market Watch.
5. Verify instrument details against an approved fixture or expectation.
6. Validate order-entry fields without submitting a live order; exercise submission only in a confirmed simulator.
7. Verify order-book, holdings, and positions against authorized test data.
8. Log out and verify protected actions require authentication again.

Exact screens, messages, data, and transitions remain requirement-dependent. This is a planning example, not evidence of product behavior or test execution.

## P - Persona

Act as a QA Test Lead/SDET for a regulated financial application. Prioritize safety, authorization, traceability, privacy, deterministic test data, and explicit separation of verified requirements from assumptions. Do not test production trading by default, expose secrets, or report unexecuted tests as results.

## O - Output

- **Deliverable:** This test plan; detailed test cases, automation, and execution report are separate follow-up deliverables.
- **Format:** Markdown, with scope, strategy, matrix, environment, data, entry/exit criteria, risks, dependencies, roles, schedule, and reporting.
- **Detail:** Standard planning detail; requirements and thresholds that are not confirmed are marked TBD or proposed.
- **Acceptance:** QA, product, security, and environment owners review the plan; confirm requirements and safety gates; and approve or amend proposed exit criteria before execution.

## T - Tone

Technical, concise, risk-aware, and precise. Keep verified facts, proposals, and unresolved questions clearly distinguished.

## Open questions before execution

1. What is the official Kite QA/staging URL, build/version, and written authorization boundary?
2. Which exact authentication steps, retry/lockout rules, session timeout, and logout behavior are approved?
3. Which workflows and order types are in scope, and what is the approved simulator or non-production order path?
4. What are the supported browser versions, device/viewports, accessibility standard, and performance objectives?
5. Which roles, API contracts, sandbox capabilities, test accounts, synthetic data, reset procedure, owners, schedule, and reporting tool are available?
6. Do product, QA, and security owners approve the proposed 95% pass rate and defect-based exit criteria, or should they be changed?
