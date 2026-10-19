# Zerodha Kite Web Application Test Cases

**Source plan:** [01_Zerodha_Kite_Test_Plan.md](../01_Zerodha_Kite_Test_Plan.md)  
**Status:** Draft; acceptance criteria and expected product behavior require approval  
**Execution status:** Not run. No test environment or test results were supplied.

## Execution controls

- Run only against a documented, authorized QA environment with synthetic accounts and data.
- Do not use real customer accounts, real funds, or live orders. Order submission is allowed only in an explicitly approved isolated simulator.
- Exact messages, field rules, authentication factors, boundaries, browser versions, and session policies must be confirmed before execution.
- Keep credentials, OTPs, recovery codes, API secrets, and personal data out of this document, screenshots, logs, and reports.
- Record **Blocked** when a prerequisite is missing; never count a blocked test as passed.

## Shared execution record

For each run, record: build/version, environment, tester/date, non-sensitive test-data reference, actual result, status (Pass/Fail/Blocked/Not Run), defect link, and evidence link. Current actual results and evidence are **Not executed / N/A** for every case below.

## Authentication and session

### AUTH-001 - Valid login

- **Requirement:** AC-LOGIN-001
- **Priority:** Critical
- **Preconditions:** Authorized QA URL is available; synthetic account is active; documented login and additional-verification flow is approved.
- **Test data:** Valid synthetic account and verification method provisioned through the approved secure process; do not record secret values here.
- **Steps:**
  1. Open the authorized QA URL.
  2. Enter the valid synthetic account identifier and password.
  3. Complete each required verification step using approved test data.
  4. Wait for the application to finish authentication.
- **Expected result:** Authentication succeeds and the documented landing screen is displayed. Protected content is available only after authentication; secrets are not exposed in the UI or diagnostics.
- **Actual result:** Not executed.
- **Status:** Not Run.
- **Evidence:** N/A.

### AUTH-002 - Reject invalid password

- **Requirement:** AC-LOGIN-002
- **Priority:** Critical
- **Preconditions:** Authorized QA URL; synthetic account; approved retry/lockout policy and account-reset method. Use an environment where a failed attempt cannot affect a real account.
- **Test data:** Valid synthetic account identifier and deliberately incorrect test password.
- **Steps:**
  1. Open the authorized QA URL.
  2. Enter the synthetic account identifier and incorrect password.
  3. Submit the login form once.
  4. Inspect the response and verify access to a protected route is not granted.
- **Expected result:** Login is rejected; the approved safe error behavior is shown; no protected data or sensitive authentication detail is exposed. Retry behavior follows the documented policy.
- **Actual result:** Not executed.
- **Status:** Not Run.
- **Evidence:** N/A.

### AUTH-003 - Validate missing mandatory fields

- **Requirement:** AC-LOGIN-003
- **Priority:** High
- **Preconditions:** Authorized QA URL; required login fields and approved validation behavior are documented.
- **Test data:** No credentials.
- **Steps:**
  1. Open the login page.
  2. Submit with all required fields empty.
  3. Repeat with each required field omitted individually while supplying the others with non-secret test values.
- **Expected result:** Submission is prevented or the approved validation is displayed for each missing field. No authenticated session is created.
- **Actual result:** Not executed.
- **Status:** Not Run.
- **Evidence:** N/A.

### AUTH-004 - Reject invalid, expired, or missing additional verification

- **Requirement:** AC-LOGIN-001
- **Priority:** High
- **Preconditions:** Authorized QA environment; additional-verification flow and negative test-data/reset procedures are confirmed.
- **Test data:** Synthetic account plus separately provisioned invalid, expired, and missing verification cases, as supported by the environment.
- **Steps:**
  1. Start login with valid primary credentials.
  2. For separate runs, submit an invalid verification value, an expired value, and no value where the flow allows submission.
  3. Observe the result and attempt to access a protected route.
- **Expected result:** Authentication does not complete for each invalid/missing case. Approved error and retry behavior is followed; protected content remains inaccessible; secrets are not exposed.
- **Actual result:** Not executed.
- **Status:** Not Run.
- **Evidence:** N/A.

### AUTH-005 - Enforce session expiry

- **Requirement:** AC-LOGIN-004
- **Priority:** Critical
- **Preconditions:** Authenticated synthetic account; approved session timeout, protected action, and safe time-advance/test-hook procedure are documented.
- **Test data:** Synthetic account with no real account data.
- **Steps:**
  1. Authenticate and open a protected page.
  2. Allow the documented timeout to elapse or use an approved test hook to expire the session.
  3. Attempt to refresh the page and perform a protected action.
