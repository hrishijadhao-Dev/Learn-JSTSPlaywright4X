# Zerodha Kite Web Application Test Plan

**Status:** Draft; product, QA, security, and environment approval required  
**Date:** 2026-10-19  
**Source brief:** [00_RICE_POT_Zerodha_Test_QA_Template.md](00_RICE_POT_Zerodha_Test_QA_Template.md)  
**Execution status:** Not run. This document defines planned tests only.

## 1. Objective

Define a risk-based test approach and scenario inventory for Zerodha Kite web workflows. Verify approved requirements in an authorized environment, with special care around authentication, protected account data, and trading actions.

All scenarios and acceptance criteria in this draft are proposals until confirmed against approved product requirements. Unknown product behavior is marked **TBD** rather than assumed.

## 2. Scope

### In scope

- Login and additional authentication, validation, session expiry, re-authentication, and logout.
- Protected-area access after authentication.
- Instrument search, Market Watch, and instrument details.
- Order-entry validation and simulated order flow only.
- Order book, holdings, and positions using approved synthetic data.
- Agreed browser/device compatibility, accessibility, regression, security/session, API/integration, and performance checks when requirements and environments are approved.

### Out of scope and safety rules

- Routine testing against production accounts, customer data, real funds, or live orders.
- Submitting any order unless an isolated simulator or explicitly authorized non-production environment is confirmed.
- Load, stress, or security testing against production or third parties without written authorization and limits.
- Native Android/iOS applications; this plan covers web only.

Do not put credentials, OTPs, recovery codes, API secrets, or personal data in test artifacts, source control, evidence, or logs. Never report a blocked or unexecuted test as passed.

## 3. Requirements and traceability

The login criteria below originated as generic examples in the source brief. Proposed module criteria are added to organize coverage; none are confirmed Zerodha requirements until approved.

| Requirement ID | Proposed acceptance criterion | Status |
|---|---|---|
| AC-LOGIN-001 | Valid test credentials and required verification grant access to the documented post-login screen. | Draft / pending validation |
| AC-LOGIN-002 | Invalid password is rejected with a safe error that does not expose sensitive information. | Draft / pending validation |
| AC-LOGIN-003 | Empty mandatory login fields prevent submission or show the approved validation. | Draft / pending validation |
| AC-LOGIN-004 | On configured session expiry, protected actions require re-authentication. | Draft / pending validation |
| AC-MW-001 | Search and Market Watch add/remove behavior follows approved matching, duplicate, limit, and persistence rules. | Draft / pending validation |
| AC-INSTR-001 | Instrument details correspond to the selected instrument and approved data source. | Draft / pending validation |
| AC-ORDER-001 | Invalid or boundary order inputs are rejected according to documented rules. | Draft / pending validation |
| AC-ORDER-002 | A valid test order can be submitted and tracked only in an authorized simulator. | Draft / pending validation |
| AC-BOOK-001 | Order-book entries and status transitions match approved simulated order data and rules. | Draft / pending validation |
| AC-PORTFOLIO-001 | Authorized holdings and positions display the approved synthetic data, including defined empty states. | Draft / pending validation |
| AC-LOGOUT-001 | Logout ends the session and protected actions require authentication afterward. | Draft / pending validation |

## 4. Test environment and data

- **Product URL supplied:** `https://zerodha.com/`; this is not confirmed as the Kite QA base URL.
- **Authorized test URL/build:** TBD. No QA environment was supplied.
- **Environment gate:** Obtain written authorization, isolation details, and operational limits before account, order, API, security, or performance tests.
- **Accounts and data:** Environment owner must provide synthetic accounts, permitted account states, instrument fixtures, simulated order data, reset/cleanup procedures, and data-retention rules.
- **Tools:** Test management, automation, CI, API client, and reporting tools are TBD. Playwright may be evaluated, but is not an approved dependency in this plan.
- **Proposed browser/device matrix:** Chrome, Edge, Firefox; desktop, mobile web, and tablet. Exact versions and viewport sizes require product confirmation. Safari and native mobile apps are not currently included.

## 5. Test approach

1. Review approved requirements, authentication/session policies, workflow rules, API contracts, supported platforms, and simulator behavior.
2. Resolve ambiguities and approve expected results before execution; update traceability IDs if product requirements use different identifiers.
3. Design tests using equivalence partitions, boundary analysis, negative testing, and state transitions.
4. Execute smoke and critical functional tests first in the authorized environment, followed by approved regression, compatibility, accessibility, integration, security/session, and performance checks.
5. Record environment/build, test data identifier (non-sensitive), steps, expected and actual results, status, evidence, and linked defects.
6. Redact sensitive values from screenshots, traces, logs, and reports. Use only approved test accounts and synthetic data.

## 6. Test case inventory

**Status for every case:** Not Run. **Actual result/evidence:** None until execution. Preconditions and expected results that depend on undocumented product behavior must be confirmed before running.

