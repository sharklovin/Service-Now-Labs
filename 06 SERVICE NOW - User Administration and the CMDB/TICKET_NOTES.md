# Ticket Notes - Lab 07

> **Lab:** Lab 07 - User Administration and the CMDB
>
> **Module:** ServiceNow User Administration and Configuration Management Database
>
> **Completed:** May 2026

---

## User Record - Nnamso Mkpong

### Identity Fields

| Field | Value | Notes |
|---|---|---|
| **User ID** | shark007 | Login credential. Set at creation. Cannot be changed without admin intervention after first login. |
| **First name** | Nnamso | Used in display name and caller search. |
| **Last name** | Mkpong | Used in display name and caller search. |
| **Title** | Service Desk Analyst | Descriptive field. Used in user directory reports. |
| **Department** | IT | Links the user to the IT department for reporting and group membership rules. |
| **Email** | nnamsotechie@gmail.com | Receives all system notifications: SLA alerts, approval requests, ticket updates. |
| **Mobile phone** | +12224441123 | Optional contact field. Used by some notification policies for SMS alerts. |
| **Language** | English | Determines the language of the ServiceNow interface for this user. |
| **Calendar integration** | Outlook | Links ServiceNow scheduling to the user's Outlook calendar for change and task scheduling. |
| **Time zone** | System (America/Los_Angeles) | All timestamps on records created by this user will display in this time zone. |
| **Active** | true | Active: true is required for login. Active: false disables the account without deleting it. |
| **Identity type** | Human | Human identity type makes the user appear in all user-facing lookup fields (Caller, Assigned to, Approver). Non-human types (Integration User, Service Account) are excluded from these lookups. |
| **Password needs reset** | false | If set to true, the user is forced to change their password on next login. Use this for initial password provisioning. |
| **Locked out** | false | Locked out: true prevents login. ServiceNow locks accounts automatically after a configurable number of failed login attempts. |
| **Created** | 2026-05-01 02:08:30 | Auto-generated timestamp on record creation. |

---

### Role Assignment

| Field | Value | Notes |
|---|---|---|
| **Role** | itil | The standard service desk analyst role. Grants access to Incident, Problem, Change, CMDB, and all ITSM modules. |
| **State** | Active | The role is in effect immediately. A role in Requested state is pending approval and not yet active. |
| **Inherited** | false | Directly assigned to this user, not inherited from a group. Both direct assignment and group inheritance produce the same access - the difference is administrative (direct is harder to manage at scale; group inheritance is better for large teams). |
| **Inheritance count** | - | Shows how many groups contribute this role if Inherited is true. Not applicable here. |

---

### Caller Validation Result

Searched for "Nnamso" in the Caller field of a new incident form.

| Result | Value |
|---|---|
| **Found in search** | Yes |
| **Display name shown** | Nnamso Mkpong |
| **Email shown** | nnamsotechie@gmail.com |
| **Position in results** | First result |
| **Validation outcome** | Pass - account is fully operational and immediately usable as a caller |

---

## CI Record - *CAROL-IBM

### Identity and Asset Fields

| Field | Value | Notes |
|---|---|---|
| **Name** | *CAROL-IBM | Unique CI identifier in the CMDB. The asterisk prefix indicates this is a PDI sample data record. |
| **Asset tag** | P1000232 | Physical label on the device. Used for asset tracking and audit reconciliation. |
| **Serial number** | L3BB911 | Manufacturer-assigned unique identifier. Used to confirm the correct physical device is being worked on. |
| **Manufacturer** | Lenovo | Used for warranty lookups, support portal access, and hardware procurement. |
| **Model ID** | Lenovo ThinkStation S20 | Specific hardware model. Determines driver compatibility, hardware specs, and end-of-life date. |
| **Asset** | P1000232 - Lenovo ThinkStation S | Links to the Asset Management record for financial and lifecycle tracking. |
| **Company** | ACME North America | The organisation that owns this asset. In multi-company instances, this scopes the CI to the correct company. |
| **Assigned to** | Carol Coughlin | The person who uses this device. Used to correlate the CI with the caller on an incident. |

### Configuration Fields

| Field | Value | Notes |
|---|---|---|
| **Operating System** | Windows XP Professional | Determines which patches apply, which apps are compatible, and which support procedures are relevant. |
| **OS Version** | 5.1.2600 | Specific OS build. Windows XP version 5.1.2600 is the RTM/SP2 build. |
| **OS Service Pack** | Service Pack 2 | Indicates the patch level of the OS. Used by patch management to identify devices needing updates. |
| **RAM (MB)** | 1,534 | Total physical memory. Used for performance diagnostics. |
| **CPU manufacturer** | Intel | Used for driver and compatibility lookups. |
| **CPU speed (MHz)** | 798 | Clock speed of the processor. Used for performance benchmarking and upgrade decisions. |
| **CPU count** | 1 | Number of physical CPUs. |

### CI Class Hierarchy

```
Configuration Item
  Hardware
    Computer
      *CAROL-IBM
```

The CI Class hierarchy determines which fields are available on the CI record. Computer class CIs have fields for OS, CPU, RAM, and network configuration. A Server class CI would have additional fields for rack location, power requirements, and virtualisation. A Software CI would have fields for version, licence count, and installation path.

---

## Incident Record - INC0010030

### Header Fields

