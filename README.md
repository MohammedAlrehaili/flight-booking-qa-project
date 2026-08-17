# Book Flight — QA Test Project

A manual QA project testing the flight booking flow of **Agile Travel** (`travel.agileway.net`), a public demo travel booking application. This repo documents the full testing process — test design, execution, and defect reporting — using **Jira + Zephyr Scale** for test case management and test execution tracking.

## About the Application Under Test

Agile Travel is a demo flight booking site covering the flow: **Login → Select Flight → Passenger Details → Payment → Confirmation**. This project focuses on manually testing that flow end-to-end, with an emphasis on input validation and business rule coverage.

## What's in This Repo

| File / Folder | Description |
|---|---|
| [`test-scenarios/Book_Flight_Test_Cases.xlsx`](test-scenarios/Book_Flight_Test_Cases.xlsx) | 58 test cases (positive, negative, edge case) across Login, Select Flight, Passenger Details, and Payment, prioritized High/Normal/Low |
| [`bug-reports/BUG_REPORTS.md`](bug-reports/BUG_REPORTS.md) | 18 defects found during execution, each with steps to reproduce, expected result, and actual result |
| [`bug-reports/screenshots/`](bug-reports/screenshots/) | Supporting screenshots referenced in the bug reports |
| [`test-summary-report.md`](test-summary-report.md) | Execution summary: pass/fail/blocked results, breakdown by module and priority, and next steps |

## Tools & Techniques Used

- Manual, black-box functional testing
- Jira + Zephyr Scale for test case management and execution tracking
- Positive, negative, and edge-case test design
- Risk-based prioritization (High / Normal / Low)
- Formal bug reporting with severity/priority and reproduction steps
- Chrome DevTools (Network tab) used as supporting evidence for a defect

## Results at a Glance

| Metric | Result |
|---|---|
| Test cases executed | 58 |
| Pass | 38 (65.5%) |
| Fail | 18 (31.0%) |
| Blocked | 2 (3.5%) |
| Defects logged | 18 |

Full breakdown by module and priority is in [`test-summary-report.md`](test-summary-report.md).

## Key Defects Found

- User can proceed to Passenger Details without selecting a flight.
- Passenger Details and Payment forms accept submission with missing/invalid required fields (no client-side validation).
- Duplicate "Pay now" clicks are not debounced, sending duplicate confirmation requests.
- Return date is not validated against the Departure date.

See [`bug-reports/BUG_REPORTS.md`](bug-reports/BUG_REPORTS.md) for the complete list.

## What This Project Demonstrates

- Designing structured test scenarios from business requirements (positive, negative, and edge cases)
- Prioritizing test coverage by risk
- Executing manual test cases and tracking results in a real test management tool
- Writing clear, reproducible bug reports
- Distinguishing confirmed defects from unverified assumptions, and knowing when to flag something as inconclusive rather than guess

