# Navigate the ServiceNow Interface and Create Your First Incident

> **Author:** Nnamso Mkpong
>
> **Domain:** ServiceNow - Incident Management, Core Navigation, Personal Developer Instance
>
> **Environment:** ServiceNow Personal Developer Instance (PDI) - developer.servicenow.com
>
> **Completed:** April 2026

---

## Objective

Log into a ServiceNow Personal Developer Instance, explore the core navigation elements, and create, categorise, and save a complete incident ticket from scratch. Demonstrate that the Incident module, all required fields, assignment routing, and work note logging all work end to end before taking a live call.

---

## Business Scenario

> **First Day on the Service Desk - 18 April 2026**
>
> You have just joined a service desk team that uses ServiceNow as its ITSM platform. Before you take your first live call, your team lead asks you to log into the system, find the Incident module, and create a test ticket to confirm you know where everything is. The test incident is a real scenario: a user called Abel Tuter has reported that Outlook will not open after this morning's system update. You need to fill in every required field correctly, assign the ticket to the Service Desk group, save it, and then update the state to In Progress with a work note showing you have begun investigating.

This lab is the foundation for everything else in ServiceNow. Every workflow, every escalation, every SLA, and every report starts with an incident being logged correctly. If the first record is wrong - wrong category, wrong priority, wrong assignment group - every downstream action built on it is also wrong. Getting this right the first time is not pedantic. It is how the system is supposed to work.

---

## Environment and Tools Used

| Component | Detail |
|---|---|
| **Platform** | ServiceNow Personal Developer Instance (PDI) |
| **Instance URL** | dev294020.service-now.com |
| **Account type** | System Administrator |
| **Incident created** | INC0010002 |
| **Caller** | Abel Tuter |
| **Category** | Software - Email |
| **Assignment Group** | Service Desk |
| **Final State** | In Progress |

---

## Understanding Priority Calculation in ServiceNow

> **Priority in ServiceNow is not a field you set manually. It is calculated automatically from Impact and Urgency. Understanding this prevents one of the most common first-day mistakes.**

```
IMPACT
  Definition: How many people or business functions are affected
  1 - High:   Entire organisation or critical business function
  2 - Medium: Department or multiple users
  3 - Low:    Single user or minor function

URGENCY
  Definition: How quickly the issue needs to be resolved
  1 - High:   Cannot work at all - no workaround available
  2 - Medium: Reduced capability - workaround exists
  3 - Low:    Minor inconvenience - workaround is comfortable

PRIORITY MATRIX
  Impact 1 + Urgency 1 = Priority 1 - Critical
  Impact 1 + Urgency 2 = Priority 2 - High
  Impact 2 + Urgency 1 = Priority 2 - High
  Impact 2 + Urgency 2 = Priority 3 - Moderate
  Impact 3 + Urgency 1 = Priority 3 - Moderate
  Impact 3 + Urgency 3 = Priority 5 - Planning

KEY RULE
  Set Impact and Urgency based on what the user tells you.
  Let the system calculate Priority.
  Never override Priority manually unless you have explicit authorisation.
```

In this lab, Impact was set to 3 - Low (one user affected) and Urgency was set to 1 - High (Outlook completely unusable). The system calculated Priority 3 - Moderate. That is the correct outcome for a single user who cannot use their email client at all.

---

## Steps Performed

---

### Phase 1 - Access the ServiceNow Personal Developer Instance

**Step 1.1 - Register and Log Into the PDI**

Register at developer.servicenow.com and request a free Personal Developer Instance. Once provisioned, log in using the admin credentials provided in the registration email. The instance URL follows the format dev[number].service-now.com.

<img width="1359" height="717" alt="01 SERVICE NOW PDI DAsh board" src="https://github.com/user-attachments/assets/0873f854-5078-4dbc-813b-f45a444cc40d" />


> **Red highlight:** The address bar shows the PDI instance URL - dev294020.service-now.com. This is your unique instance. No one else shares it. Every record, workflow, and configuration change you make here is isolated to this instance.
>
> **Blue highlight:** The user profile dropdown shows the System Administrator role and the Log out option. This confirms you are logged in with admin rights, which gives you access to all modules including Admin-only configuration. On a production instance, admin rights are restricted. On the PDI, they are open by default.

---

### Phase 2 - Navigate to the Incident Module

**Step 2.1 - Find the Incident List Using the All Menu**