| Field | Value | Notes |
|---|---|---|
| **Number** | INC0010030 | Auto-assigned on form open. |
| **Caller** | Nnamso Mkpong | The new user account created in this lab, immediately usable as a caller. |
| **Configuration item** | *CAROL-IBM | The CI linked to this incident. Creates a bidirectional relationship in the CMDB. |
| **Short description** | Laptop not booting | Clear, specific description of the fault symptom. |
| **Opened** | 2026-05-03 07:21:17 | Timestamp when the incident form was first opened. |
| **Impact** | 3 - Low | Single user affected. |
| **Urgency** | 3 - Low | User can potentially use another device while this is resolved. |
| **Priority** | 5 - Planning | Calculated from Impact 3 + Urgency 3. Lowest active priority tier. |
| **State** | New | Initial state on creation. |
| **View** | Self Service | The incident was created using the Self Service view, which shows a simplified form layout. |

---

### Work Note Log

**Work Note 1**

| Field | Value |
|---|---|
| **Content** | CI record *CAROL-IBM linked. Device history reviewed. No prior incidents in the last 30 days. |
| **Type** | Work note (internal - not visible to caller) |
| **Purpose** | Audit evidence that the CI was linked and the CMDB history was consulted before investigation began |

**What this note tells a future analyst reading the record:**
- The CI link was intentional and verified (not auto-populated)
- The device history was actively checked, not assumed
- The 30-day clean history means the laptop fault is likely a one-off event, not a pattern of hardware failure
- The analyst followed the asset-aware support process before proceeding with diagnostics

---

## Before and After - CI Field on the Incident

### Before Linking (Screenshot 07)

```
Configuration item: [empty]
```

State: The incident is open, the caller is set, the short description is entered, but there is no connection to the physical device. If this incident were closed in this state, the CMDB would have no record that INC0010030 ever involved *CAROL-IBM.

### After Linking (Screenshot 08)

```
Configuration item: *CAROL-IBM
```

State: The incident is now linked to the CI. The *CAROL-IBM CI record will show INC0010030 in its Incidents related list. Any future incident involving the same device can reference this history.

---

## CMDB Relationship Behaviour

When a CI is linked to an incident in ServiceNow, the relationship is bidirectional and automatic:

**From the incident:** The Configuration item field shows the CI name. Clicking the info icon opens the CI record without leaving the incident.

**From the CI:** The Incidents related list at the bottom of the CI record shows every incident that has been linked to this CI. The list shows incident number, short description, state, opened date, and closed date. This is the complete support history of the device.

**No manual update is needed on the CI side.** Linking the CI on the incident automatically updates the CI's related list. This is ServiceNow's relational database working as designed - the link is stored once and rendered from both directions.

**The relationship persists after the incident is closed.** Closed incidents remain in the CI's Incidents related list permanently. This is what makes the CMDB a historical record rather than just a current-state snapshot.

---

## Key Observations on ServiceNow User Administration and CMDB Behaviour

**1. The itil role is additive, not restrictive.**
The itil role grants permissions. It does not remove any permissions the user already has. If a user later needs additional access (for example, the change_manager role to approve change requests), that role can be added alongside itil. Roles accumulate - the user's effective permissions are the union of all roles assigned.

**2. User records should be created before the first day.**
User account creation takes seconds, but propagation through notification rules, group membership, and access control checks can take a few minutes in larger instances. Creating accounts the day before start ensures the analyst can log in immediately on their first morning.

**3. The CMDB is only as accurate as the data that feeds it.**
In production, CI data is populated by ServiceNow Discovery (network scanning), by SCCM or Intune integration (endpoint management data), or by manual entry. Manually maintained CMDBs drift from reality quickly. Automated discovery is the only reliable way to keep CI data current at scale. The OS version, RAM, and CPU fields on *CAROL-IBM are only useful for support if they reflect the device's current state - if the device was upgraded from 4GB to 16GB RAM and the CMDB was not updated, the RAM field is misleading.

**4. CI names should follow a naming convention.**
The *CAROL-IBM naming pattern (asterisk + person name + manufacturer code) is the PDI sample data convention. In production, CI naming conventions encode meaningful information: WIN11-NM-04 encodes OS (Windows 11), location (NM = North Manchester), and device number (04). A consistent naming convention makes CI search faster and reduces the chance of linking the wrong CI to an incident.

**5. The Self Service view hides fields that the full ITIL view shows.**
INC0010030 was created using the Self Service view, which presents a simplified form for end users. The Configuration item field is visible in Self Service view, but some fields (Category, Subcategory, Assignment group) are hidden. The ITIL view (switchable via the view selector at the top of the form) shows all fields. Analysts should work in the ITIL view to ensure they can set all relevant fields.

**6. Work notes on an incident are visible to the entire support team.**
Any member of the assignment group, any manager with the correct role, and any admin can read all work notes on an incident. Work notes are not private to the analyst who wrote them. Sensitive information (passwords, personal health information, disciplinary context) must never be added to work notes.

**7. The Caller field and the Assigned to field serve different purposes.**
Caller is who reported the problem. Assigned to is who is working the problem. They are often different people. Setting Caller correctly ensures the right person's contact details are on the incident and that the incident appears in the correct user's history. Setting Assigned to correctly ensures the ticket appears in the right analyst's work queue.