- **Expected result:** The expired session cannot access protected data or perform protected actions. The application follows the approved redirect/re-authentication behavior and does not display stale protected content.
- **Actual result:** Not executed.
- **Status:** Not Run.
- **Evidence:** N/A.

### AUTH-006 - Logout and prevent protected access through browser history

- **Requirement:** AC-LOGOUT-001
- **Priority:** Critical
- **Preconditions:** Authenticated synthetic account; protected route identified; logout behavior documented.
- **Test data:** Synthetic account.
- **Steps:**
  1. Authenticate and open a protected page.
  2. Use the application’s logout action.
  3. Use browser Back and attempt to refresh the protected page.
  4. Open the protected route directly in a new tab.
- **Expected result:** The session is ended according to policy. Cached content is not usable for protected actions; refresh and direct navigation require re-authentication.
- **Actual result:** Not executed.
- **Status:** Not Run.
- **Evidence:** N/A.

### ACCESS-001 - Deny protected routes without a valid session

- **Requirement:** AC-LOGIN-004
- **Priority:** Critical
- **Preconditions:** Authorized QA URL; protected routes and unauthenticated/expired-session behavior are documented.
- **Test data:** No session, then a separately expired synthetic session.
- **Steps:**
  1. Open a protected route directly without logging in.
  2. Repeat after authenticating and expiring the session through the approved method.
  3. Check page content and attempt one protected action in each state.
- **Expected result:** Access is denied or redirected as specified. Account data and protected actions are unavailable until a valid session is established.
- **Actual result:** Not executed.
- **Status:** Not Run.
- **Evidence:** N/A.

## Search, Market Watch, and instrument details

### SEARCH-001 - Search exact, partial, and unmatched instrument terms

- **Requirement:** AC-MW-001
- **Priority:** High
- **Preconditions:** Authorized synthetic account; approved instrument fixture and search matching rules are available.
- **Test data:** Known exact-match term, supported partial-match term, and term with no matching instrument.
- **Steps:**
  1. Search for the exact-match term and record returned instruments.
  2. Search for the partial-match term.
  3. Search for the unmatched term.
  4. Select a result only in the approved test environment and verify its identity.
- **Expected result:** Results follow documented matching and ranking rules; the unmatched term shows the approved empty state; selection cannot silently resolve to a different instrument.
- **Actual result:** Not executed.
- **Status:** Not Run.
- **Evidence:** N/A.

### MW-001 - Add and remove an instrument from Market Watch

- **Requirement:** AC-MW-001
- **Priority:** High
- **Preconditions:** Authorized synthetic account; one approved test instrument; add/remove and persistence behavior documented.
- **Test data:** Known instrument identifier from the approved fixture.
- **Steps:**
  1. Search for the test instrument.
  2. Add it to Market Watch.
  3. Verify the displayed instrument identity.
  4. Navigate away and return or reload if persistence is part of the requirement.
  5. Remove the instrument and verify the list again.
- **Expected result:** The correct instrument is added and removed. Persistence matches the documented rule; no unrelated Market Watch entries are changed.
- **Actual result:** Not executed.
- **Status:** Not Run.
- **Evidence:** N/A.

### MW-002 - Handle duplicate additions and Market Watch limit

- **Requirement:** AC-MW-001
- **Priority:** Medium
- **Preconditions:** Authorized synthetic account; duplicate and maximum-list behavior/limits are documented; test list can be reset.
- **Test data:** One instrument for duplicate checks and approved fixtures to reach the documented list limit.
- **Steps:**
  1. Add the same instrument more than once.
  2. Verify the list for duplicate entries.
  3. Populate the list to the documented limit.
  4. Attempt to add one more instrument.
- **Expected result:** Duplicate handling and limit behavior match the specification; the list remains consistent and provides approved feedback when a limit prevents an addition.
- **Actual result:** Not executed.
- **Status:** Not Run.
- **Evidence:** N/A.

### INSTR-001 - Verify instrument details match the selected instrument

- **Requirement:** AC-INSTR-001
- **Priority:** High
- **Preconditions:** Authorized synthetic account; approved instrument fixture identifies expected fields and values.
- **Test data:** Known instrument in search/Market Watch and corresponding fixture.
- **Steps:**
  1. Select the test instrument from search or Market Watch.
  2. Open its details view.
  3. Compare the displayed instrument identity and requirement-defined fields with the approved fixture.
  4. Navigate to another instrument and verify the view updates to that selection.
- **Expected result:** Instrument identity and specified fields correspond to the selected instrument and approved source. No stale details from the previous selection are shown.
- **Actual result:** Not executed.
- **Status:** Not Run.
- **Evidence:** N/A.

