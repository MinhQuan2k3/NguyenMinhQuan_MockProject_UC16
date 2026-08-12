# UC20 – Final Test Cases

## 1. Document Information

| Item | Value |
|---|---|
| Use Case | UC20 – Edit Interview Schedule Details |
| Stage | Giai đoạn 1 – Final Test Case |
| Source | Node 6 raw output + Node 7 AI Self-Review + Human Review 3 |
| Status | **Final – Human Reviewed** |
| Version | v1.0 |

## 2. Human Review 3 Decision

The raw Node 6 output contained 25 Test Cases. Human Review 3 was performed against `UC20_clean.md`, the reviewed ambiguity/risk/test-condition artifacts, the raw Node 6 output and Node 7 AI Self-Review.

The final set removes unsupported scenarios, corrects BRL-20-03 scope, removes contradictory Result behavior, removes duplicate UI checks, and replaces fabricated AC/BR identifiers with authoritative UC references.

## 3. Final Test Case Set

| ID | Test Case Title | Precondition | Steps | Expected Result | Priority | Source | Result |
|---|---|---|---|---|---|---|---|
| [UC20]-TC-001 | Verify authorized user can access Edit | User is logged in and has appropriate permission; an interview schedule exists. | 1. Open Interview Schedule List.<br>2. Select Edit for a valid schedule. | Edit is available and the corresponding Edit Interview Schedule screen opens. | P0 | UC20 Overview – Pre-condition/Actor; Basic Flow Step 1 | Untested |
| [UC20]-TC-002 | Verify Edit from List loads the selected schedule | User has appropriate permission; schedule S-01 exists with known current data. | 1. Open Interview Schedule List.<br>2. Select Edit for S-01. | Edit screen displays the current data belonging to S-01. | P0 | UC20 Basic Flow Steps 1–2; Screen Description | Untested |
| [UC20]-TC-003 | Verify Edit from Detail opens the corresponding schedule | User has appropriate permission; user is viewing Detail for S-01. | 1. Select Edit from Interview Schedule Detail. | Edit screen opens for S-01 and displays its corresponding data. | P1 | UC20 Alternative Flow A1 | Untested |
| [UC20]-TC-004 | Verify Edit screen contains documented components | User has opened Edit for a valid schedule. | 1. Inspect module name, breadcrumb, function title, fields, Status, Result and action controls. | All components defined in the Screen Description are present with their documented control types. | P1 | UC20 Screen Description | Untested |
| [UC20]-TC-005 | Verify editable schedule fields can be modified | User is on Edit screen for a valid schedule. | 1. Modify Schedule Title.<br>2. Modify Interviewer.<br>3. Modify Schedule.<br>4. Modify Schedule From/To.<br>5. Modify Location.<br>6. Modify Recruiter Owner. | Each field described as editable accepts modification according to its documented control type. | P0 | UC20 Screen Description refs 4–11 | Untested |
| [UC20]-TC-006 | Verify Assign me control is displayed | User is on Edit screen. | 1. Locate Assign me. | Assign me is displayed using the documented link/button control. | P1 | UC20 Screen Description ref 12 | Untested |
| [UC20]-TC-007 | Verify required-field validation passes when required data is complete | User is on Edit screen; all confirmed required fields are completed. | 1. Keep required fields populated.<br>2. Submit the change. | ME002 “Required field” is not displayed because no required field is missing. | P0 | BRL-20-01; ME002 | Untested |
| [UC20]-TC-008 | Verify ME002 for missing required field | User is on Edit screen; other required fields contain valid data. | 1. Leave a field confirmed as required empty.<br>2. Submit the change. | System displays ME002 “Required field”. | P0 | BRL-20-01; ME002 | Untested |
| [UC20]-TC-009 | Verify only Open Job is available for selection | User is on Edit screen; Job options include Open and non-Open Jobs. | 1. Open Job selection.<br>2. Inspect available Jobs. | Only Job records with Status = Open are available for selection. | P0 | BRL-20-03 | Untested |
| [UC20]-TC-010 | Verify Status is displayed and read-only | User is on Edit screen for a schedule with known Status. | 1. Inspect Status.<br>2. Attempt to edit it. | Current Status is displayed and cannot be edited. | P1 | UC20 Screen Description ref 13 | Untested |
| [UC20]-TC-011 | Verify Result is displayed and editable | User is on Edit screen for a schedule with known Result. | 1. Inspect Result.<br>2. Modify Result. | Current Result is displayed and the control allows editing as documented. No specific Result values are assumed. | P1 | UC20 Screen Description ref 14 | Untested |
| [UC20]-TC-012 | Verify Submit, Cancel and Cancel Schedule controls are displayed | User is on Edit screen. | 1. Inspect the action area. | Submit, Cancel and Cancel Schedule are present as documented buttons. | P1 | UC20 Screen Description refs 15–17 | Untested |
| [UC20]-TC-013 | Verify successful update displays ME014 | User is on Edit screen; valid changes are entered; update succeeds. | 1. Change at least one valid editable value.<br>2. Submit.<br>3. Observe response. | System displays ME014 “Change has been successfully updated”. | P1 | UC20 Screen Description ref 15; ME014 | Untested |
| [UC20]-TC-014 | Verify failed update displays ME013 | User is on Edit screen; valid input is prepared; a controlled update failure is available. | 1. Submit the valid change under the controlled failure condition.<br>2. Observe response. | System displays ME013 “Failed to updated change”. | P1 | UC20 Screen Description ref 15; ME013 | Untested |

