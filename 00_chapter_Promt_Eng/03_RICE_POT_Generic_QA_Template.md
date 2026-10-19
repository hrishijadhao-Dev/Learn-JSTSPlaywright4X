# RICE POT --- Generic QA Work Template

Use this prompt template for QA tasks, test plans, test cases, test
automation, defect analysis, and QA documentation. Replace bracketed
placeholders with project-specific details. Remove sections that do not
apply.

## R --- Role

Act as a \[QA role, e.g., Senior QA Engineer / SDET / QA Automation
Architect\] with \[years\] years of experience in \[domain/project
type\]. Apply strong knowledge of \[tools, technologies, frameworks,
standards, and testing methods\].

## I --- Instructions

-   **Task:** \[Describe the requested QA task or deliverable.\]
-   **Scope:** \[Application, feature, module, user journey, API, or
    system under test.\]
-   **Requirements:** \[List functional and non-functional
    requirements.\]
-   **Test coverage:** \[Positive, negative, boundary, exploratory,
    regression, accessibility, performance, security, or other relevant
    coverage.\]
-   **Tools and technology:** \[Languages, frameworks, libraries, test
    management tools, CI/CD, browsers, devices, environments.\]
-   **Design and standards:** \[Required patterns, coding standards,
    naming conventions, test design techniques, architecture, and
    reporting expectations.\]
-   **Constraints / mandatory rules:** \[Explicit must-do
    requirements.\]
-   **Prohibited practices:** \[Explicit must-not-do requirements.\]
-   **Assumptions and dependencies:** \[Known assumptions,
    prerequisites, test data, accounts, environment availability.\]
-   **Error handling and diagnostics:** \[Expected exception handling,
    logging, screenshots, evidence, retries, and failure reporting.\]
-   **Acceptance criteria:** \[Define what a successful deliverable or
    test run must demonstrate.\]

## C --- Context

Project/product: \[Name and short description\]

Feature or workflow: \[Feature under test\]

Environment and URL: \[Environment, base URL, build/version\]

User types and permissions: \[Relevant roles and access levels\]

Business rules: \[Rules and expected behaviors\]

Test data: \[Valid, invalid, boundary, and reusable data; do not include
real secrets\]

Known risks / limitations: \[Relevant risks, integrations, dependencies,
or constraints\]

## E --- Example

Provide an example of the desired structure, input, output, test case,
code pattern, or acceptance criteria.

\[Insert example here, or write "No example provided".\]

## P --- Persona

Work as a \[specific QA persona, e.g., Senior SDET / Test Lead / Test
Architect\]. Prioritize accuracy, maintainability, traceability,
risk-based coverage, clear evidence, and production-ready practices. Do
not invent requirements or claim tests were executed unless execution
evidence is available.

## O --- Output

Deliverables required: 1. \[Deliverable 1\] 2. \[Deliverable 2\] 3.
\[Deliverable 3\]

Output format: \[Markdown table / test case format / runnable source
code / test plan / checklist / project structure / spreadsheet / other\]

Required fields or files: \[List required columns, sections, file names,
paths, formats, or artifacts\]

Level of detail: \[Concise / standard / detailed\]

Output restrictions: \[Whether explanations, comments, dependencies,
assumptions, or extra files are allowed\]

If information is missing, \[ask clarifying questions / state
assumptions clearly / provide a reusable placeholder\]. Do not fabricate
results, credentials, URLs, or project-specific facts.

## T --- Tone

Use a \[technical / concise / formal / instructional\] tone. Keep the
output \[enterprise-grade / reusable / precise / easy to maintain\],
with consistent terminology and formatting.

------------------------------------------------------------------------

## Optional QA deliverable selectors

Use the relevant selector(s) in the Instructions and Output sections.

### For a test plan

Include objectives, scope, out-of-scope items, test strategy, test
types, environments, test data, entry/exit criteria, risks,
dependencies, roles, schedule, deliverables, and reporting.

### For test cases

Include test case ID, title, requirement/reference, priority,
preconditions, test data, steps, expected result, actual result, status,
and evidence. Include positive, negative, boundary, and role/permission
cases as appropriate.

### For test automation

Specify language, framework, project structure, design pattern, locator
strategy, waits, assertions, setup/teardown, exception handling,
logging, reporting, data management, execution commands, and required
files. Ensure code is consistent and runnable within the stated
environment.

### For defect reporting

Include summary, environment/build, preconditions, reproduction steps,
expected result, actual result, severity, priority, evidence,
reproducibility, and related requirement/test case.

### For QA analysis or review

Include review scope, findings, severity/risk, evidence, impact,
recommendations, assumptions, and unresolved questions.