## Order entry and order book

### ORDER-001 - Reject order entry with missing required fields

- **Requirement:** AC-ORDER-001
- **Priority:** Critical
- **Preconditions:** Isolated authorized simulator; documented order fields and validation behavior; no live routing possible.
- **Test data:** Synthetic account and approved instrument; leave each required field empty in separate attempts.
- **Steps:**
  1. Open order entry for the test instrument in the simulator.
  2. Submit or validate with all required fields empty.
  3. Repeat with each required field omitted individually.
  4. Confirm whether any order record was created.
- **Expected result:** Invalid submissions are rejected with documented validation. No order is created or routed outside the simulator.
- **Actual result:** Not executed.
- **Status:** Not Run.
- **Evidence:** N/A.

### ORDER-002 - Validate order quantity, price, and combinations at boundaries

- **Requirement:** AC-ORDER-001
- **Priority:** Critical
- **Preconditions:** Isolated simulator; approved minimum/maximum values, increments, instrument rules, and invalid combinations documented.
- **Test data:** Synthetic instrument and boundary values supplied by product/environment owner.
- **Steps:**
  1. For each documented numeric boundary, test just below, at, and just above the boundary.
  2. Test values that violate documented increments or precision.
  3. Test each documented invalid order-type/field combination.
  4. Validate without submitting a live order; inspect whether a simulator record is created.
- **Expected result:** Each value and combination is accepted or rejected according to documented rules with appropriate feedback. No live order is created or routed.
- **Actual result:** Not executed.
- **Status:** Not Run.
- **Evidence:** N/A.

### ORDER-003 - Cancel a valid simulated order before final submission

- **Requirement:** AC-ORDER-002
- **Priority:** Critical
- **Preconditions:** Isolated simulator confirmed; synthetic account/instrument; valid test values; documented review/cancel flow.
- **Test data:** One approved valid simulated order payload; do not include account secrets.
- **Steps:**
  1. Open order entry and enter the approved valid test values.
  2. Open the review/confirmation step.
  3. Compare the review with the entered values.
  4. Cancel before final submission.
  5. Inspect the order book for any created record.
- **Expected result:** Review values match the input. Cancel exits the flow without creating an order record or initiating an external trade.
- **Actual result:** Not executed.
- **Status:** Not Run.
- **Evidence:** N/A.

### ORDER-004 - Submit and track an authorized simulated order

- **Requirement:** AC-ORDER-002
- **Priority:** Critical
- **Preconditions:** **Blocked** until an isolated simulator, written authorization, controlled synthetic data, and safe order parameters are confirmed.
- **Test data:** One approved simulated order and synthetic account/instrument.
- **Steps:**
  1. Confirm the active environment is the approved isolated simulator and verify its safety boundary.
  2. Enter the approved order values and review them.
  3. Submit only after explicit test authorization.
  4. Record the simulator response and inspect the corresponding order-book record/status.
- **Expected result:** Simulator response and order status follow documented behavior. No exchange execution or live trade is implied; stop immediately if simulator isolation cannot be verified.
- **Actual result:** Not executed.
- **Status:** Blocked - simulator and authorization not confirmed.
- **Evidence:** N/A.

### BOOK-001 - Verify simulated order-book records and statuses

- **Requirement:** AC-BOOK-001
- **Priority:** High
- **Preconditions:** Authorized simulator; synthetic order records and approved status-transition mapping available.
- **Test data:** Known simulated records covering the documented statuses.
- **Steps:**
  1. Open the order book for the synthetic account.
  2. Compare record identity and status with the approved fixture.
  3. Refresh or revisit the order book if that behavior is specified.
  4. Observe transitions only when generated by the approved simulator workflow.
- **Expected result:** Records and status transitions match documented simulator behavior; data belongs only to the authorized synthetic account.
- **Actual result:** Not executed.
- **Status:** Not Run.
- **Evidence:** N/A.

## Holdings and positions

### PORT-001 - Display authorized populated holdings and positions

- **Requirement:** AC-PORTFOLIO-001
- **Priority:** High
- **Preconditions:** Authorized synthetic account with approved populated holdings/positions fixture.
- **Test data:** Synthetic portfolio fixture and expected values from the environment owner.
- **Steps:**
  1. Authenticate as the approved synthetic account.
  2. Open holdings and compare requirement-defined fields with the fixture.
  3. Open positions and compare requirement-defined fields with the fixture.
  4. Confirm data is associated only with the authorized test account.
