# Week 02 — Boundary Value Analysis, Equivalence Partitioning and Defect Lifecycle

## Session summary

This review covered three manual-testing topics: Boundary Value Analysis (BVA), Equivalence Partitioning (EP), and defect lifecycle management. The examples use numeric input ranges from café ordering and gaming lounge booking systems.

## 1. Boundary Value Analysis (BVA)

BVA is a black-box test design technique that selects values at and immediately around the boundaries of an input range. Boundary defects are common because of incorrect comparison operators, off-by-one errors, and incorrect range checks.

For an inclusive range from minimum (min) to maximum (max), the common six-value boundary set is:

- (min - 1): immediately below the minimum — invalid.
- (min): minimum — valid.
- (min + 1): immediately above the minimum — valid.
- (max - 1): immediately below the maximum — valid.
- (max): maximum — valid.
- (max + 1): immediately above the maximum — invalid.

### Example: gaming lounge booking

The system accepts bookings from 1 to 10 hours, inclusive.

| Test value | Expected result | Reason |
|---:|---|---|
| 0 | Reject | Below minimum |
| 1 | Accept | Minimum boundary |
| 2 | Accept | Just above minimum |
| 9 | Accept | Just below maximum |
| 10 | Accept | Maximum boundary |
| 11 | Reject | Above maximum |

A nominal value such as 5 can be useful for general functional coverage, but it does not replace the six boundary checks in this six-value model.

## 2. Equivalence Partitioning (EP)

EP is a black-box test design technique that divides an input domain into groups (equivalence partitions) expected to produce the same system behavior. A representative value is selected from each partition to reduce redundant tests.

### Example: gaming lounge booking

Accepted booking duration: 1–8 hours, inclusive.

| Partition | Input range | Representative | Expected result |
|---|---|---:|---|
| Invalid — below minimum | Less than 1 | 0 | Reject |
| Valid | 1–8 | 4 | Accept |
| Invalid — above maximum | Greater than 8 | 9 | Reject |

Do not split a valid partition into smaller groups unless the application is expected to behave differently within those groups.

## 3. EP vs BVA

| Technique | Main focus | Test-data selection |
|---|---|---|
| EP | Groups of inputs expected to behave alike | One representative from each partition |
| BVA | Edges of ordered input partitions | Values at and immediately around boundaries |

A practical sequence is to identify the equivalence partitions first, then apply BVA to the boundaries of ordered partitions.

## 4. Defect lifecycle

A common simplified defect workflow is:

**New → Assigned → Fixed → Retest → Closed**

- **New:** Tester reports the defect with reproducible details.
- **Assigned:** The defect is assigned to a responsible developer or team member.
- **Fixed:** The developer implements a correction.
- **Retest:** The tester executes the relevant test again to verify the correction.
- **Closed:** The tester confirms the defect is resolved and closes it.

If the defect still occurs during retesting, it should be **Reopened** and returned for further investigation and correction:

**Retest → Reopened → Assigned → Fixed → Retest**

The tester should preserve clear reproduction steps, test data, expected result, actual result, and supporting evidence. A displayed error message does not make a test pass if the application still performs a prohibited action.

## 5. Expected result vs actual result

A test fails when the observed behavior does not match the expected behavior, including when the system performs an unintended side effect.

### Example: invalid café order quantity

- Input: quantity 0.
- Expected result: display an appropriate validation message and do not create an order.
- Actual result: display the validation message but create the order.
- Status: **Fail**.

The error message alone is insufficient because the prohibited order creation still occurred.

## 6. Corrections reinforced in this review

- BVA requires individual boundary test values, not broad ranges.
- For an inclusive range of 1–10, the six values are 0, 1, 2, 9, 10, and 11.
- EP partitions should reflect different expected system behavior; avoid arbitrary subdivisions.
- The developer fixes a defect before the tester retests it.
- A failed retest results in reopening the defect, not closing it.
- For a password range of 6–12 characters, the six boundary values are 5, 6, 7, 11, 12, and 13.

## Scope note

This document records the concepts and corrections covered in the study session. It does not claim that a real application was tested or that any Jira issue was created.
