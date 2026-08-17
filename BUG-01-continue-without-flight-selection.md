# BUG-01: User can proceed to Passenger Details page without selecting a flight

| Field | Value |
|---|---|
| **Module** | Flight Selection |
| **Severity** | High |
| **Priority** | High |
| **Status** | Open |
| **Environment** | Chrome 148, `travel.agileway.net` |
| **Reported by** | Mohammed Alrehaili |
| **Date** | 2026-08-16 |
| **Related test case** | [BF-T77](../test-scenarios/test-cases.md) |

## Summary

Clicking **Continue** with no flight checkbox selected still advances the user to the
Passenger Details page instead of blocking submission with a validation error.

## Steps to Reproduce

1. Navigate to the Select Flight page (`travel.agileway.net/flights/start`).
2. Fill in valid flight search criteria (trip type, origin, destination, and dates).
3. Without checking any flight checkbox in the flight list, click **Continue**.

## Expected Result

The system should display a validation error indicating that a flight must be selected,
and should **not** proceed past the Select Flight page.

## Actual Result

The system proceeds directly to the Passenger Details page with no flight selected and no
validation error shown.

| Before — no flight selected | After — Continue clicked |
|---|---|
| ![Select Flight page with no checkbox selected](../screenshots/BUG-01-before.png) | ![Passenger Details page reached anyway](../screenshots/BUG-01-after.png) |

## Notes

- This directly violates the requirement that a flight selection is mandatory before
  proceeding to Passenger Details.
- Recommend adding a client- and server-side check that blocks submission when zero
  flights are selected.