- **Expected result:** Displayed values match approved synthetic data; unrelated account data is not exposed.
- **Actual result:** Not executed.
- **Status:** Not Run.
- **Evidence:** N/A.

### PORT-002 - Display empty holdings and positions states

- **Requirement:** AC-PORTFOLIO-001
- **Priority:** Medium
- **Preconditions:** Authorized synthetic account with no holdings or positions; empty-state requirements confirmed.
- **Test data:** Approved empty portfolio fixture.
- **Steps:**
  1. Authenticate as the synthetic account with empty portfolio data.
  2. Open holdings.
  3. Open positions.
  4. Verify the views remain usable and navigate away/back if required.
- **Expected result:** Each view displays its documented empty state and does not show unrelated or stale portfolio data.
- **Actual result:** Not executed.
- **Status:** Not Run.
- **Evidence:** N/A.

## Cross-cutting quality checks

### COMPAT-001 - Run critical smoke flows on the supported browser/device matrix

- **Requirement:** Approved platform matrix (TBD)
- **Priority:** High
- **Preconditions:** Product-approved browser versions and viewports; authorized environment; smoke scenarios selected.
- **Test data:** Synthetic account and stable test fixtures.
- **Steps:**
  1. For each approved browser/device combination, run login, search/Market Watch, and one protected-page smoke flow.
  2. Record browser/version, device/viewport, and any layout or interaction differences.
  3. Run order-related checks only in the approved simulator.
- **Expected result:** Critical flows operate according to requirements on each supported combination. Unsupported combinations are recorded as out of scope, not failed.
- **Actual result:** Not executed.
- **Status:** Not Run.
- **Evidence:** N/A.

### A11Y-001 - Check keyboard access and critical form accessibility

- **Requirement:** Approved accessibility standard (TBD)
- **Priority:** Medium/High
- **Preconditions:** Authorized environment; accessibility standard and applicable WCAG level confirmed.
- **Test data:** Synthetic account; login and critical form pages.
- **Steps:**
  1. Navigate login and critical form controls using keyboard only.
  2. Verify focus order and visible focus against the approved standard.
  3. Inspect accessible names/labels and required-field/error announcements with approved tooling.
  4. Check contrast and responsive behavior against the agreed criteria.
- **Expected result:** Interactions meet the approved accessibility criteria; each violation has a reproducible description and non-sensitive evidence.
- **Actual result:** Not executed.
- **Status:** Not Run.
- **Evidence:** N/A.

### SEC-001 - Verify approved authentication and session security controls

- **Requirement:** Approved security/session policy (TBD)
- **Priority:** Critical
- **Preconditions:** **Blocked** until written authorization, security policy, test account, retry limits, and test boundaries are approved.
- **Test data:** Synthetic account and approved policy values only.
- **Steps:**
  1. Verify invalid-login responses do not reveal secrets or protected data.
  2. Verify protected routes reject unauthenticated and expired sessions.
  3. Verify logout invalidates the session as specified.
  4. Exercise retry/rate-limit checks only within the written authorization and agreed limits.
- **Expected result:** Observed behavior meets the approved security policy; no protected data is exposed. Stop if authorization or safe limits are unclear.
- **Actual result:** Not executed.
- **Status:** Blocked - written authorization and policy not confirmed.
- **Evidence:** N/A.

### PERF-001 - Measure agreed user journeys against approved performance objectives

- **Requirement:** Approved performance SLOs (TBD)
- **Priority:** Medium/High
- **Preconditions:** **Blocked** until an isolated environment, written workload authorization, workload limits, and measurable SLOs are approved.
- **Test data:** Synthetic accounts/data and an approved workload profile.
- **Steps:**
  1. Confirm the target is isolated and the workload is within written limits.
  2. Execute only the approved user journey and workload profile.
  3. Collect agreed latency/throughput/error measurements.
  4. Compare results with approved thresholds and record environment/build details.
- **Expected result:** Measurements are evaluated against explicit SLOs. No production or third-party load is generated; stop if scope or isolation is uncertain.
- **Actual result:** Not executed.
- **Status:** Blocked - environment and SLOs not confirmed.
- **Evidence:** N/A.

## Open items before execution

1. Confirm the authorized Kite QA URL, build/version, and written test boundary.
2. Approve authentication factors, error handling, retry/lockout rules, timeout, and logout behavior.
3. Confirm order rules and provide an isolated simulator before ORDER-004 or any order submission.
4. Approve instrument/search fixtures, portfolio fixtures, reset procedure, and synthetic test accounts.
5. Confirm browser/device versions, accessibility criteria, and performance SLOs.
6. Approve security test scope and workload limits before SEC-001 or PERF-001.
