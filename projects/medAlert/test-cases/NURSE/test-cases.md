## TC-001 -  Nurse saves valid patient vital signs

| Field | Detail |
|---|---|
| Feature | Record patient health data |
| Technique | Happy path |
| Severity | Critical |
| Preconditions | Camila Duarte, password `senha123`, is logged in as nurse; the patient is under her responsibility. |

**Steps:** 1. Open an assigned patient's health record. 2. Enter heart rate `72 bpm`, SpO2 `98%`, temperature `36.8 °C`, and systolic blood pressure `120 mmHg`. 3. Save the health record.

**Expected result:** A success alert confirms that the patient health data was saved.

**Review:** Kept

---

## TC-002 - Nurse records heart rate at the lower normal boundary

| Field | Detail |
|---|---|
| Feature | Heart rate threshold |
| Technique | Boundary |
| Severity | High |
| Preconditions | Camila Duarte is logged in and viewing an assigned patient. |

**Steps:** 1. Enter heart rate `50 bpm`, SpO2 `98%`, temperature `36.8 °C`, and systolic blood pressure `120 mmHg`. 2. Save the record.

**Expected result:** The heart rate record is saved without a HIGH heart-rate alert.

**Review:** Kept

---

## TC-003 - Nurse records heart rate below the lower boundary

| Field | Detail |
|---|---|
| Feature | Heart rate threshold |
| Technique | Boundary |
| Severity | High |
| Preconditions | Camila Duarte is logged in and viewing an assigned patient. |

**Steps:** 1. Enter heart rate `49 bpm`, SpO2 `98%`, temperature `36.8 °C`, and systolic blood pressure `120 mmHg`. 2. Save the record.

**Expected result:** A HIGH heart-rate alert is created with status `Pending`.

**Review:** Kept

---

## TC-004 - Nurse records heart rate at 99 bpm

| Field | Detail |
|---|---|
| Feature | Heart rate threshold |
| Technique | Boundary |
| Severity | Medium |
| Preconditions | Camila Duarte is logged in and viewing an assigned patient. |

**Steps:** 1. Enter heart rate `99 bpm`, SpO2 `98%`, temperature `36.8 °C`, and systolic blood pressure `120 mmHg`. 2. Save the record.

**Expected result:** The heart rate record is saved without a HIGH heart-rate alert.

**Review:** Kept

---

## TC-005 - Nurse records heart rate at 100 bpm

| Field | Detail |
|---|---|
| Feature | Heart rate threshold |
| Technique | Boundary |
| Severity | High |
| Preconditions | Camila Duarte is logged in and viewing an assigned patient. |

**Steps:** 1. Enter heart rate `100 bpm`, SpO2 `98%`, temperature `36.8 °C`, and systolic blood pressure `120 mmHg`. 2. Save the record.

**Expected result:** The system's behavior matches the team-confirmed interpretation of the conflicting heart-rate rules.

**Review:** Kept

---

## TC-006 - Nurse records oxygen saturation at 95%

| Field | Detail |
|---|---|
| Feature | Oxygen saturation threshold |
| Technique | Boundary |
| Severity | Critical |
| Preconditions | Camila Duarte is logged in and viewing an assigned patient. |

**Steps:** 1. Enter heart rate `72 bpm`, SpO2 `95%`, temperature `36.8 °C`, and systolic blood pressure `120 mmHg`. 2. Save the record.

**Expected result:** The oxygen saturation record is saved without a CRITICAL oxygen alert.

**Review:** Kept

---

## TC-007 - Nurse records oxygen saturation below 95%

| Field | Detail |
|---|---|
| Feature | Oxygen saturation threshold |
| Technique | Boundary |
| Severity | Critical |
| Preconditions | Camila Duarte is logged in and viewing an assigned patient. |

**Steps:** 1. Enter heart rate `72 bpm`, SpO2 `94%`, temperature `36.8 °C`, and systolic blood pressure `120 mmHg`. 2. Save the record.

**Expected result:** A CRITICAL oxygen saturation alert is created with status `Pending`.

**Review:** Kept

---

## TC-008 - Nurse records temperature at 37.7 °C

| Field | Detail |
|---|---|
| Feature | Body temperature threshold |
| Technique | Boundary |
| Severity | High |
| Preconditions | Camila Duarte is logged in and viewing an assigned patient. |

**Steps:** 1. Enter heart rate `72 bpm`, SpO2 `98%`, temperature `37.7 °C`, and systolic blood pressure `120 mmHg`. 2. Save the record.

**Expected result:** The temperature record is saved without a HIGH temperature alert.

**Review:** Kept

---

## TC-009 - Nurse records temperature at 37.8 °C

| Field | Detail |
|---|---|
| Feature | Body temperature threshold |
| Technique | Boundary |
| Severity | High |
| Preconditions | Camila Duarte is logged in and viewing an assigned patient. |

**Steps:** 1. Enter heart rate `72 bpm`, SpO2 `98%`, temperature `37.8 °C`, and systolic blood pressure `120 mmHg`. 2. Save the record.

