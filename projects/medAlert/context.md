# Project context: MedAlert

> Source: *QA 5x Technical Challenge — MedAlert* (PDF specification).
> The business rules below are the **source of truth**: any system behavior that diverges from them is a bug or inconsistency to report.

## What the system is
MedAlert is a hospital alert management platform. Nurses record patients' vital signs, the system raises alerts based on fixed thresholds, and alerts follow a status workflow (acknowledge / escalate). Doctors set thresholds, prescribe medication and discharge patients.

The system handles **health data** and has **role-based access control**, so data privacy and permissions are high-risk areas.

## Roles and permissions
| Role | Can do |
|------|--------|
| **Patient** | View **their own** vital signs, alerts and prescriptions; request nursing assistance |
| **Nurse** | View the patients **under their responsibility**; record vital signs; acknowledge or escalate alerts |
| **Doctor** | View the patients **under their responsibility**; set alert thresholds; prescribe medication; discharge patients |
| **Logged out** | Login screen, "Sign up" and "Reset system data" links only (expected: no access to clinical data or the `/api/...` clinical endpoints) |

## Test users
All passwords: `senha123`

| User | Role |
|------|------|
| Marina Souza | Patient |
| Roberto Lima | Patient |
| Camila Duarte | Nurse |
| Paulo Ferreira | Nurse |
| Dra. Helena Prado | Doctor |

- Use only these users. To test more scenarios, create new accounts (patient, nurse or doctor) with the **"Sign up"** link on the login screen.
- The specification **does not say** which patients are assigned to which nurse or doctor. Check this in the running system before writing access-control tests.

## Environment
- Full stack, runs locally: front end, Node.js back end, file-based SQLite database. No data leaves the machine.
- Prerequisite: Node.js 18+
- Setup: `npm install`, then `npm start`, then open `http://localhost:3000`
- REST API under `/api/...`. Tests can run through the UI and/or directly against the API.
- Setup and troubleshooting are in the repository's `README.md`.

### Test data
- Data persists across server restarts.
- Data **resets automatically every day**.
- Manual reset: the **"Reset system data"** link on the login screen, or `npm run reset-db`.

## Business rules

### BR-01: Vital sign alert thresholds
| Vital sign | Normal range | Alert rule | Severity |
|------------|--------------|------------|----------|
| Heart rate (HR) | 50–100 bpm | HR >= 100 bpm **or** HR < 50 bpm | HIGH |
| Oxygen saturation (SpO2) | >= 95% | SpO2 < 95% | CRITICAL |
| Body temperature | up to 37.7 °C | temperature >= 37.8 °C | HIGH |
| Systolic blood pressure | up to 139 mmHg | systolic >= 140 mmHg | MEDIUM |

### BR-02: Alert status flow
`Pending` → `Acknowledged` (manual, nurse action)
`Pending` → `Escalated` (manual by the nurse, **or** automatic)

### BR-03: Automatic escalation
A **CRITICAL** alert that stays in **Pending** for **more than 15 minutes** must be escalated automatically to the patient's doctor.

### BR-04: Access control
- A patient can only view **their own** clinical data.
- A nurse can only view and act on patients **under their responsibility**.
- A doctor can only view patients **under their responsibility**.
- Clinical data (chart, medical notes, prescriptions) is sensitive and **must not leak between roles**.

## High-risk areas
- Leaks of sensitive health data between patients and roles, through both the UI and the API
- Irreversible actions, such as discharging a patient
- Boundary values in the alert thresholds
- Time-based rules (15-minute automatic escalation)
- Stateful workflows (alert status transitions)

## Known ambiguities (open questions)
- **HR = 100 bpm:** the normal range says "50–100 bpm", but the alert rule says "HIGH when HR >= 100". Is 100 normal or an alert?
- **Patient assignments:** which patients belong to which nurse and doctor? Can an assignment change?
- **Status transitions after Pending:** can an Escalated alert later be Acknowledged? Are Acknowledged/Escalated final states?
- **Automatic escalation:** what does "more than 15 minutes" mean at exactly 15:00? How is "the patient's doctor" decided if more than one doctor exists (for example, one created via Sign up)?
- **Custom thresholds:** doctors can "set alert thresholds". How do they interact with the fixed rules in BR-01? Per patient? Within limits?
- **Sign up:** can anyone self-register as a nurse or doctor? Are new accounts assigned any patients?
- **Discharge:** what happens to a discharged patient's open alerts and data access?
- **Multiple values at once:** when one reading triggers more than one alert (for example, low SpO2 and high temperature), is it one alert or several?

## Out of scope / constraints
- The specification states that not every problem in the system is listed in it. Exploratory testing is expected.
- All deliverables (test cases, bug reports, code comments) must be in **English**.