## 4. Removed Raw Test Cases

| Raw TC | Decision | Reason |
|---|---|---|
| TC-002 | Remove | Unauthorized/unauthenticated behavior is not specified by UC20. |
| TC-004 | Remove | Invalid/missing schedule identifier is not specified. |
| TC-006 | Remove | Invalid Detail-screen schedule context is not specified. |
| TC-016 | Remove | Incorrectly treats Result as read-only; UC says Result allows editing. |
| TC-017 | Remove | Duplicates Status/Result checks and incorrectly makes Result non-editable. |
| TC-020 | Remove | Incorrectly generalizes BRL-20-03 to Interviewer and Owner. |
| TC-021 | Remove | Same BRL-20-03 scope error. |
| TC-023 | Remove | Duplicates TC-022 button-presence coverage. |

## 5. Corrections / Consolidations

- TC-001: removed invented Manager Role A/B/C; uses documented appropriate permission.
- TC-003 and TC-005: retained with corrected traceability.
- TC-007/008 and TC-009/010/011/012/013/014: consolidated where raw cases duplicated the same approved condition.
- TC-015: retained as Status read-only.
- TC-018/019: retained with corrected `BRL-20-01` trace.
- TC-022: retained as action-button coverage.
- TC-024/025: retained with direct ME014/ME013 trace.

## 6. Traceability Rule

Final Test Cases do **not** use fabricated `AC-20-xx` or `BR-20-xx` identifiers from raw AI output.

Authoritative sources are:

- UC20 Overview – Actor / Pre-condition
- UC20 Basic Flow
- UC20 Alternative Flow – A1
- UC20 Screen Description
- BRL-20-01
- BRL-20-03
- ME002
- ME013
- ME014

## 7. Unresolved Topics Deliberately Not Tested

- invalid/missing schedule;
- authentication failure behavior;
- detailed permission matrix;
- exact required-field list;
- Result allowed values;
- date/time validation;
- Cancel outcome;
- Cancel Schedule outcome;
- Assign Me persistence;
- concurrency.

## 8. Final Metrics

| Metric | Value |
|---|---:|
| Raw Node 6 Test Cases | 25 |
| Raw Test Cases removed | 8 |
| Final Test Cases | 14 |
| AI Self-Review explicit true issues | 3 |
| Additional Human Review issue instances | 9 |
| Final status | **PASS WITH CORRECTIONS** |

The smaller final set is intentional: unsupported, contradictory and duplicate AI-generated cases were removed rather than retained to inflate coverage.