**Expected result:** A HIGH temperature alert is created with status `Pending`.

**Review:** Kept

---

## TC-010 - Nurse records systolic blood pressure at 139 mmHg

| Field | Detail |
|---|---|
| Feature | Systolic blood pressure threshold |
| Technique | Boundary |
| Severity | Medium |
| Preconditions | Camila Duarte is logged in and viewing an assigned patient. |

**Steps:** 1. Enter heart rate `72 bpm`, SpO2 `98%`, temperature `36.8 °C`, and systolic blood pressure `139 mmHg`. 2. Save the record.

**Expected result:** The blood pressure record is saved without a MEDIUM systolic blood pressure alert.

**Review:** Kept
---

## TC-011 - Nurse records systolic blood pressure at 140 mmHg

| Field | Detail |
|---|---|
| Feature | Systolic blood pressure threshold |
| Technique | Boundary |
| Severity | Medium |
| Preconditions | Camila Duarte is logged in and viewing an assigned patient. |

**Steps:** 1. Enter heart rate `72 bpm`, SpO2 `98%`, temperature `36.8 °C`, and systolic blood pressure `140 mmHg`. 2. Save the record.

**Expected result:** A MEDIUM systolic blood pressure alert is created with status `Pending`.

**Review:** Kept

---

## TC-012 - Save is rejected when heart rate is missing

| Field | Detail |
|---|---|
| Feature | Vital sign validation |
| Technique | Partitioning |
| Severity | High |
| Preconditions | Camila Duarte is logged in and viewing an assigned patient. |

**Steps:** 1. Enter valid SpO2, temperature, and systolic blood pressure values. 2. Leave heart rate empty. 3. Save the record.

**Expected result:** The record is not saved and a heart-rate validation message is displayed.

**Review:** Kept

---

## TC-013 - Save is rejected when heart rate is nonnumeric

| Field | Detail |
|---|---|
| Feature | Vital sign validation |
| Technique | Invalid input |
| Severity | High |
| Preconditions | Camila Duarte is logged in and viewing an assigned patient. |

**Steps:** 1. Try to enter `not-a-number` in the heart-rate field. 2. Enter valid values in the remaining fields. 3. Save the record.

**Expected result:** The record is not saved and a heart-rate validation message is displayed.