Click All in the top navigation bar. Navigate to Service Desk then Incidents. The incident list view opens showing all active incidents in the system. Observe the columns: Number, Opened, Short description, Caller, Priority, State, Category, Assignment group, Assigned to, Updated, Updated by.

<img width="1363" height="634" alt="02 incident view list" src="https://github.com/user-attachments/assets/c17bb46c-3bf2-4e8e-a39e-5ff498c13ecf" />


> **Green highlight:** The New button in the top right of the list creates a new incident. This is how every ticket starts.
>
>
> The list shows 40 incidents, 1 to 20 of 40. ServiceNow paginates by default. The filter bar at the top and the column headers are both clickable - you can sort by any column or add filters to narrow the list.

---

### Phase 3 - Open the Blank Incident Form

**Step 3.1 - Click New to Open a Fresh Incident Record**

Click the New button. A blank incident form opens. The system has already assigned an INC number - INC0010002. This number is reserved the moment the form opens. If you close without saving, the number is released and reassigned to the next ticket.

<img width="1349" height="682" alt="03 blank incidient form" src="https://github.com/user-attachments/assets/ac48c392-4bca-487d-a6d6-09764ae74892" />


> **Red highlight:** The Caller field and Short description field both show a red asterisk. These are the two minimum required fields. ServiceNow will not let you submit without them.
>
> **Orange highlight:** The Priority field shows 5 - Planning in grey. This is the default before Impact and Urgency are set. It is a calculated read-only field. You cannot click into it and type a number. Changing Impact or Urgency will change this value automatically.
>
> The default Category is Inquiry / Help. The default State is New. These are correct starting values - the form is pre-populated with the most common baseline so you only need to change what is different about this specific incident.

---

### Phase 4 - Complete the Incident Form

**Step 4.1 - Fill in All Required and Relevant Fields**

Work through the form left to right, top to bottom. Start with Caller because the system uses the caller's department and location to suggest relevant fields. Then set Category, Subcategory, Assignment Group, Impact, Urgency, and Short description.

Fields completed:

| Field | Value | Reason |
|---|---|---|
| **Caller** | Abel Tuter | The user who reported the issue - found using the search icon |
| **Category** | Software | Outlook is a software application |
| **Subcategory** | Email | Outlook is specifically the email client |
| **Assignment Group** | Service Desk | First-line team handles software issues before escalation |
| **Impact** | 3 - Low | Single user affected |
| **Urgency** | 1 - High | User cannot use Outlook at all - no workaround |
| **Priority** | 3 - Moderate | System calculated from Impact 3 + Urgency 1 |
| **Short description** | Outlook will not open after this morning update | Specific and searchable - includes the cause context |

<img width="1359" height="493" alt="04 completed incident form" src="https://github.com/user-attachments/assets/41856909-3154-43bc-a927-da62e434e8b3" />


> **Green highlights:** Caller (Abel Tuter), Category/Subcategory (Software/Email), and Assignment Group (Service Desk) are all set. These three fields together determine where the ticket goes and who works it.
>
> **Orange highlight:** Priority shows 3 - Moderate. This was calculated automatically when Urgency was changed to 1 - High while Impact remained 3 - Low. The system did the arithmetic. No manual override was needed or appropriate.
>
> **Blue highlight:** Short description reads "Outlook will not open after this morning update." This is specific enough to be useful in a search and descriptive enough that a technician reading it knows exactly what they are walking into.

---

### Phase 5 - Save the Incident

**Step 5.1 - Submit the Form and Confirm the INC Number**

Click Submit to save the incident. ServiceNow saves the record and returns you to the incident list. INC0010002 appears at the top of the list with all fields correctly populated.

<img width="1361" height="226" alt="05 incident saved in queue" src="https://github.com/user-attachments/assets/f103187e-b346-494d-8997-109e87d032de" />


> **Green highlight:** INC0010002 is visible in the list. Every field shows correctly: Opened 2026-04-18 07:45:58, Short description "Outlook will not open after this morning update", Caller Abel Tuter, Priority 3 - Moderate, State New, Category Software, Assignment group Service Desk. The ticket is in the system and routable.
>
> At this point the incident exists as a formal record. If a technician opens the All Open queue and filters by Assignment group = Service Desk, this ticket will appear. The assignment group routing is what gets it to the right team.

---

### Phase 6 - Search for the Incident by INC Number

**Step 6.1 - Use the Column Search to Find INC0010002**

In the incident list, use the Number column filter to search for INC0010002. The filter applies and the view narrows to a single result. The breadcrumb at the top confirms the active filter: All > Active = true > Number = INC0010002.

