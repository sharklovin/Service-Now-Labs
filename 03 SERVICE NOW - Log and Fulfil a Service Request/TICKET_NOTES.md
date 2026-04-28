# Lab 03 - Ticket Notes

> Fulfilment documentation for REQ0010002 - New Hire Setup
> Date: 2026-04-28
> Logged by: System Administrator

---

## Parent Request

| Field | Value |
|---|---|
| Request Number | REQ0010002 |
| Requested for | System Administrator |
| Opened | 2026-04-28 01:33:04 |
| Opened by | System Administrator |
| Due date | 2026-05-07 01:33:02 |
| Price | $1,100.00 |
| Approval | Approved |
| Request state | Approved |
| Order Guide | New Hire |

**Summary:** New hire setup request submitted via the Service Catalog using the New Hire Order Guide. The request bundles four items across three fulfilment teams. All RITMs routed automatically based on catalog item configuration.

---

## RITM0010007 - Standard Laptop

| Field | Value |
|---|---|
| RITM Number | RITM0010007 |
| Item | Standard Laptop |
| Request | REQ0010002 |
| Requested for | System Administrator |
| Opened | 2026-04-28 01:33:03 |
| Due date | 2026-05-07 01:33:02 |
| Assignment Group | Hardware |
| Order Guide | New Hire |
| Stage | Waiting for Approval |
| State | Work in Progress |
| Quantity | 1 |

**Work Notes:**
> Laptop allocated, asset tagged and prepared for delivery

**Fulfilment Actions:**
- Standard laptop model identified from hardware inventory
- Asset tag applied and recorded in CMDB
- Device imaged with standard SOE (Standard Operating Environment)
- Packaged and staged for delivery to new hire desk location
- Awaiting manager approval before physical handover

---

## RITM0010009 - New Email Account

| Field | Value |
|---|---|
| RITM Number | RITM0010009 |
| Item | New Email Account |
| Request | REQ0010002 |
| Requested for | System Administrator |
| Opened | 2026-04-28 01:33:03 |
| Due date | 2026-04-28 01:33:02 |
| Assignment Group | Service Desk |
| Order Guide | New Hire |
| Stage | waiting_for_approval |
| State | Work in Progress |
| Quantity | 1 |

**Work Notes:**
> Active Directory account created and Microsoft 365 license assigned

**Fulfilment Actions:**
- Active Directory user account created in the corporate domain
- Username format: firstname.lastname@company.com
- Temporary password issued (expires on first login - user must set new password)
- Microsoft 365 Business Standard licence assigned
- Exchange Online mailbox provisioned automatically
- Welcome email sent to manager with credentials for handover
- Account added to standard new hire security groups

---

## RITM0010008 - Corp VPN Access

| Field | Value |
|---|---|
| RITM Number | RITM0010008 |
| Item | Corp VPN |
| Request | REQ0010002 |
| Requested for | System Administrator |
| Opened | 2026-04-28 01:33:03 |
| Due date | 2026-04-28 01:33:02 |
| Assignment Group | Network Team |
| Order Guide | New Hire |
| Stage | waiting_for_approval |
| State | Work in Progress |
| Quantity | 1 |

**Work Notes:**
> Access request submitted and VPN profile configured

**Fulfilment Actions:**
- VPN access request reviewed by Network Team
- User account added to VPN security group in Active Directory
- Cisco AnyConnect profile configured for standard remote access tier
- MFA enrollment link sent to new hire email
- VPN connection tested from external network - confirmed working
- User guide for VPN connection attached to RITM for reference

---

## RITM0010001 - Standard Laptop (Closed)

| Field | Value |
|---|---|
| RITM Number | RITM0010001 |
| Item | Standard Laptop |
| Request | REQ0010002 |
| Requested for | System Administrator |
| Opened | 2026-04-28 01:33:03 |
| Due date | 2026-05-07 01:33:02 |
| Assignment Group | Hardware |
| Order Guide | New Hire |
| Stage | Order Fulfillment |
| State | **Closed Complete** |
| Quantity | 1 |

**Work Notes:**
> Laptop allocated, asset tagged, and prepared for delivery

**Closure Notes:**
- All hardware fulfilment steps completed
- Physical delivery confirmed
- User acknowledgement received
- RITM closed - Stage advanced to "Order Fulfillment" automatically
- No further action required on this RITM

---

## Fulfilment Timeline

```
2026-04-28 01:33:03   REQ0010002 created via Service Catalog (New Hire Order Guide)
2026-04-28 01:33:03   RITMs auto-generated: RITM0010001, RITM0010007, RITM0010008, RITM0010009
2026-04-28 01:33:04   Order Status confirmation shown to requester
2026-04-28            RITM0010009 actioned by Service Desk - AD account and M365 licence created
2026-04-28            RITM0010008 actioned by Network Team - VPN profile configured
2026-04-28            REQ0010002 Approval status: Approved
2026-04-28            RITM0010001 closed - State: Closed Complete, Stage: Order Fulfillment
2026-05-07 (target)   RITM0010007 delivery due - Standard Laptop
```

---

## Observations and Learning Points

### 1. Requests vs Incidents
Requests originate from the Service Catalog and represent fulfilment work. Incidents originate from service disruptions and represent break-fix work. They are managed in separate queues, follow different workflows, and are reported on differently. Mixing the two creates reporting inaccuracies and SLA compliance issues.

### 2. Order Guides
An Order Guide bundles multiple catalog items into a single request. This is ideal for scenarios like new hire onboarding where multiple items always go together. Each bundled item still generates its own RITM and routes independently.

### 3. RITM Auto-Routing
When a catalog item is submitted, ServiceNow uses the catalog item configuration (specifically the "Fulfillment Group" field on the catalog item) to automatically set the Assignment Group on the RITM. This means agents in the right teams receive the work without manual dispatching.

### 4. Parent-Child State Relationship
The parent REQ does not need to be manually closed. When all child RITMs reach "Closed Complete" or "Closed Cancelled", the REQ state updates automatically. Partially closed requests show the in-progress state of the remaining open RITMs.

### 5. Work Notes vs Comments
- **Work Notes** are internal - visible only to agents and fulfillment teams. Use these to document technical actions taken.
- **Comments** (with "Customer Visible" checked) are sent to the requester. Use these for communication updates.
- Always document fulfilment actions in Work Notes before closing an RITM.

---

## Validation Summary

| Check | Result |
|---|---|
| REQ0010002 created | Confirmed |
| REQ shows Approved state | Confirmed |
| 4 RITMs generated automatically | Confirmed |
| RITM0010007 assigned to Hardware | Confirmed |
| RITM0010009 assigned to Service Desk | Confirmed |
| RITM0010008 assigned to Network Team | Confirmed |
| Work notes present on all RITMs | Confirmed |
| RITM0010001 Closed Complete | Confirmed |
| Stage "Order Fulfillment" on closed RITM | Confirmed |
| Parent REQ reflects Approved/progressing state | Confirmed |

---

*Lab 03 - Log and Fulfil a Service Request | ServiceNow PDI | 2026-04-28*
