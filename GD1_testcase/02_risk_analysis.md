# Business Rules & Risk Analysis

## 1. Document Information

| Item | Value |
|---|---|
| Use Case | UC20 – Edit Interview Schedule Details |
| Stage | Giai đoạn 1 – Business Rules & Risk Analysis |
| Input | `UC20_clean.md` |
| Human Review Input | `01_ambiguity_analysis.md` |
| AI Source | Node 3 – Business Rules + Risk Analysis |
| Output | `02_risk_analysis.md` |
| Status | Human-reviewed baseline |

---

# 2. Purpose

This document records the Business Rule and Risk Analysis for UC20 after Human Review 1.

The objectives are:

1. Extract testable business rules from the Use Case.
2. Identify important functional behaviors derived from the flow and screen description.
3. Assess the risk associated with each important behavior.
4. Preserve traceability from each rule/risk back to the UC.
5. Prevent unresolved or rejected AI assumptions from becoming confirmed requirements.
6. Provide a prioritized input for the Test Condition generation stage.

The Business Rule analysis is based on the requirement baseline and the decisions recorded in `01_ambiguity_analysis.md`.

---

# 3. Risk Assessment Method

Risk is evaluated using two dimensions:

- **Likelihood** – probability that the behavior may fail or be implemented incorrectly.
- **Impact** – consequence if the behavior fails.

The qualitative scale is:

| Level | Meaning |
|---|---|
| Low | Limited effect; unlikely to affect core business behavior |
| Medium | Noticeable functional impact or moderate probability |
| High | Significant functional/business impact or relatively high probability |
| Critical | Failure can cause severe business/data/security consequences |

For prioritization:

```text
Risk Priority = Likelihood × Impact
```

The Node 3 output used qualitative values rather than numeric scores. Therefore this document preserves the qualitative assessment rather than inventing numeric scores that were not produced by the Agent.

---

# 4. Business Rule Inventory

## 4.1 Explicit / Source-supported Business Rules

The following rules are directly supported by the UC or its Screen Description.

| ID | Type | Business Rule | Source / Traceability | Status |
|---|---|---|---|---|
| BR-20-01 | Dependency | User must be logged in and have the appropriate permission before executing the Edit function. | Overview – Pre-condition | EXPLICIT |
| BR-20-02 | Functional | User can select Edit from the Interview Schedule List to begin editing. | Basic Flow – Step 1 | EXPLICIT |
| BR-20-03 | Functional | System loads the information of the selected interview schedule. | Basic Flow – Step 1 | EXPLICIT |
| BR-20-04 | Functional | System displays the Edit Interview Schedule screen with the current schedule data. | Basic Flow – Step 2; Post-condition | EXPLICIT |
| BR-20-05 | Functional | User can open the Edit Interview Schedule screen from the Interview Schedule Detail screen through Edit. | Alternative Flow – A1 | EXPLICIT |
| BR-20-06 | Functional | Schedule Title is editable. | Screen Description – Schedule Title | EXPLICIT |
| BR-20-07 | Functional | Interviewer can be selected through the Interviewer selection control. | Screen Description – Interviewer | EXPLICIT |
| BR-20-08 | Functional | Schedule date is editable. | Screen Description – Schedule | EXPLICIT |
| BR-20-09 | Functional | Schedule From and Schedule To can be entered/edited. | Screen Description – Schedule From / Schedule To | EXPLICIT |
| BR-20-10 | Functional | Location is editable. | Screen Description – Location | EXPLICIT |
| BR-20-11 | Functional | Recruiter Owner can be selected through the Owner selection control. | Screen Description – Recruiter Owner | EXPLICIT |
| BR-20-12 | Functional | The system provides an Assign Me action that assigns the current user. | Screen Description – Assign Me | EXPLICIT |
| BR-20-13 | Functional | The current Status and Result are displayed on the Edit screen. | Screen Description – Status / Result | EXPLICIT |
| BR-20-14 | Functional | The Edit screen provides Submit, Cancel and Cancel Schedule actions. | Screen Description – Buttons | EXPLICIT |
| BR-20-15 | Validation | All required fields must be completed. | BRL-20-01 | EXPLICIT |
| BR-20-16 | Validation | If a required field is not completed, the system displays ME002 – `Required field`. | BRL-20-01; ME002 | EXPLICIT |
| BR-20-17 | Constraint | Only items with Open status are available for selection during editing. | BRL-20-03 | EXPLICIT, scope clarification required |
| BR-20-18 | Validation / Error Handling | ME013 – `Failed to updated change` is displayed when the update fails. | Validation Messages – ME013 | EXPLICIT |
| BR-20-19 | Functional / Result | ME014 – `Change has been successfully updated` is displayed when the update succeeds. | Validation Messages – ME014 | EXPLICIT |

