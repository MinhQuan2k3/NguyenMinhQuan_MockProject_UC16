\# UC20: Edit interview details



\---



\## Overview



| Item | Description |

|------|-------------|

| Use Case ID | UC20 |

| Use Case Name | Edit Interview Schedule Details |

| System | HRU System |

| Actor | Manager Role A, Manager Role B, Manager Role C |

| Trigger | User clicks the Edit action from the Interview Schedule screen. |

| Pre-condition | User has logged into the system with appropriate permission. |

| Post-condition | System displays the Edit Interview Schedule screen. |



\---



\## Basic Flow



| Step | Actor | Action | Next |

|------|------|--------|------|

| 1 | User | Select the Edit action from the Interview Schedule List. | System loads interview schedule information. |

| 2 | System | Display the Edit Interview Schedule screen with current data. | End |



\---



\## Alternative Flow



| Step | Actor | Action | Next |

|------|------|--------|------|

| A1 | User | Click Edit from the Interview Schedule Detail screen. | System opens the Edit Interview Schedule screen. |



\---



\## Screen Components



| Ref | Component ID | Control Type | Data Type | Description |

|----|---------------|--------------|-----------|-------------|

| 1 | LabelA | Label | N/A | Module name |

| 2 | BreadcrumbA | Breadcrumb | N/A | Sub-module name |

| 3 | LabelB | Label | N/A | Function title |

| 4 | TextboxA | Textbox | Text | Editable schedule title |

| 5 | ComboboxA | Combobox | Text | Interviewer Selection |

| 6 | DatePickerA | Date | Date | Editable schedule date |

| 7 | TimePickerA | Time | Time | Schedule start time |

| 8 | TimePickerB | Time | Time | Schedule end time |

| 9 | TextboxB | Textbox | Text | Editable location |

|10 | ComboboxB | Combobox | Text | Owner selection |

|11 | LinkButtonA | Link | N/A | Assign current user |

|12 | LabelC | Label | Text | Display status |

|13 | LabelD | Label | Text | Display result |

|14 | ButtonA | Button | N/A | Submit |

|15 | ButtonB | Button | N/A | Cancel |

|16 | ButtonC | Button | N/A | Cancel Schedule |



\---



\## Business Rules



| Rule ID | Description |

|---------|-------------|

| BRL-20-01 | User must complete all required fields. Otherwise display validation message ME002: "Required field". |

| BRL-20-03 | Only items with Open status are available for selection while editing. |



\---



\## Validation Messages



| Code | Message |

|------|---------|

| ME002 | Required field |

| ME013 | Failed to update change |

| ME014 | Change has been successfully updated |



\---



\## Notes



\- Mockup images have been removed.

\- Internal URLs have been replaced.

\- Internal naming has been generalized.

\- No credential, token or internal information is included.

