# Log and Fulfil a Service Request

**Platform:** ServiceNow Personal Developer Instance (PDI)

**Module:** Service Catalog - Request Management

**Priority:** High

**Estimated Duration:** 45-60 minutes

---

## Objective

Use the ServiceNow Service Catalog to submit a service request, fulfil it through the request workflow, and close it with evidence of completion.

---

## Business Scenario

> A new employee is starting on Monday and needs the following items provisioned before their first day:
>
> - A **Standard Laptop** (hardware)

> - A **New Email Account** (Active Directory + Microsoft 365 licence)
> - **Corporate VPN Access** (network provisioning)
>
> The request comes through the self-service portal. Your job is to log it correctly as a **Request** - not an Incident - assign the fulfilment tasks to the right teams, document all actions taken, and close each task as it is completed.

---

## Key Concepts Before You Begin

| Term | Definition |
|---|---|
| **REQ** | The parent Request record - a container for everything the user asked for |
| **RITM** | Request Item - one line item within the request (one per catalog item ordered) |
| **Task** | A sub-task that can be created under an RITM for granular work tracking |
| **Incident** | Break-fix work - something broken that needs restoring. Never use an incident for fulfilment work |
| **Catalog Item** | A pre-built, orderable service from the Service Catalog |

---

## Tools Required

| Resource | Details |
|---|---|
| Platform | ServiceNow PDI |
| Navigation | Self Service > Service Catalog |
| Navigation | Service Desk > Requests |
| Records used | REQ, RITM |
| Modules | Service Catalog, Request Management |

---

## Lab Steps

### Step 1 - Understand Requests vs Incidents

Navigate to **Service Desk > Requests** and separately to **Service Desk > Incidents**. Observe the structural difference.

- The **Request list** (Tasks View) shows records prefixed `REQ` with a Task type of `Request`
- The **Incident list** shows records prefixed `INC` and relates to service disruptions

> A request is fulfilment work. An incident is break-fix work. This distinction is fundamental to ITIL-aligned service management.

<img width="1365" height="637" alt="01_request_vs_incident_list" src="https://github.com/user-attachments/assets/0b9b566e-6083-47ac-8ba3-b18ea3bd1ea6" />

*Fig 1 - Left: Tasks view showing REQ0000001 as a Request type. Right: Incidents view showing INC0008111 "User cannot connect to VPN" - these are two fundamentally different record types.*

---

### Step 2 - Browse the Service Catalog

Navigate to **Self Service > Service Catalog**.

Explore the available categories:
- **Hardware** - laptops, phones, tablets
- **Software** - applications for installation
- **Services** - document production and professional services
- **Can We Help You?** - a general gateway for submitting requests
- **Office** - printing, supplies, document shipping

Note the **Top Requests** sidebar on the right - this shows the most commonly ordered items in your instance.

<img width="1356" height="638" alt="02_service_catalog_overview" src="https://github.com/user-attachments/assets/504e78b2-4e97-4bd4-92d8-4c87e2ad37bd" />

*Fig 2 - The Service Catalog homepage. The "Can We Help You?" tile and Top Requests sidebar (both highlighted) are key starting points for end users and help desk agents.*

---

### Step 3 - Submit the New Hire Request

For this lab, the request was submitted using the **New Hire Order Guide** which bundles multiple catalog items into a single request. This generated **REQ0010002**.

The order included four line items:
1. Remote access to Internal Corporate Systems (due 2026-04-28)
2. New Email Creation (due 2026-04-28)
3. Desk Set Up for New Hires or Employee Moves (due 2026-05-07)
4. Standard Monitor - 27", 1920x1080, 280Hz, IPS Variable, FreeSync (due 2026-04-30)

> If your PDI does not have a New Hire Order Guide, submit individual catalog items from the Hardware and Software categories and note the REQ number generated.

<img width="1363" height="632" alt="03_order_status_req0010002" src="https://github.com/user-attachments/assets/88a1af26-d203-432b-b986-ffd4cd6155ee" />

*Fig 3 - Order Status confirmation for REQ0010002. The highlighted section shows the four line items, their delivery dates, and their current Stage indicators. The order was placed on 2026-04-28 at 01:33:04.*

---

### Step 4 - Locate the RITM Records

Each line item in the order generates its own **RITM (Request Item)** record automatically. Open the parent REQ and scroll to the **Requested Items** related list, or navigate directly via:

**Service Desk > Requested Items** and filter by Request = REQ0010002

You should see:
- RITM0010001 - Standard Laptop
- RITM0010007 - Standard Laptop
- RITM0010008 - Corp VPN
- RITM0010009 - New Email Account

> The RITM is the unit of work. Each RITM is assigned to a different team and moves through its own lifecycle independently.

---

### Step 5 - Fulfil RITM: Standard Laptop (RITM0010007)

Open **RITM0010007**.

**Fields to observe:**
- **Item:** Standard Laptop
- **Assignment Group:** Hardware
- **Stage:** Waiting for Approval
- **State:** Work in Progress
- **Order Guide:** New Hire

**Action taken:**
1. Confirm the assignment group is set to `Hardware`
2. Verify the Stage shows `Waiting for Approval`
3. Add a Work Note: `Laptop allocated, asset tagged and prepared for delivery`
4. The RITM remains in `Work in Progress` until approval and delivery is confirmed

<img width="1365" height="637" alt="04_ritm0010007_standard_laptop" src="https://github.com/user-attachments/assets/a277dccf-0cae-4217-8326-5a47d28e9386" />