<img width="1362" height="302" alt="06 Incident search result" src="https://github.com/user-attachments/assets/fa133b2e-2797-4624-af67-6739016721bc" />


> **Orange highlight:** The breadcrumb filter shows the active search criteria. Number = INC0010002. This is one of two ways to find a specific ticket - column filter or the top search bar. The column filter stays within the incident module. The top search bar searches across all record types.
>
> **Blue highlight:** The State column now shows In Progress. This reflects the status update performed in the next step - the screenshot was captured after the state change. The updated timestamp has moved to 2026-04-18 07:58:07, showing the exact moment the state was changed.

---

### Phase 7 - Update State to In Progress and Add a Work Note

**Step 7.1 - Open the Ticket, Change State, and Document the Investigation Start**

Open INC0010002. Change State from New to In Progress. In the Activity section at the bottom of the form, select Work notes and add a note explaining what investigation has started. Click Update to save.

Work note added:
> Investigation started. Checking Outlook logs and update history.

<img width="1117" height="424" alt="07 activity log in progress" src="https://github.com/user-attachments/assets/14361f3f-b941-4634-912c-45d87f05c6a1" />


> **Green highlight:** The most recent work note reads "Investigation started. Checking Outlook logs and update history." timestamped 2026-04-18 07:58:07. This is the active investigation note - it tells anyone who picks up this ticket exactly where the investigation is.
>
> **Orange highlight:** The field change entry directly below records "Incident state: In Progress was New." This is the audit trail. ServiceNow logs every field change automatically. You cannot edit or delete this entry. It is permanent. The timestamp matches the work note above - both changes happened in the same Update action.
>
> **Blue highlight:** The earlier work note at 07:54:23 reads "User reports Outlook not opening after system update this morning. Issue requires investigation." This was added when the ticket was first saved. Together, the two work notes tell the story of the ticket: first contact, then investigation start.

---

## Before and After Comparison

### Before - Incident Not Yet Created

| What existed | What was missing |
|---|---|
| A user with a problem | Any formal record of the problem |
| A verbal report from Abel Tuter | A ticket number to reference |
| Knowledge that Outlook was broken | Category, priority, assignment routing |
| No visibility for the team | No SLA clock running |

Without a ticket, the problem is invisible to the rest of the team. There is no way to track it, no SLA timer, no assignment routing, and no audit trail. If Abel Tuter calls back in two hours, whoever answers has no record of the first call.

---

### After - INC0010002 Created and In Progress

| Field | Value | What it enables |
|---|---|---|
| **Number** | INC0010002 | Unique reference for all communications |
| **Caller** | Abel Tuter | Contact and department linked to the record |
| **Category** | Software - Email | Correct routing and reporting |
| **Assignment Group** | Service Desk | Appears in the right team's queue |
| **Priority** | 3 - Moderate | SLA timer started at the correct tier |
| **State** | In Progress | Team knows someone is working it |
| **Work notes** | 2 entries | Audit trail and investigation log |

The ticket is now a formal record. Abel Tuter can be given the INC number as a reference. The Service Desk queue shows the ticket. SLA is running. Any team member who picks it up can read the work notes and continue without a briefing.

---

## The Activity Log as an Audit Trail

Every change made to a ServiceNow incident is recorded in the Activity section. This includes field changes, work notes, comments, attachments, and approvals. The activity log is append-only - no one can edit or delete an entry once it is saved.

This matters for several reasons. In a support context, the activity log is the evidence that work was done. If a user escalates and asks why it took three days to resolve their incident, the activity log shows exactly what happened and when. In a compliance context, the audit trail is the record that proves the process was followed.

The two types of entries in the activity log are:
- Work notes - visible to the support team only, not to the caller
- Comments - visible to the caller if they have portal access

In this lab, both entries were work notes. The caller (Abel Tuter) cannot see them. If you need to send the caller an update, use Comments instead of Work notes.

---

## Help Desk Ticket Notes

See `TICKET_NOTES.md` in this folder for field-by-field notes on INC0010002, the priority calculation walkthrough, and observations on ServiceNow form behaviour that are worth knowing before logging a live incident.

---

## Outcome and Validation