| ID | Requirement | Priority | Preconditions / data | Steps | Expected result | Status |
|---|---|---|---|---|---|---|
| AUTH-001 | AC-LOGIN-001 | Critical | Authorized QA URL; valid synthetic account; documented authentication method | Open login; enter valid credentials; complete required verification | Authentication succeeds and the documented landing screen is shown; no sensitive value is exposed | Not Run |
| AUTH-002 | AC-LOGIN-002 | Critical | Authorized QA URL; synthetic account with invalid-password test data | Enter valid user identifier and incorrect password; submit | Access is denied; approved safe error appears; no protected content is accessible | Not Run |
| AUTH-003 | AC-LOGIN-003 | High | Authorized QA URL | Submit with each mandatory field empty, then with required fields individually missing | Submission is prevented or approved field validation appears; no authenticated session is created | Not Run |
| AUTH-004 | AC-LOGIN-001 | High | Synthetic account; additional verification flow confirmed | Complete primary credentials; provide invalid, expired, or missing second factor as permitted by the test design | Authentication does not complete; approved error/retry behavior is followed without revealing secrets | Not Run |
| AUTH-005 | AC-LOGIN-004 | Critical | Authenticated synthetic account; timeout policy and test method documented | Allow or induce session expiry; request a protected page/action | Session is invalidated as specified; protected action requires re-authentication; no protected data is returned | Not Run |
| AUTH-006 | AC-LOGOUT-001 | Critical | Authenticated synthetic account | Log out; use browser back and attempt a protected URL/action | Session ends per policy; protected content is not available without re-authentication | Not Run |
| ACCESS-001 | AC-LOGIN-004 | Critical | No session and expired-session states; protected routes identified | Open protected routes directly; repeat with an expired session | Access is denied or redirected according to the approved policy; no account data is exposed | Not Run |
| SEARCH-001 | AC-MW-001 | High | Authorized session; approved instrument fixtures and search rules | Search exact, partial, valid, and unmatched terms | Results follow approved matching rules; unmatched terms show the defined empty state; no incorrect instrument is selected | Not Run |
| MW-001 | AC-MW-001 | High | Authorized session; known test instrument; Market Watch rules and limits documented | Add an instrument; inspect list; remove it; reload/navigate if persistence is specified | Correct item is added once and removed; persistence and list limits match approved rules | Not Run |
| MW-002 | AC-MW-001 | Medium | Authorized session; duplicate and list-limit behavior documented | Add the same instrument repeatedly; attempt to exceed the documented limit | Duplicate and limit behavior matches the specification; list remains consistent | Not Run |
| INSTR-001 | AC-INSTR-001 | High | Authorized session; approved instrument fixture | Select an instrument from search/Market Watch; open details | Displayed identity and requirement-defined fields match the selected instrument and approved fixture | Not Run |
| ORDER-001 | AC-ORDER-001 | Critical | Authorized simulator; order-entry rules and synthetic instrument data available | Open order entry; omit required fields and submit/validate without placing a live order | Invalid form is rejected with approved validation; no order is created | Not Run |
| ORDER-002 | AC-ORDER-001 | Critical | Simulator; documented quantity, price, and order-type boundaries | Test values below, at, and above each approved boundary; test invalid combinations | Values and combinations are accepted/rejected according to documented rules; no live order is submitted | Not Run |
| ORDER-003 | AC-ORDER-002 | Critical | Simulator confirmed; synthetic account/instrument; safe test order approved | Enter a valid test order; review; cancel before final submission | Review matches inputs; cancel exits without creating an order | Not Run |
| ORDER-004 | AC-ORDER-002 | Critical | Isolated simulator; submission explicitly authorized; controlled data | Submit one approved test order; inspect confirmation and resulting order record | Simulator returns the documented result and order identifier/status; no exchange execution or live trade is implied | Blocked until simulator and authorization are confirmed |
| BOOK-001 | AC-BOOK-001 | High | Simulator; known synthetic order records and approved status mapping | Open order book; compare records/statuses; refresh or revisit if specified | Visible records and transitions match the supplied fixture and approved state rules | Not Run |
| PORT-001 | AC-PORTFOLIO-001 | High | Authorized synthetic account with populated portfolio fixture | Open holdings and positions; compare displayed values with fixture | Authorized data is displayed and matches approved expected values; no unrelated account data is exposed | Not Run |
| PORT-002 | AC-PORTFOLIO-001 | Medium | Authorized synthetic account with no holdings/positions | Open holdings and positions | Approved empty state is displayed; page remains usable and does not imply an error unless specified | Not Run |
| COMPAT-001 | Platform matrix | High | Supported browser versions and viewports approved | Run critical smoke flows on each agreed desktop/mobile-web/tablet combination | Core workflows remain usable and consistent; deviations are recorded against supported-platform requirements | Not Run |
| A11Y-001 | Accessibility criteria | Medium/High | Agreed accessibility standard and test environment | Keyboard-navigate login and critical forms; inspect labels, focus, errors, and contrast | Critical interactions meet the agreed standard; violations are recorded with evidence | Not Run |
| SEC-001 | Security/session policies | Critical | Written authorization; approved test account and rate limits | Check safe error behavior, session invalidation, protected-route access, and approved retry controls | Behavior meets approved security policy; no sensitive data or protected content is exposed | Blocked until authorization and policy are confirmed |
| PERF-001 | Performance objectives | Medium/High | Isolated environment; workload limits and measurable SLOs approved | Measure agreed user journeys under the approved workload | Results meet approved thresholds; no production or third-party load is generated | Blocked until environment and SLOs are confirmed |