*Fig 4 - RITM0010007 for Standard Laptop. Highlighted: Stage "Waiting for Approval" and the Work Notes field documenting the fulfilment action taken by the Hardware team.*

---

### Step 6 - Fulfil RITM: New Email Account (RITM0010009)

Open **RITM0010009**.

**Fields to observe:**
- **Item:** New Email Account
- **Assignment Group:** Service Desk
- **Stage:** waiting_for_approval
- **State:** Work in Progress
- **Order Guide:** New Hire

**Action taken:**
1. Confirm assignment group is `Service Desk`
2. Add a Work Note: `Active Directory account created and Microsoft 365 license assigned`
3. The account provisioning is logged and traceable

<img width="1363" height="614" alt="05_ritm0010009_new_email_account" src="https://github.com/user-attachments/assets/3a53b135-1b93-48f8-9863-ac0b38b7296d" />

*Fig 5 - RITM0010009 for New Email Account. Highlighted: Assignment Group "Service Desk" and Stage "waiting_for_approval". The Work Notes confirm the AD account and M365 licence were provisioned.*

---

### Step 7 - Fulfil RITM: Corp VPN Access (RITM0010008)

Open **RITM0010008**.

**Fields to observe:**
- **Item:** Corp VPN
- **Assignment Group:** Network Team
- **Stage:** waiting_for_approval
- **State:** Work in Progress
- **Order Guide:** New Hire

**Action taken:**
1. Assignment group is `Network Team` - correctly routed
2. Add Work Note: `Access request submitted and VPN profile configured`
3. State is set to `Work in Progress` (shown with green highlight in the State field)

<img width="1365" height="619" alt="06_ritm0010008_corp_vpn_access" src="https://github.com/user-attachments/assets/e8dffe9d-d225-4978-bd9f-71aa7c56de1e" />

*Fig 6 - RITM0010008 for Corp VPN. Highlighted: State dropdown showing "Work in Progress" (note the active green border) and Assignment Group "Network Team". Work Note reads "Access request."*

---

### Step 8 - Confirm Parent REQ Status

Navigate back to the parent **REQ0010002**.

Observe the following fields:
- **Approval:** Approved
- **Request state:** Approved
- **Price:** $1,100.00
- **Due date:** 2026-05-07

> The parent REQ record automatically reflects the aggregate state of its child RITMs. Once all RITMs are closed, the REQ state will update to Closed Complete without manual intervention.

<img width="1352" height="372" alt="07_req0010002_parent_approved" src="https://github.com/user-attachments/assets/a1200770-10f0-4396-90f1-d33f789ba381" />

*Fig 7 - Parent REQ0010002. Highlighted: both the "Approval" field and "Request state" field showing "Approved". The $1,100.00 price reflects the Standard Laptop catalog item cost.*

---

### Step 9 - Close an RITM as Complete

Open **RITM0010001** (the first Standard Laptop RITM that has progressed further in the workflow).

**Fields confirming closure:**
- **Stage:** Order Fulfillment
- **State:** Closed Complete
- **Assignment Group:** Hardware
- **Work Notes:** Laptop allocated, asset tagged, and prepared for delivery

**To close an RITM:**
1. Confirm all fulfilment actions are documented in Work Notes
2. Change **State** to `Closed Complete`
3. Click **Update**
4. The Stage will automatically move to `Order Fulfillment`

<img width="1346" height="623" alt="08_ritm0010001_closed_complete" src="https://github.com/user-attachments/assets/5831a648-2139-4b4e-8607-20863a0cdc92" />

*Fig 8 - RITM0010001 fully closed. Highlighted: Stage "Order Fulfillment" and State "Closed Complete". This is the target end state for every RITM once work is done and documented.*

---

### Step 10 - Validate Completion

Use the checklist below to confirm the lab is complete.

| Validation Check | Expected Result | Status |
|---|---|---|
| REQ record exists | REQ0010002 visible in Service Desk > Requests | - |
| REQ approval state | Shows "Approved" | - |
| RITM count | At least 3 RITMs exist under REQ0010002 | - |
| RITM assignment | Each RITM assigned to correct group (Hardware / Service Desk / Network Team) | - |
| Work Notes present | Each RITM has a fulfilment note in the Activity log | - |
| One RITM closed | RITM0010001 shows State = "Closed Complete" | - |
| Stage progression | Closed RITM shows Stage = "Order Fulfillment" | - |
| Parent REQ updates | REQ state reflects child RITM progress | - |

---

## Key Differences: Request vs Incident

```
REQUEST (REQ / RITM)                    INCIDENT (INC)
- Fulfilment work                       - Break-fix work
- User wants something new              - Something is broken
- Planned, deliverable-based            - Urgent restoration focus
- Follows approval workflow             - Follows investigation workflow
- Assigned by catalog item routing      - Assigned by support tier
- Closed when delivered                 - Closed when service restored
```

---

## Concepts Summary

**REQ - Request**
The parent container record. Created when a user submits a basket of items from the catalog. The REQ holds metadata like the requester, total price, due date, and overall approval state.

**RITM - Request Item**
One item from the catalog, represented as its own work record. Each RITM has its own assignment group, state, and activity log. This is where fulfilment agents do their work.

**Task**
An optional sub-task under an RITM for breaking fulfilment into smaller steps. Not always used - depends on the catalog item configuration.

**Incident**
A completely separate record type for service disruptions. Never use an incident to fulfil a request. Never use a request to log a break-fix issue.

---