---

# 5. Scope Clarification for BR-20-17

The Node 3 Agent interpreted the `Open`-status rule broadly as applying to an unspecified `item`.

Human Review 1 explicitly rejected that broad interpretation.

The authoritative business rule is:

> BRL-20-03 applies to **Job with Open status**.

Therefore:

```text
BR-20-17
Object = Job
Allowed status = Open
```

It must **not** automatically be interpreted as:

```text
Interviewer = Open
Recruiter Owner = Open
Interview Schedule = Open
```

The Job field itself was identified as a Human Review finding because BRL-20-03 references Job while the original Screen Description did not clearly contain a Job field.

### Test Design Impact

The next stage should test the confirmed rule:

- Open Job is available for selection.

It should not create unsupported tests for unrelated objects.

---

# 6. Derived / Flow-based Rules

Some behaviors are not written as formal Business Rules but are required to make the documented flow meaningful.

These are marked as **DERIVED**, not EXPLICIT.

| ID | Type | Derived Rule | Traceability | Classification |
|---|---|---|---|---|
| DR-20-01 | Flow | The Edit operation must identify the interview schedule associated with the user's Edit action. | Basic Flow – Step 1 | DERIVED |
| DR-20-02 | Flow | After opening the Edit screen, the current schedule data is used as the basis for editing. | Basic Flow – Step 2 | DERIVED |
| DR-20-03 | Flow | Submit must initiate the update process for the edited schedule. | Submit + ME013/ME014 | DERIVED |
| DR-20-04 | Flow | Successful update must correspond to ME014. | ME014 | DERIVED |
| DR-20-05 | Flow | Failed update must correspond to ME013. | ME013 | DERIVED |
| DR-20-06 | Flow | Required-field validation must occur before a successful update can be completed. | BRL-20-01 + Submit | DERIVED |

These derived rules are acceptable for test-condition generation because they are directly supported by the relationship between the documented UI controls, messages and business rules.

---

# 7. Rules That Must NOT Be Treated as Confirmed

The Node 3 output contains several statements explicitly marked `[SUY LUẬN]`. These must not be treated as authoritative requirements.

## 7.1 BR-20-20 – Schedule Identification

Node 3 proposed:

> System must correctly identify the interview schedule to edit.

This is a reasonable derived behavior, but it should remain **DERIVED**, not a new formal business rule.

---

## 7.2 BR-20-21 – Submit Causes Update

Node 3 proposed that clicking Submit must perform the update so that ME013/ME014 have meaning.

This is a reasonable flow derivation, but it should remain:

```text
DERIVED
```

and should not be converted into a new official `BRL-20-xx` requirement without BA confirmation.

---

## 7.3 BR-20-22 – Status and Result Read-only

The Node 3 Agent proposed that fields not described as editable, including Status and Result, should be treated as display-only.

This interpretation is **not accepted as written**.

Human Review 1 established:

- Status is explicitly read-only.
- Result is described as editable, but its allowed values and validation are unclear.

Therefore:

| Field | Decision |
|---|---|
| Status | Read-only |
| Result | Editable according to current UC description |
| Result validation | Unconfirmed |
| Result allowed values | Unconfirmed |

This correction is important before Test Condition generation.

---

# 8. Risk Analysis

## 8.1 AC / Behavior Risk Assessment

The Node 3 Agent assessed the following behaviors.

