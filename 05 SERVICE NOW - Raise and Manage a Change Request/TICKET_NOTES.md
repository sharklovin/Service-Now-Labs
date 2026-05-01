# Ticket Notes - CHG0030007

> **Change type:** Normal
>
> **Module:** ServiceNow Change Management
>
> **Lab:** Lab 06 - Raise and Manage a Change Request
>
> **Completed:** May 2026

---

## Change Record Field Summary

| Field | Value | Notes |
|---|---|---|
| **Number** | CHG0030007 | Auto-assigned on form open. Reserved immediately. |
| **Requested by** | System Administrator | The PDI admin account. In production, this would be the engineer or team lead raising the request. |
| **Model** | Normal | Drives the workflow template and required fields. |
| **Type** | Normal | Confirms this follows the full ITIL Normal Change lifecycle. |
| **Category** | Other | Used for reporting. In a mature instance, Network or Infrastructure would be more precise. |
| **Priority** | 4 - Low | Priority of the change process itself. Not the urgency of the underlying risk - that is captured by Risk. |
| **Risk** | Moderate | Justified by: affects all second-floor users, brief network disruption during maintenance window, known rollback path. |
| **Impact** | 3 - Low | Set at Low because the impact is limited to one floor, during a planned maintenance window, outside business hours. |
| **Assignment group** | Network Team | Routes the change to the correct team queue. |
| **Short description** | Upgrade core network switch firmware for second floor | Specific, unambiguous. Identifies the action (firmware upgrade), the asset (core network switch), and the scope (second floor). |
| **Description** | Planned upgrade of core switch firmware to improve performance, patch vulnerabilities, and ensure stability. | Answers what, why, and expected outcome. |
| **Planned start date** | 2026-05-09 02:23:31 | A future maintenance window date outside business hours. |
| **Planned end date** | 2026-05-09 02:23:48 | End of the maintenance window. Used for conflict checking. |
| **Conflict status** | Not Run | Conflict check was not run in this lab exercise. In production, run the conflict check before submitting for CAB review. |
| **Final state** | Closed | Record is permanent and immutable. |
| **Close code** | Successful | Upgrade completed without incident. |

---

## Planning Tab Fields

### Justification

Not completed in this lab. In production, Justification should answer: why is this change necessary now? What is the risk of not making this change?

For CHG0030007 a complete justification would read:

> The second-floor core switch is running firmware version X.X. This version has two known CVEs rated CVSS 7.4 and 8.1. Deferring the upgrade beyond this maintenance window extends the vulnerability exposure window. Additionally, the current firmware has a documented performance regression under sustained traffic loads above 80% utilisation, which has been observed during peak hours. The upgrade addresses both the security and performance issues in a single maintenance window.

### Implementation Plan

```
Step 1 - Confirm maintenance window with stakeholders
Step 2 - Take configuration backup of the current switch
Step 3 - Apply firmware upgrade
Step 4 - Verify connectivity across all switch ports
Step 5 - Monitor system for 30 minutes before closing
```

**Why this order matters:** Step 2 must happen before Step 3. The configuration backup is the mechanism that makes the backout plan executable. If the backup is taken after the upgrade attempt and the upgrade corrupts the configuration, there is nothing to restore. The sequence is deliberate.

### Backout Plan

```
If the upgrade fails, restore the configuration backup and revert to the
previous firmware version. Estimated recovery time: 15 minutes.
```

**What makes this a good backout plan:**
- Specific action: restore the configuration backup (the one taken in Step 2)
- Specific outcome: previous firmware version running
- Time estimate: 15 minutes (allows window planning)
- Trigger: "if the upgrade fails" - clear condition for invocation

**What would make it better in production:**
- Name the exact backup file location and filename
- Name the specific command or procedure to restore the backup
- Name who is responsible for deciding to invoke the backout plan
- Specify what "upgrade fails" means precisely - does a partial upgrade trigger backout, or only a complete failure?

### Test Plan

```
Ping all connected devices
Verify internet access
Confirm file server access
Check VoIP phone registration
```

