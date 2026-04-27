# INC0008111 - Ticket Notes

**Incident:** INC0008111
**Short Description:** User cannot connect to VPN
**Caller:** System Administrator
**Urgency:** 3 - Low
**Opened:** 2019-07-22 14:04:57
**Closed:** 2026-04-26 07:28:02

---

## Activity Log - Full Chronological Record

---

### [1] - 2026-04-26 05:12:45 | Comments | System Administrator

**State at time of note:** In Progress

> Contacted user to confirm the issue. User reports VPN client returns error code 429 during connection attempt. Issue started after recent Windows update.

---

### [2] - 2026-04-26 05:19:25 | Comments | System Administrator

**State at time of note:** In Progress

> Checked Active Directory - account active, VPN group membership confirmed. Checked VPN gateway status page - no outage reported. Issue appears to be client-side.

---

### [3] - 2026-04-26 05:20:30 | Comments | System Administrator

**State at time of note:** In Progress

> Guided user to uninstall and reinstall the Cisco AnyConnect client. Issue persisted. Escalating to network team for gateway-side log review.

---

### [4] - 2026-04-26 05:22:38 | Comments | System Administrator

**State at time of note:** In Progress

> Guided user to uninstall and reinstall the Cisco AnyConnect client. Issue persisted. Escalating to network team for gateway-side log review.

*(Escalation note - assignment group changed to Network Team, state set to On Hold - Awaiting Change)*

---

### [5] - 2026-04-26 05:36:42 | Comments | System Administrator

**State at time of note:** On Hold - Awaiting Change

> Network Team confirmed a policy change was applied to the VPN gateway last night that affected single-factor auth users. Policy has been reverted. User asked to retry.

---

### [6] - 2026-04-26 05:42:37 | Comments | System Administrator

**State at time of note:** In Progress

> Network Team: User tested VPN connection after policy revert and confirmed successful connection. Issue resolved.

---

### [7] - 2026-04-26 05:43:56 | Comments | System Administrator

**State at time of note:** Resolved

> VPN connectivity issue caused by recent policy change on VPN gateway affecting single-factor authentication users. Network team reverted the policy, restoring access. User confirmed successful connection post-change.

*(This entry contains the formal Resolution Notes added when state changed to Resolved)*

---

### [8] - 2026-04-26 05:52:21 | Field Changes | System Administrator

**State at time of entry:** Resolved (was On Hold)

| Field | New Value | Previous Value |
|---|---|---|
| Incident state | Resolved | On Hold |
| Resolution code | Resolved by problem | - |
| Resolution notes | Closed by Caller | - |

*(System-generated audit entry recording all field changes at resolution)*

---

### [9] - 2026-04-26 07:28:02 | Field Changes | System

**State at time of entry:** Closed (was Resolved)

> Incident auto-closed after resolution confirmation period elapsed. Closed timestamp populated: 2026-04-26 07:28:02.

---

## Resolution Summary

| Field | Value |
|---|---|
| Root Cause | VPN gateway policy change applied the previous night blocked single-factor authentication users |
| Fix Applied | Network Team reverted the gateway policy change |
| Confirmed By | User - tested connection post-revert and confirmed success |
| Resolution Code | Resolved by Problem |
| Resolution Notes | VPN connectivity issue caused by recent policy change on VPN gateway affecting single-factor authentication users. Network team reverted the policy, restoring access. User confirmed successful connection post-change. |

---

## State Transition History

```
New
  |
  v
In Progress  (Work Note #1 - user contacted, error 429 confirmed)
  |
  v
In Progress  (Work Note #2 - AD + gateway checks completed)
  |
  v
In Progress  (Work Note #3 - AnyConnect reinstall failed)
  |
  v
On Hold - Awaiting Change  (Escalated to Network Team)
  |
  v
In Progress  (Network team reverted policy, user confirmed success)
  |
  v
Resolved  (Resolution code + notes filled in)
  |
  v
Closed  (Auto-close after confirmation period)
```