| ID | Behavior / AC | Likelihood | Impact | Risk | Rationale |
|---|---|---|---|---|---|
| AC-20-01 | User selects Edit from Interview Schedule List and system loads the schedule. | Medium | High | Medium | Incorrect schedule/context mapping may open the wrong record or prevent editing. |
| AC-20-02 | Edit screen displays current schedule data. | Medium | High | Medium | This is core Edit functionality; failure can result in incorrect or incomplete editing data. |
| AC-20-03 | User can open Edit from Interview Schedule Detail. | Medium | Medium | Medium | Alternative Flow does not clearly define where it rejoins the main flow. |
| AC-20-04 | User with appropriate permission can use Edit. | High | High | High | Permission is not fully defined. Incorrect authorization may allow unauthorized modification or block legitimate users. |
| AC-20-05 | Editable schedule fields can be modified. | Medium | High | Medium | Fields are identified as editable, but detailed validation/format rules are incomplete. |
| AC-20-06 | Interviewer and Owner can be selected through their controls. | High | High | High | Selection behavior and data-source rules are incomplete. |
| AC-20-07 | Assign Me assigns the current user correctly. | High | Medium | Medium | It is unclear exactly which owner field is affected and when the change is persisted. |
| AC-20-08 | Status and Result are displayed. | Medium | Medium | Medium | Display behavior is defined, but Result behavior and values are incomplete. |
| AC-20-09 | Submit, Cancel and Cancel Schedule are available. | Medium | Medium | Medium | Presence is defined, but behavior of Cancel Schedule is insufficiently specified. |
| AC-20-10 | Edit screen opens with current data. | Medium | Medium | Medium | Current Post-condition is inconsistent with the complete update scope of UC20. |
| AC-20-11 | Successful Submit produces ME014. | High | High | High | Successful update is a core business result but the original flow does not explicitly describe it. |
| AC-20-12 | Failed update produces ME013. | High | High | High | Incorrect failure handling can cause users to believe changes were saved when they were not. |
| AC-20-13 | Required fields must be completed. | High | High | High | Missing validation can create incomplete interview schedules. |
| AC-20-14 | Missing required field produces ME002. | High | Medium | Medium | Message exists, but exact display and validation behavior are unclear. |
| AC-20-15 | Only Open items are available for selection. | High | High | High | Incorrect filtering could allow an invalid Job or hide valid selectable data. |

The above risk assessments are taken from the Node 3 output. 

---

# 9. Risk Priority Summary

Based on the available Node 3 analysis:

## High Risk

The following areas should receive priority during Test Condition generation:

1. **Permission / authorization**
2. **Interviewer and Owner selection**
3. **Successful update / ME014**
4. **Failed update / ME013**
5. **Required-field enforcement**
6. **Job/Open-status filtering**
7. **Correct update context / selected schedule**

These areas combine significant business impact with meaningful uncertainty in the current specification. 

## Medium Risk

The following areas have moderate priority:

1. Opening Edit from Detail.
2. Editable schedule fields.
3. Assign Me.
4. Status/Result display.
5. Cancel / Cancel Schedule presence.
6. Initial Edit screen loading.

---

# 10. Risk Areas Added by Human Review

The Human Review identified several issues that should be carried into Risk Analysis even though they were not completely captured by the Node 3 output.

| Risk ID | Human Finding | Risk | Priority |
|---|---|---|---|
| HR-R01 | Job referenced by BRL-20-03 but missing/unclear in Screen Description | BRL-20-03 may not be testable or may be implemented against the wrong UI component | High |
| HR-R02 | Required fields are not explicitly identified | Positive/negative validation coverage may be incomplete | High |
| HR-R03 | Result values and validation are unspecified | Invalid or inconsistent Result values may be accepted | High |
| HR-R04 | Status-dependent editability is unclear | Users may edit schedules in an invalid state or be incorrectly blocked | High |
| HR-R05 | Assign Me persistence is unclear | Assignment may be lost or persisted unexpectedly | Medium |
| HR-R06 | Cancel Schedule behavior is unspecified | Schedule state may be changed incorrectly or unexpectedly | Medium |
| HR-R07 | Date/time validation is unspecified | Invalid schedule dates/times may be accepted | Medium |
| HR-R08 | Permission matrix is unspecified | Unauthorized or incorrectly blocked updates | High |

These findings originate from Human Review 1 and should not be represented as AI findings. 

---

# 11. Unresolved / Deferred Requirements

The following topics must remain clearly separated from confirmed business rules.

| Topic | Status | Test Condition Treatment |
|---|---|---|
| Exact permission matrix | UNCONFIRMED | Do not invent role-specific rules |
| Existing Job becomes non-Open after selection | OUT OF SCOPE / UNCONFIRMED | Do not require a test condition |
| Combobox search behavior | UNCONFIRMED | Do not assume search |
| Combobox single/multi-select | UNCONFIRMED | Do not assume multi-select |
| Empty combobox behavior | UNCONFIRMED | Do not invent expected behavior |
| Past-date restriction | UNCONFIRMED | Do not assume invalid |
| Schedule overlap | UNCONFIRMED | Do not assume validation |
| Timezone | UNCONFIRMED | Do not invent timezone behavior |
| Load failure | OUT OF SCOPE unless separately required | Do not automatically create test case |
| Concurrent update | OUT OF SCOPE | Do not create concurrency test |
| Cancel confirmation | UNCONFIRMED | Do not assume confirmation dialog |
| Cancel Schedule resulting status | UNCONFIRMED | Do not assume resulting status |
| Result allowed values | UNCONFIRMED | Requires clarification |
| Status-dependent editability | UNCONFIRMED | Requires clarification |
| BRL-20-02 | REJECTED | No test condition |