**Review:** Edited (it`s not possible to type letters, only numbers)

---

## TC-014 - Save is rejected when SpO2 is negative

| Field | Detail |
|---|---|
| Feature | Vital sign validation |
| Technique | Invalid input |
| Severity | High |
| Preconditions | Camila Duarte is logged in and viewing an assigned patient. |

**Steps:** 1. Enter `-1` for SpO2. 2. Enter valid values in the remaining fields. 3. Save the record.

**Expected result:** The record is not saved and an SpO2 validation message is displayed.

**Review:** Kept -> The record was saved with -1 for SpO2
---

## TC-015 - Responsible nurse records assigned patient data

| Field | Detail |
|---|---|
| Feature | Nurse permission |
| Technique | Permission |
| Severity | Critical |
| Preconditions | Patient assignments are known; Camila Duarte is logged in and responsible for the selected patient. |

**Steps:** 1. Open the assigned patient's health record. 2. Enter valid values for all four vital signs. 3. Save the record.

**Expected result:** The health record is saved and the success alert is displayed.

**Review:** Kept

---

## TC-016 - Nurse cannot record data for an unassigned patient

| Field | Detail |
|---|---|
| Feature | Nurse permission |
| Technique | Permission |
| Severity | Critical |
| Preconditions | Patient assignments are known; Camila Duarte is logged in and not responsible for the selected patient. |

**Steps:** 1. Attempt to open or directly submit a vital-sign record for the unassigned patient through the UI or `/api/...` endpoint.

**Expected result:** Access is denied and no vital-sign record is saved.

**Review:** Kept -> it allowed to send other patient data logged as Camila Duarte, showing to Paulo Ferreira , i.e, data that he did not send

---

## TC-017 - Patient cannot record another patient's health data

| Field | Detail |
|---|---|
| Feature | Patient permission |
| Technique | Permission |
| Severity | Critical |
| Preconditions | Marina Souza is logged in. |

**Steps:** 1. Attempt to open Roberto Lima's health-record form or submit vital-sign data for Roberto through the UI or an `/api/...` endpoint.

**Expected result:** Access is denied and no health record is saved.

**Review:** Kept -> it allowed to see other patient data using other one as logged, just by changing patient id on the endpoint

---

## TC-018 - Patient cannot record their own vital signs

| Field | Detail |
|---|---|
| Feature | Patient permission |
| Technique | Permission |
| Severity | Critical |
| Preconditions | Marina Souza is logged in. |

**Steps:** 1. Attempt to open the vital-sign recording form or call the clinical recording endpoint.

**Expected result:** Access is denied and no vital-sign record is saved.

**Review:** Kept

---

## TC-019 - Doctor cannot record vital signs

| Field | Detail |
|---|---|
| Feature | Doctor permission |
| Technique | Permission |
| Severity | Critical |
| Preconditions | Dra. Helena Prado is logged in. |

**Steps:** 1. Attempt to open the vital-sign recording form or call the clinical recording endpoint.

**Expected result:** Access is denied and no vital-sign record is saved.

**Review:** Kept -> It's not possible from the UI after login but from the API it's possible using the doctor cookie hash

---

## TC-020 - Logged-out user cannot access vital-sign recording

| Field | Detail |
|---|---|
| Feature | Logged-out permission |
| Technique | Permission |
| Severity | Critical |
| Preconditions | No user is logged in. |

**Steps:** 1. Open the vital-sign recording URL. 2. Attempt to submit data directly to an `/api/...` clinical endpoint.

**Expected result:** Recording access is denied and the user is redirected to the login screen.

**Review:** Kept

---

## TC-021 - Nurse acknowledges a pending alert

| Field | Detail |
|---|---|
| Feature | Alert status workflow |
| Technique | State transition |
| Severity | High |
| Preconditions | Camila Duarte is logged in; the patient has a pending alert. |

**Steps:** 1. Open the pending alert. 2. Select `Acknowledge`.

**Expected result:** The alert status changes from `Pending` to `Acknowledged`.

**Review:** Kept

---

## TC-022 - Nurse escalates a pending alert

| Field | Detail |
|---|---|
| Feature | Alert status workflow |
| Technique | State transition |
| Severity | High |
| Preconditions | Camila Duarte is logged in; the patient has a pending alert. |

**Steps:** 1. Open the pending alert. 2. Select `Escalate`.

**Expected result:** The alert status changes from `Pending` to `Escalated`.

**Review:** Kept
---

## TC-023 - Critical pending alert escalates after 15 minutes

| Field | Detail |
|---|---|
| Feature | Automatic escalation |
| Technique | Time-based |
| Severity | Critical |
| Preconditions | A CRITICAL alert for an assigned patient is in `Pending` status and remains pending for more than 15 minutes. |

**Steps:** 1. Wait beyond 15 minutes while observing the alert. 2. Refresh or reopen the alert.

**Expected result:** The alert status changes automatically from `Pending` to `Escalated`.

**Review:** Kept -> Automatic escalation does not happen

---

# Summary Table

| ID | Title | Technique | Severity |
|---|---|---|---|
| TC-001 | Nurse saves valid patient vital signs | Happy path | Critical |
| TC-002 | Heart rate at lower normal boundary | Boundary | High |
| TC-003 | Heart rate below lower boundary | Boundary | High |
| TC-004 | Heart rate at 99 bpm | Boundary | Medium |
| TC-005 | Heart rate at 100 bpm | Boundary | High |
| TC-006 | Oxygen saturation at 95% | Boundary | Critical |
| TC-007 | Oxygen saturation below 95% | Boundary | Critical |
| TC-008 | Temperature at 37.7 °C | Boundary | High |
| TC-009 | Temperature at 37.8 °C | Boundary | High |
| TC-010 | Systolic pressure at 139 mmHg | Boundary | Medium |
| TC-011 | Systolic pressure at 140 mmHg | Boundary | Medium |
| TC-012 | Missing heart-rate value | Partitioning | High |
| TC-013 | Nonnumeric heart-rate value | Invalid input | High |
| TC-014 | Negative SpO2 value | Invalid input | High |
| TC-015 | Responsible nurse records data | Permission | Critical |
| TC-016 | Unassigned patient data denied | Permission | Critical |
| TC-017 | Patient cannot access another patient's data | Permission | Critical |
| TC-018 | Patient cannot record vital signs | Permission | Critical |
| TC-019 | Doctor cannot record vital signs | Permission | Critical |
| TC-020 | Logged-out recording denied | Permission | Critical |
| TC-021 | Nurse acknowledges pending alert | State transition | High |
| TC-022 | Nurse escalates pending alert | State transition | High |
| TC-023 | Critical alert escalates after 15 minutes | Time-based | Critical |

# Questions for the team

- Is heart rate `100 bpm` normal or should it trigger a HIGH alert? The business rules currently conflict.
- Is each field mandatory, and what validation ranges and decimal formats should apply?
- Which patients are assigned to Camila Duarte and Paulo Ferreira, and can assignments change?
- Can an Escalated alert later be Acknowledged, or are Escalated and Acknowledged final states?
- At exactly 15:00 after becoming Pending, should a CRITICAL alert remain Pending or escalate?
- If one reading triggers multiple alert types, should the system create one alert or multiple alerts?
- How is the responsible doctor selected when there are multiple doctors?
- How do doctors' custom thresholds interact with the fixed thresholds in BR-01?
- Is there an administrator role, and if so, what permissions should it have?
- Can new Sign-up accounts act as nurses or doctors, and how are patient assignments established?