| Check | Result |
|---|---|
| ServiceNow PDI accessed with admin credentials | Pass |
| Incident module found via All menu navigation | Pass |
| Blank incident form opened using New button | Pass |
| Caller set to Abel Tuter | Pass |
| Category set to Software, Subcategory to Email | Pass |
| Assignment Group set to Service Desk | Pass |
| Priority calculated as 3 - Moderate from Impact 3 + Urgency 1 | Pass |
| Short description set to specific realistic description | Pass |
| Incident saved as INC0010002 | Pass |
| INC0010002 visible in incident list with correct fields | Pass |
| Incident found using column number filter | Pass |
| State changed from New to In Progress | Pass |
| Work note added documenting investigation start | Pass |
| Activity log shows both work notes and field change entry | Pass |
| All field changes timestamped and immutable in audit trail | Pass |

---

## What I Learned

1. **Priority is calculated, not entered.** The Priority field is read-only in ServiceNow. Setting Impact to 3 - Low and Urgency to 1 - High produced Priority 3 - Moderate automatically. This is the matrix working as designed. Agents who try to manually set priority by editing the field discover it is greyed out for a reason.

2. **The INC number is reserved the moment the form opens.** INC0010002 was assigned before a single field was filled in. Closing without saving releases the number but the gap in the sequence remains. This is why ServiceNow incident numbers are not perfectly sequential in live environments - abandoned forms leave gaps.

3. **Work notes and comments are different things.** Work notes are internal. Comments are customer-facing. Both appear in the Activity section but with different icons and visibility rules. Adding a sensitive investigation note as a Comment instead of a Work note would expose it to the caller via the portal. This is a real mistake that happens on first-day tickets.

4. **The assignment group is what routes the ticket, not the individual assignee.** Setting Assignment group to Service Desk puts the ticket in the Service Desk team's queue, visible to everyone in that group. Assigned to is optional at creation - it gets filled in when a specific person picks up the work. A ticket with no Assigned to but a correct Assignment group is in the right queue. A ticket with no Assignment group is invisible to any team.

5. **The activity log cannot be edited.** Every field change is logged automatically and permanently. This is not just a feature - it is a compliance requirement. The immutable audit trail is what makes ServiceNow records admissible as evidence of work done in regulated environments.

6. **Searching by INC number in the column filter stays within the Incident module.** Using the top search bar across ServiceNow searches all record types. If you type INC0010002 in the top bar, you might get results from Change requests or Problems with similar numbers. The column filter in the Incident list is faster and more precise for finding a specific incident.

---

## Real World Relevance

The ability to log an incident correctly in ServiceNow is the baseline skill for every service desk role that uses the platform. But the deeper skill this lab demonstrates is understanding why each field exists and what it does to the record downstream. Category and Subcategory drive reporting. Assignment Group drives routing and SLA. Priority drives escalation thresholds. Work notes drive audit compliance.

In organisations using ServiceNow at enterprise scale, a poorly logged incident creates problems that compound over time. Wrong category means the monthly incident report shows the wrong distribution of issue types. Wrong assignment group means the SLA is tracked against the wrong team. Missing work notes means no audit trail if the ticket is escalated or disputed.

A service desk analyst who understands the form - not just how to fill it in but why each field matters - is the one who gets trusted with more complex workflows, escalation handling, and eventually configuration responsibilities. This lab is the starting point for all of that.

---

## Troubleshooting Reference

| Situation | Correct Action | Common Mistake |
|---|---|---|
| Priority field is greyed out and cannot be edited | This is correct - Priority is calculated from Impact and Urgency. Change those fields instead | Trying to click into the Priority field and type a number |
| Caller field search returns no results | Type the first name only, not the full name. ServiceNow user search is first-name first | Typing the full name with exact capitalisation and getting no matches |
| Ticket saved but not visible in the incident list | Check the active filter at the top of the list - the list may be filtered to a different state or assignment group | Assuming the ticket was not saved when it actually exists outside the current filter |
| Work note added but visible to the caller | Check that Work notes tab is selected in the Activity section, not Comments. Comments are customer-visible | Adding internal investigation notes as Comments and having the caller see them via the portal |
| State will not change to In Progress | Click Update after changing the State dropdown - ServiceNow does not auto-save on field change | Changing the State dropdown and navigating away without clicking Update |
| INC number gap in the sequence | Normal behaviour - form was opened and closed without saving. The reserved number is released but the sequence moves forward | Assuming a number gap means a record was deleted |
| Assignment group showing empty after save | The field was cleared before Submit. ServiceNow does not warn on empty non-required fields. Re-open and set the Assignment group then click Update | Submitting without assignment group and not noticing until the ticket is missing from all team queues |