These classifications follow the Human Review decisions. 

---

# 12. AI Overreach Controls

The following controls must be applied when this document is used by the next Node.

### Control 1 – No BRL-20-02

The absence of BRL-20-02 is not evidence that the requirement is missing.

The numbering gap was explicitly rejected during Human Review 1.

### Control 2 – BRL-20-03 = Job

`Open` status filtering applies to **Job**.

It must not be generalized to Interviewer, Owner or Schedule.

### Control 3 – Result is not automatically read-only

Status is read-only.

Result remains an editable field according to the current requirement baseline, although its validation and allowed values are unresolved.

### Control 4 – Do not turn QA questions into requirements

The following remain questions rather than requirements:

- past date;
- overlapping schedule;
- timezone;
- concurrent update;
- load failure;
- Cancel confirmation.

---

# 13. Traceability Matrix

| Business Rule / Risk | Source | Next-stage Use |
|---|---|---|
| BR-20-01 | BRL-20-01 | Required-field test conditions |
| BR-20-03 | BRL-20-03 | Job/Open-status test conditions |
| BR-20-15 | BRL-20-01 | Validation conditions |
| BR-20-16 | ME002 | Validation/error conditions |
| BR-20-18 | ME013 | Update-failure condition |
| BR-20-19 | ME014 | Update-success condition |
| DR-20-01 | Basic Flow | Schedule identification condition |
| DR-20-03 | Submit + ME013/ME014 | Update condition |
| DR-20-06 | BRL-20-01 + Submit | Validation-before-update condition |
| HR-R01 | Human Finding H-01 | Job selection coverage |
| HR-R02 | Human Finding H-02 / #9 | Required-field coverage |
| HR-R03 | Human Finding H-02 | Result coverage |
| HR-R04 | Human Finding H-04 | Status-condition coverage |
| HR-R05 | Finding #14 | Assign Me coverage |
| HR-R06 | Finding #8 | Cancel Schedule coverage |
| HR-R07 | Finding #16 | Deferred unless confirmed |
| HR-R08 | Finding #2 | Deferred unless permission requirements confirmed |

---

# 14. Recommended Test-Condition Priorities

Based on the risk analysis, the next stage should prioritize conditions in this order.

## Priority 1 – Core Update Integrity

```text
1. Valid Edit data
2. Submit
3. Required-field validation
4. Successful update → ME014
5. Failed update → ME013
```

## Priority 2 – Business Constraints

```text
6. Job selection
7. Only Open Job available
8. Correct interview schedule loaded
9. Permission / authorized actor
```

## Priority 3 – Field Behavior

```text
10. Schedule Title
11. Interviewer
12. Schedule
13. Schedule From
14. Schedule To
15. Location
16. Recruiter Owner
17. Assign Me
```

## Priority 4 – Navigation / Secondary Actions

```text
18. Entry from Interview Schedule List
19. Entry from Interview Schedule Detail
20. Cancel
21. Cancel Schedule
```

Items whose business rules remain unresolved should be explicitly marked as **Clarification Required** rather than tested using invented expected results.

---

# 15. Limitations of Node 3 Output

The Node 3 execution completed with:

```text
finish_reason = length
```

and:

```text
completion_tokens = 2500
```

Therefore, the original AI output was truncated before the complete Risk Analysis could be emitted.

Consequently:

- The Business Rule section available from the output has been retained.
- The available Risk Analysis entries have been retained.
- Missing rows have **not** been invented.
- Human Review findings have been incorporated separately.
- The final document should be treated as a **human-curated risk baseline**, not a verbatim copy of an uninterrupted AI output.

This limitation should be retained as evidence of the current Node 3 configuration.

---

# 16. Final Assessment

Node 3 successfully identified the major risk areas of UC20, particularly:

- authorization;
- schedule loading;
- editable schedule data;
- selection controls;
- Submit/update;
- required-field validation;
- ME013 / ME014;
- Open-status selection.

The most important correction from Human Review is that the AI output must not be accepted blindly.

In particular:

1. `BRL-20-03` is specifically about **Job with Open status**.
2. `BRL-20-02` must not be invented.
3. `Result` must not be classified as read-only merely because it is represented by a label in the source.
4. Unconfirmed date/time, concurrency, load-failure and Cancel behavior must remain unresolved.
5. Human findings H-01 through H-04 must be preserved as separate evidence.

The resulting risk baseline is sufficiently structured to proceed to the next stage: **Test Condition generation**.