### Test case recording fields

For execution, record for each case: test case ID, run/build, environment, tester/date, test data reference (non-sensitive), actual result, status (Pass/Fail/Blocked/Not Run), defect link, and evidence link. A case is not **Pass** without observed evidence against an approved expected result.

## 7. Coverage matrix

| Area | Planned tests | Risk |
|---|---|---|
| Login and additional verification | AUTH-001 to AUTH-004 | Critical |
| Session, logout, protected access | AUTH-005, AUTH-006, ACCESS-001 | Critical |
| Search and Market Watch | SEARCH-001, MW-001, MW-002 | High |
| Instrument details | INSTR-001 | High |
| Order validation and simulator flow | ORDER-001 to ORDER-004 | Critical |
| Order book | BOOK-001 | High |
| Holdings and positions | PORT-001, PORT-002 | High |
| Compatibility and accessibility | COMPAT-001, A11Y-001 | Medium/High |
| Security and performance | SEC-001, PERF-001 | Critical / Medium-High; gated |

## 8. Entry criteria

- Product owner approves modules, requirements, and acceptance criteria.
- Authorized QA URL, build/version, access boundary, and environment owner are documented.
- Synthetic accounts, fixtures, simulator, and reset procedures are available and verified.
- Authentication/session policy, order rules, supported platform matrix, and applicable API contracts are documented.
- Test cases, defect workflow, evidence handling, severity definitions, and any security/performance authorization are reviewed.

## 9. Exit criteria

Proposed criteria; QA, product, and security owners must approve or replace before execution:

- All approved requirements map to test cases and have a recorded execution status.
- 100% of planned critical tests are executed, or remaining cases are recorded as Blocked with owner and impact.
- All critical tests pass; proposed overall pass rate is at least 95% of executed tests.
- No open critical/high defects affecting authentication, session security, protected account access, or safe order handling.
- No unresolved critical security findings; required security review is complete.
- Agreed regression suite passes; all failures have linked defects and evidence.
- QA lead and designated product/security owners approve exceptions and release readiness.

Blocked tests do not count as passed. The 95% target and defect thresholds are proposals, not known Zerodha release policy.

## 10. Risks, dependencies, and owners

| Risk/dependency | Impact / action | Owner |
|---|---|---|
| No authorized QA environment or test accounts | Execution cannot safely begin; provision isolated environment and synthetic data | Environment owner - TBD |
| Authentication/session rules unknown | Expected results may be inaccurate; publish approved policies | Product/security - TBD |
| No approved order simulator | Order submission tests remain blocked; confirm safe simulation capability | Product/environment owner - TBD |
| API/sandbox availability unverified | API coverage remains conditional; confirm current support, contracts, and allowed operations | API owner - TBD |
| Browser support and performance SLOs unknown | Compatibility/performance results lack pass criteria; approve matrix and thresholds | Product/engineering - TBD |
| Market data variability | Tests may be nondeterministic; define fixtures and freshness tolerances | Product/data owner - TBD |

## 11. Roles, schedule, and reporting

| Role | Responsibility | Owner |
|---|---|---|
| Product owner / business analyst | Confirm scope, business rules, requirements, and acceptance criteria | TBD |
| QA lead / SDET | Own test design, traceability, execution, evidence, and reporting | TBD |
| Environment owner | Provision authorized environment, accounts, synthetic data, and reset procedures | TBD |
| Security owner | Approve security scope, policies, authorization, and findings disposition | TBD |
| API/integration owner | Provide interface contracts and permitted simulator/API operations | TBD |

Schedule, staffing, release date, and reporting system are TBD. Execute in phases: requirements review, test design, environment/data readiness, smoke, risk-based execution, regression, and sign-off. Each report should include build/environment, scope, planned/executed/pass/fail/blocked counts, defects by severity, risks, coverage, evidence, and go/no-go recommendation.

## 12. Open questions before execution

1. What is the authorized Kite QA URL, build/version, and written testing boundary?
2. What are the exact login factors, retry/lockout rules, session timeout, and logout/session invalidation behavior?
3. Which order types and workflows are included, and what simulator is approved?
4. Which browser versions, viewports, accessibility standard, and performance SLOs are supported?
5. Which account roles, API contracts, sandbox capabilities, test data, reset procedures, owners, schedule, and reporting tools are available?
6. Do product, QA, and security owners approve the proposed exit thresholds?
