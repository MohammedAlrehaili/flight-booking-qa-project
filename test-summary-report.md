# Test Summary Report — Book Flight

| Field | Value |
|---|---|
| **Project** | Book Flight (Agile Travel — `travel.agileway.net`) |
| **Test Cycle** | Version 1.0 |
| **Executed By** | Mohammed Alrehaili |
| **Execution Dates** | 2026-08-16 – 2026-08-17 |
| **Test Management Tool** | Jira + Zephyr Scale |
| **Total Test Cases** | 58 |

## 1. Overall Results

| Result | Count | % of Total |
|---|---|---|
| Pass | 38 | 65.5% |
| Fail | 18 | 31.0% |
| Blocked | 2 | 3.5% |
| **Total** | **58** | **100%** |

Of the 58 test cases executed, 38 passed, confirming that the core "happy path" flows (Login, Select Flight, Passenger Details, and Payment with valid data) work as expected. The 18 failures all fall under negative/invalid-input scenarios and correspond to 18 confirmed defects (BG-1 – BG-18, see [bug-reports/BUG_REPORTS.md](bug-reports/BUG_REPORTS.md)) — mainly missing client-side validation, allowing the user to proceed with invalid or empty required fields.

## 2. Results by Module

| Module | Test Group | Pass | Fail | Blocked | Total |
|---|---|---|---|---|---|
| Login | Valid Login | 4 | 0 | 0 | 4 |
| Login | Invalid Login | 8 | 0 | 0 | 8 |
| Booking a Flight | Valid Select Flight | 9 | 0 | 0 | 9 |
| Booking a Flight | Invalid Select Flight | 0 | 7 | 0 | 7 |
| Booking a Flight | Valid Passenger Details | 5 | 0 | 0 | 5 |
| Booking a Flight | Invalid Passenger Details | 2 | 4 | 1 | 7 |
| Booking a Flight | Valid Payment | 10 | 0 | 0 | 10 |
| Booking a Flight | Invalid Payment | 0 | 7 | 1 | 8 |
| **Total** | | **38** | **18** | **2** | **58** |

**Observations:**

- All "Valid" (positive) test groups passed 100%, so the core booking flow is functionally sound end-to-end.
- The **Invalid Select Flight** group failed completely (7/7) — every negative scenario in flight selection exposed a missing validation (e.g. proceeding without selecting a flight, invalid date combinations).
- **Invalid Passenger Details** and **Invalid Payment** each have a majority of failures, indicating input validation is the weakest area of the application overall.
- **Login** (both valid and invalid cases) is the most stable module, with no failures.

## 3. Results by Priority

| Priority | Pass | Fail | Blocked | Total |
|---|---|---|---|---|
| High | 17 | 16 | 0 | 33 |
| Normal | 11 | 2 | 0 | 13 |
| Low | 10 | 0 | 2 | 12 |
| **Total** | **38** | **18** | **2** | **58** |

16 of the 18 failing test cases are **High priority**, meaning most of the defects found affect core, business-critical validation rules (e.g. mandatory flight selection, mandatory passenger/payment fields) rather than edge cases.

## 4. Blocked Test Cases

Two test cases were marked **Blocked** rather than Pass/Fail:

1. Card number length limit
2. First/Last name maximum length

Both were testing rules that are not documented or explicitly specified anywhere in the application (no stated max length for these fields), so a definitive Pass/Fail verdict couldn't be given without confirming the intended behavior with the product owner. They are recorded here as Blocked to reflect that execution was inconclusive, rather than as a confirmed defect.

## 5. Defect Summary

All 18 Fail results correspond 1:1 to defects logged in Jira (BF-1 – BF-18 / BG-1 – BG-18). The most impactful issues include:

- User can proceed to Passenger Details without selecting a flight.
- User can proceed with invalid or empty required fields on Passenger Details and Payment (no client-side validation).
- Duplicate "Pay now" clicks are not debounced, allowing duplicate submission requests.
- Return date validation gaps (e.g. Return date before Departure date not blocked).
- Concurrency/race-condition testing around the duplicate "Pay now" submission defect, to see if it can result in duplicate bookings or charges.
- Accessibility checks (keyboard navigation, screen reader labels) on the booking form.
- Formal confirmation of undocumented business rules (name/card field length limits) with the product owner, to close out the two Blocked cases.
