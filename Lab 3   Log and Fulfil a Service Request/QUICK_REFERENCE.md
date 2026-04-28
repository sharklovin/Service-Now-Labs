# Quick Reference - ServiceNow Request Management

## Record Number Prefixes

| Prefix | Record Type | Where to Find |
|---|---|---|
| REQ | Request (parent) | Service Desk > Requests |
| RITM | Request Item | Service Desk > Requested Items |
| TASK | Task (sub-task) | Service Desk > Tasks |
| INC | Incident | Service Desk > Incidents |
| CHG | Change Request | Change > All |
| PRB | Problem | Problem > All |

---

## RITM Lifecycle States

```
Open
  |
  v
Work in Progress
  |
  v
Waiting for Approval  <-- approval gates can pause here
  |
  v
Approved
  |
  v
Order Fulfillment     <-- physical/technical work happens here
  |
  v
Closed Complete       <-- target end state
     or
Closed Cancelled      <-- if cancelled before completion
```

---

## Key Navigation Paths

| Task | Navigation |
|---|---|
| Browse catalog | Self Service > Service Catalog |
| View your requests | Self Service > My Requests |
| View all requests | Service Desk > Requests |
| View all RITMs | Service Desk > Requested Items |
| View catalog items | Service Catalog > Catalog Items |
| Manage order guides | Service Catalog > Order Guides |

---

## Closing an RITM Correctly

1. Open the RITM record
2. Add a **Work Note** describing what was done (be specific)
3. Change **State** to `Closed Complete`
4. Click **Update**
5. Verify the Stage updates to `Order Fulfillment`
6. Verify the parent REQ state reflects the change

---

## Common Mistakes to Avoid

| Mistake | Why It Matters |
|---|---|
| Logging a request as an incident | Breaks ITIL categorisation and reporting |
| Closing RITM without a work note | No audit trail - no evidence of what was done |
| Manually closing the parent REQ | ServiceNow does this automatically - manual closure can cause issues |
| Not checking the assignment group | Work lands in the wrong queue |
| Mixing Comments and Work Notes | Customer-visible comments go to the requester - internal notes must use Work Notes |

---

*ServiceNow ITSM - Lab 03 Quick Reference*