**Why these four tests:** They cover the four service categories that use the switch as their network path. IP connectivity (ping), external access (internet gateway), internal file services (file server), and real-time communications (VoIP). If all four pass, every service that depends on this switch is confirmed working. If any fail, the backout plan is invoked immediately.

**What would improve the test plan in production:**
- Specify device names or IP addresses to ping, not just "all connected devices"
- Specify the file server name and a test file path to confirm access
- Specify which VoIP phones should be checked (all, or a representative sample)
- Specify who is responsible for running each test and confirming the result

---

## State Transition Log

| From state | To state | Timestamp | Notes |
|---|---|---|---|
| - | New | 2026-05-01 | Form submitted, CHG0030007 created |
| New | Assess | 2026-05-01 | Auto-advanced on Submit, all required fields valid |
| Assess | Authorize | 2026-05-01 | Change manager reviewed planning fields |
| Authorize | Scheduled | 2026-05-01 | Approval record set to Approved by Howard Johnson at 03:13:56 |
| Scheduled | Implement | 2026-05-01 03:16:26 | Maintenance window opened |
| Implement | Review | 2026-05-01 03:19:26 | Implementation complete, tests passed |
| Review | Closed | 2026-05-01 | Close code Successful, closure notes added |

---

## Approval Record Details

| Field | Value |
|---|---|
| **Approver** | Howard Johnson |
| **Approving** | Change Request: CHG0030007 |
| **Approval for** | CHG0030007 |
| **State** | Approved |
| **Approved at** | 2026-05-01 03:13:56 |
| **Previous state** | Requested |
| **Changed by** | System Administrator (simulating CAB approval in PDI) |

In a production environment, Howard Johnson would log in to ServiceNow and set the approval state himself. The audit trail would show his username, not the System Administrator. The PDI simulation uses admin credentials to demonstrate the workflow without requiring a second user account.

---

## Work Notes Log

### Work Note 1 - Implement State

**Posted:** 2026-05-01 03:17:34
**Posted by:** System Administrator
**Type:** Work note (internal, not visible to caller)

```
Maintenance window started at 02:00.
Switch backup completed.
Firmware upgrade in progress.
```

**Purpose:** Documents the real-time status during the maintenance window. Anyone monitoring the change queue can see that work started on schedule, the backup completed successfully (meaning the backout plan is executable if needed), and the upgrade is actively being applied.

---

### Work Note 2 - Review State

**Posted:** 2026-05-01 03:19:26
**Posted by:** System Administrator
**Type:** Work note (internal, not visible to caller)

```
Firmware upgrade completed successfully.
All connectivity tests passed.
No issues observed during monitoring period.
```

**Purpose:** Documents the outcome against the test plan. Three statements, each mapping to a specific test: upgrade completed (confirming Step 3 succeeded), all connectivity tests passed (confirming the test plan checks all returned positive), no issues during monitoring (confirming Step 5 completed without alerts).

---

## Closure Information

| Field | Value |
|---|---|
| **Close code** | Successful |
| **Close notes** | Firmware upgrade completed successfully. All connectivity tests passed. No issues observed during monitoring period. |

**Close code options in ServiceNow Change Management:**

- **Successful** - Change implemented as planned, all tests passed, no unplanned impact
- **Successful with issues** - Change implemented but with minor deviations from the plan, resolved during the window
- **Unsuccessful** - Change attempted but failed, backout plan invoked, original state restored
- **Canceled** - Change withdrawn before implementation

The close code is used for CAB metrics. Over time, a high rate of Unsuccessful close codes in a category (network changes, application deployments, database changes) signals that the planning process for that category needs improvement.

---

## Key Observations on ServiceNow Change Management Behaviour

**1. The CHG number is reserved the moment the form opens.**
CHG0030007 was assigned before any field was filled in. If the form is closed without saving, the number is released but the sequence has already incremented. Gaps in CHG numbers are normal and do not indicate deleted records.

