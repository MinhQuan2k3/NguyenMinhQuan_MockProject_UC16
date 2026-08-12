# AI Self-Review & Human Review Log

## 1. Purpose

This document records the comparison between Node 7 AI Self-Review and the Human Review performed after it.

The objective is to measure whether AI Self-Review can replace Human Review.

## 2. Baseline

| Metric | Value |
|---|---:|
| Node 6 raw Test Cases | 25 |
| Node 7 AI Self-Review | Completed |
| Human Review 3 | Completed |
| Final Test Cases | 14 |

## 3. AI Self-Review Findings

Node 7 explicitly identified **3 genuine hallucination issues**:

| ID | Test Case | Finding | Human Decision |
|---|---|---|---|
| AI-01 | TC-002 | Unauthorized/unauthenticated behavior is not specified by UC20. | Confirmed – remove |
| AI-02 | TC-004 | Invalid/missing schedule identifier is not specified. | Confirmed – remove |
| AI-03 | TC-006 | Invalid/missing Detail schedule context is not specified. | Confirmed – remove |

Node 7 also correctly noted that TC-024 and TC-025 have support from ME014/ME013, although the Submit/update flow is incompletely described.

## 4. Additional Human Review Findings

| ID | Test Case(s) | Human Finding | Decision |
|---|---|---|---|
| HR3-01 | TC-001 | Invented Manager Role A/B/C granularity not established by the approved UC baseline. | Rewrite |
| HR3-02 | TC-016 | Result was treated as read-only, contradicting the Screen Description. | Remove |
| HR3-03 | TC-017 | Duplicate Status/Result coverage and incorrectly makes Result non-editable. | Remove |
| HR3-04 | TC-020 | BRL-20-03 incorrectly applied to Interviewer/Owner. | Remove |
| HR3-05 | TC-021 | Same BRL-20-03 scope error. | Remove |
| HR3-06 | TC-022/TC-023 | Duplicate button coverage. | Consolidate |
| HR3-07 | Most raw TCs | Fabricated `AC-20-xx` / `BR-20-xx` identifiers used as Sources. | Correct |
| HR3-08 | TC-018/TC-019 | `BR-20-01` should be `BRL-20-01`. | Correct |
| HR3-09 | TC-024/TC-025 | Trace directly to ME014/ME013 instead of inferred AC/BR IDs. | Correct |

## 5. AI vs Human Detection

### AI Self-Review

**3 true issues explicitly found.**

All three were confirmed by Human Review.

### Human Review

Human Review identified **9 additional issue instances** beyond the three explicit AI findings.

The additional issues include wrong Result editability, wrong BRL-20-03 scope, invented role granularity, duplicate cases, and widespread traceability problems.

### False positives

No major false positive was found among the three explicit AI hallucination findings.

## 6. Traceability Review

The most significant issue missed by AI Self-Review was traceability.

Raw Test Cases repeatedly used:

- `AC-20-01` … `AC-20-11`
- `BR-20-01`
- `BR-20-04` … `BR-20-16`

These are not authoritative identifiers in UC20. The UC contains `BRL-20-01` and `BRL-20-03`, together with Basic Flow, Alternative Flow, Screen Description and Validation Messages.

Human Review therefore replaced fabricated identifiers with direct source references.

## 7. Coverage / Quality Review

Human Review also identified:

- Result incorrectly tested as read-only;
- BRL-20-03 applied to the wrong UI objects;
- duplicate UI/button cases;
- unresolved requirements converted into concrete behavior.

The final artifact preserves unresolved requirements instead of inventing expected behavior.

## 8. Change Log

| Metric | Value |
|---|---:|
| Raw Test Cases | 25 |
| Removed | 8 |
| Final | 14 |
| AI true issues | 3 |
| Additional Human issue instances | 9 |
| Confirmed AI false positives | 0 |

“Issue instances” and “Test Cases removed” are deliberately separate metrics.


## 9. Final Decision

**PASS WITH CORRECTIONS**

The final 14 Test Cases are approved.

Raw Node 6 and Node 7 outputs should be preserved separately as evidence and should not be overwritten.
