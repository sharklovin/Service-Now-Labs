# Lab 2 - ServiceNow Incident Lifecycle

## What Is This?

This repository contains a complete, screenshot-documented walkthrough of **Lab 2: Work an Incident Through Its Full Lifecycle** using a ServiceNow Personal Developer Instance (PDI).

It is designed to be used as a self-paced learning resource, a team training reference, or a portfolio artifact demonstrating hands-on ServiceNow ITSM skills.

---

## Repository Structure

```
lab2-servicenow-incident-lifecycle/
|
|- README.md                         <- Full step-by-step lab guide (start here)
|- INC0008111-ticket-notes.md        <- Complete Activity log transcription
|- LAB-OVERVIEW.md                   <- This file
|
|- screenshots/
   |- step-01_new-incident-created.png
   |- step-02_state-in-progress-first-work-note.png
   |- step-03_second-work-note-ad-check.png
   |- step-04_third-work-note-escalation.png
   |- step-05_escalation-note-duplicate-view.png
   |- step-06_state-on-hold-awaiting-change.png
   |- step-07_user-confirmed-vpn-resolved.png
   |- step-08_state-resolved-resolution-notes.png
   |- step-09_field-changes-resolved-by-problem.png
   |- step-10_incident-closed-final-state.png
```

---

## How to Use This Lab

1. Open `README.md` - follow each step in order
2. Each step includes a screenshot showing the expected ServiceNow state
3. Red annotation boxes in screenshots highlight the key fields to focus on
4. Use the checklist at the bottom of `README.md` to validate your work
5. Reference `INC0008111-ticket-notes.md` to compare your Activity log entries

---

## Skills Demonstrated

- ServiceNow Incident Management module navigation
- Full ITSM lifecycle execution (New - In Progress - On Hold - Resolved - Closed)
- Structured work note writing at every state transition
- Incident escalation with proper documentation
- Root cause identification and resolution documentation
- Audit trail verification via Activity log

---

## Prerequisites

- Access to a ServiceNow PDI (free at [developer.servicenow.com](https://developer.servicenow.com))
- Completion of Lab 1 (Create and Categorize an Incident) is recommended
- Basic familiarity with the ServiceNow interface

---

## Incident Summary

| Field | Value |
|---|---|
| Incident | INC0008111 |
| Issue | User cannot connect to VPN |
| Root Cause | VPN gateway policy change blocking single-factor auth users |
| Resolution | Network team reverted gateway policy |
| Total Activities | 10 |
| Final State | Closed |