**2. State transitions are logged automatically.**
Every state change - New to Assess, Scheduled to Implement, Implement to Review - generates an automatic audit entry with a timestamp and the username of whoever made the change. These entries cannot be edited or deleted.

**3. Work notes are internal; comments are customer-facing.**
Both appear in the Activity section but with different visibility. Work notes are visible to the support team only. Comments are visible to the requester if they have portal access. In change management, most communication is via work notes. Comments are used when the requester needs a status update.

**4. The conflict check is separate from saving the record.**
The Conflict status showing Not Run does not mean there are no conflicts - it means the check has not been run. In production, always run the conflict check before submitting for CAB review. Scheduling a change that conflicts with another change on the same CI can cause both to fail.

**5. The Closure Information tab fields only appear when the change is in Review or Closed state.**
Close code and Close notes are not visible on the main form during New, Assess, or Authorize. They appear only when the change is ready to close. Looking for them earlier in the lifecycle will not find them.

**6. The approval record is separate from the change record.**
The approval exists as its own record linked to the change. Navigating to the change record does not automatically show the approval - you need to open the Approvals related list or navigate directly to the approval record. The approval state must be set to Approved before the change can advance past Scheduled.

**7. Advancing the state requires clicking Update or Submit.**
ServiceNow does not auto-save on state changes. Selecting a new state from the dropdown and then navigating away will lose the change. Always click Update after any modification.

---

## Risk Assessment Guidance

The Risk field in ServiceNow Change Management is a subjective assessment. There is no automatic calculation from other fields the way Priority is calculated from Impact and Urgency in Incident Management. The technician must assess risk based on the specific circumstances of the change.

A useful framework for setting risk level:

```
LOW RISK
  - Affects a single user or device
  - Fully reversible with no data loss
  - Tested process done multiple times before
  - No dependency on other systems
  - No user-visible impact during implementation

MODERATE RISK (used in this lab)
  - Affects a team, floor, or department
  - Reversible via a tested backout plan
  - Process is understood but not routine
  - Some dependency on other systems
  - Brief user-visible impact during maintenance window

HIGH RISK
  - Affects the entire organisation or a critical system
  - Reversal is complex, time-consuming, or uncertain
  - First time this process has been attempted
  - Strong dependencies - failure cascades to other systems
  - Extended user-visible impact or potential data exposure

CRITICAL RISK (requires CAB escalation)
  - Affects production systems for all users
  - No tested backout plan exists
  - Irreversible - no ability to restore previous state
  - Regulatory or compliance implications
  - Potential for data loss or breach
```

CHG0030007 was assessed as Moderate because: it affects all second-floor users (broader than a single user), it has a specific and tested backout path (restore config backup), the firmware upgrade process is understood by the network team, and the impact is limited to a planned maintenance window outside business hours.

---

## Relationship Between Change Management and Incident Management

Change management and incident management are the two most frequently interacting ITIL processes. Understanding their relationship is essential for working in any service desk or operations role.

**Changes can cause incidents.** A firmware upgrade that introduces a bug, a configuration change that breaks a dependency, a scheduled maintenance window that overruns and affects business hours - all of these create incidents. The change record is the first place to look when a new incident appears shortly after a maintenance window. ServiceNow supports this through the CI (Configuration Item) field - if both the change and the incident reference the same CI, they can be correlated in reporting.

**Incidents can trigger changes.** A recurring incident - Outlook crashing after a specific update, network drops on a specific segment - eventually leads to a problem record, which in turn leads to a change request to fix the root cause. The incident is the symptom; the change is the cure.

**The change record protects the support team.** If an incident occurs after a change, the support team can review the change record to understand exactly what was done, in what sequence, by whom, and when. The implementation plan, work notes, and closure documentation give the incident responder a complete picture of the recent change activity without having to reconstruct it from memory or verbal briefings.

In CHG0030007, the test plan specifically checks for the services most likely to be affected by a switch firmware issue. If a network incident is raised on 2026-05-09 involving any of those four services, the first question the incident manager will ask is whether CHG0030007 completed successfully. The closed, documented change record answers that question immediately.
