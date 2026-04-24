# Ticket Notes - Lab 01: Navigate the ServiceNow Interface and Create Your First Incident

> These notes document INC0010002 field by field, the decisions made during the lab, and the observations worth keeping before logging a live incident in ServiceNow. Written as a real handover document - specific enough to be useful on a Monday morning when someone else picks up this ticket.

---

## Incident Record - INC0010002

**Short description:** Outlook will not open after this morning update
**Caller:** Abel Tuter
**Category:** Software
**Subcategory:** Email
**Assignment Group:** Service Desk
**Assigned to:** (empty - not yet assigned to an individual)
**Impact:** 3 - Low
**Urgency:** 1 - High
**Priority:** 3 - Moderate (calculated)
**State:** In Progress
**Opened:** 2026-04-18 07:45:58
**Last updated:** 2026-04-18 07:58:07
**Updated by:** admin

---

## Field-by-Field Notes

---

**Number - INC0010002**

The INC number was assigned automatically when the New button was clicked and the blank form opened. It is not editable. In a production environment with high ticket volume, INC numbers increment fast. The number itself carries no meaning about severity or content - it is purely a unique identifier for reference and search.

One thing worth knowing: if you open a new incident form and then close the browser tab without saving, the INC number that was reserved is not reused. The next ticket gets the next number. This is why production systems show gaps in the INC sequence. It is not a sign that records were deleted.

---

**Caller - Abel Tuter**

The Caller field was populated by typing "Abel" into the search box and selecting Abel Tuter from the results. ServiceNow searches the Users table when you click the magnifying glass. The search is first-name-first and partial - typing three or four characters is usually enough to narrow the results.

The Caller field matters for two reasons. First, it links the incident to a person record, which pulls in the caller's department, location, and contact information. This data can be used in reports - for example, which department has the most incidents this month. Second, if the caller has a portal account, linking them to the ticket is what allows them to see updates and close the ticket themselves.

Abel Tuter is a test user that comes pre-loaded in most ServiceNow PDI instances. Using a pre-loaded test user avoids having to create a user record before logging the first incident.

---

**Category - Software / Subcategory - Email**

Category was set to Software. Subcategory was set to Email. The category selection changed the available subcategory options - subcategory is dependent on category. If you select Hardware, the subcategory list changes to hardware-related options. If you select Software, you get software-related options including Email, OS, Application.

The correct category for an Outlook issue is Software because Outlook is a software application. The correct subcategory is Email because the specific application affected is the email client. If the issue were a corrupted Word document, the category would still be Software but the subcategory would be something like Office Suite or Application depending on what your organisation has configured.

Category and subcategory drive the Monthly Incident Report breakdown. If this ticket were categorised as Inquiry / Help instead of Software, the reporting would show fewer software incidents than actually occurred. Over time, miscategorised tickets make the data unreliable.

---

**Assignment Group - Service Desk**

Set to Service Desk. This is the first-line team. The assignment group is the field that makes the ticket visible in a team's queue. Once saved, any agent in the Service Desk group who filters the incident list by Assignment group = Service Desk will see this ticket.

The Assigned to field was left empty. This is correct at this stage. When a ticket arrives in the queue, it is unassigned within the group. An agent picks it up and assigns it to themselves by clicking Assign to me or by entering their name in the Assigned to field. Leaving it empty at creation means it waits in the shared queue rather than going directly to an individual who may be busy or absent.

In organisations with high ticket volume, tickets that are assigned to an individual rather than a group are a queue management problem. If the person is off sick, the ticket sits unseen. If it is in the group queue, any available agent can pick it up.

---

**Impact - 3 Low**

Single user affected. Abel Tuter cannot open Outlook but no one else has reported the same issue. The impact assessment is based on what the caller reports at the time of logging. If two more users call in the next hour with the same problem, the incident can be escalated and the impact changed to 2 - Medium or 1 - High.

Impact assessment at first contact is always based on available information. Setting it too high inflates priority and consumes SLA resources unnecessarily. Setting it too low risks missing a wider outage. 3 - Low for a single-user Outlook issue is the correct baseline.

---

**Urgency - 1 High**

The user cannot open Outlook at all. There is no workaround - they cannot access their email through any other means in this scenario. Urgency 1 - High is correct because the user's ability to work is fully blocked, not reduced.

If the user had said "Outlook is slow but opens eventually", urgency would be 2 - Medium because a workaround exists (wait longer). If they had said "Outlook sometimes shows a warning but I can dismiss it and carry on", urgency would be 3 - Low. The urgency decision hinges on whether the user can still function.

---

**Priority - 3 Moderate (calculated)**

Impact 3 + Urgency 1 = Priority 3 Moderate. This is the ServiceNow priority matrix result for a single high-urgency user. The Priority field is read-only. It updated automatically when Urgency was changed to 1 - High.

Priority 3 - Moderate typically means the SLA target is something like 8 business hours for first response and 24 hours for resolution, though this varies by organisation. The SLA clock started when the ticket was saved at 07:45:58.

---

**Short Description - Outlook will not open after this morning update**

This description was chosen deliberately. A short description should tell a technician three things: what is broken, who or what is affected, and if known, the trigger. "Outlook will not open" tells them what is broken. "After this morning update" tells them the likely trigger. Together, a technician reading this description knows to check the Windows Update history and Outlook repair options before they even open the caller's full description.

A short description like "Email problem" or "Software issue" fails all three tests. It tells the technician almost nothing before they open the ticket.

The short description is also what appears in the incident list view, email notifications, and reports. It needs to be searchable. "Outlook will not open after this morning update" will surface if someone searches for "Outlook" or "update". "Software issue" will not help with either search.

---

## Work Notes Recorded

---

**Work note 1 - 2026-04-18 07:54:23 - Added at first save**

> User reports Outlook not opening after system update this morning. Issue requires investigation.

This note was added when the incident was first submitted. It documents what the caller said in their own terms. The purpose of this note is to preserve the original report before any investigation has changed the framing. If the investigation later reveals the cause is something else entirely, this note still shows what the user originally described.

Added as a Work note, not a Comment. The caller cannot see it.

---

**Work note 2 - 2026-04-18 07:58:07 - Added when state changed to In Progress**

> Investigation started. Checking Outlook logs and update history.

This note was added at the same time as the state change from New to In Progress. Both changes were saved together using the Update button. The activity log shows them at the same timestamp - 07:58:07.

The note is brief and specific. It tells anyone reading the ticket where the investigation is going. "Checking Outlook logs and update history" means checking the Windows Event Viewer for Outlook errors and looking at Windows Update history to identify what was installed overnight. That is a specific plan. A note that says "looking into it" is not a plan.

---

## Activity Log Observations

The activity log for INC0010002 shows four entries in reverse chronological order:

1. Work note at 07:58:07 - Investigation started
2. Field change at 07:58:07 - Incident state: In Progress was New
3. Work note at 07:54:23 - User reports Outlook issue
4. Field change at 07:54:23 - Impact, Incident state New, Opened by System Administrator, Priority 3 Moderate

Entry 4 is the creation record. ServiceNow logs the initial field values when a ticket is first saved. This is how you know what the ticket looked like when it was created even if someone later changes fields. The original Impact (3 - Low) and Priority (3 - Moderate) are preserved in the audit trail even if someone later changes them.

The audit trail is write-once. Nothing in the activity log can be deleted or edited after saving. This is what makes it usable as evidence.

---

## PDI Navigation Notes

**All menu** - The main navigation. Clicking All opens a full application tree showing every module available to your role. Service Desk > Incidents is the path to the incident list. The menu is searchable - typing "Incident" in the filter at the top of the All menu narrows the list.

**Favorites** - Starred modules appear here. After navigating to Incidents via the All menu, you can star it to add it to Favorites for faster access. On a live service desk, Incidents and the relevant queue views are typically starred.

**History** - Shows recently visited records and modules. Useful for returning to a ticket you had open earlier without searching for it again.

**Top search bar** - Searches across all record types. Typing INC0010002 here returns the incident. Typing a user's name returns their user record, any incidents they are the caller on, and any other records linked to them. It is a global search, not a module-specific one.

**User profile icon** - Top right. Opens the profile menu showing your current role, instance name, and options including Impersonate user (useful for testing portal views as a non-admin user) and Elevate role (used when you need to access elevated permissions temporarily).

---

## Things Worth Knowing Before a Live Incident

**Save frequently if you are adding a long description.** ServiceNow does not auto-save form content. If the browser crashes or the session times out while you are writing a detailed description, the content is lost. Write detailed notes in a text editor and paste them in, or save the ticket with minimal content first and then update it.

**The form header changes when you submit.** Before submit, the header says "New record." After submit, it shows the INC number and the Update button replaces Submit. If you see Submit still showing, the ticket has not been saved yet.

**Clicking Resolve instead of Update permanently changes the state.** The Resolve button transitions the incident to Resolved state and starts the reopen timer. If you click it by mistake, you can change the State back to In Progress but it leaves a state change entry in the audit log. On a live ticket, an accidental Resolve is visible to the caller if they have portal access.

**The Assignment Group and Assigned to fields behave differently.** Clearing the Assignment Group removes the ticket from all team queues - it becomes invisible to everyone. Clearing Assigned to keeps the ticket in the group queue as unowned. Always double-check Assignment Group is set before saving.

**Work notes are visible to other agents but not to the caller.** Customer-visible updates go in Comments. If you need to ask the caller for more information via the portal, use Comments. If you are documenting your investigation for the team, use Work notes.

---

*Nnamso Mkpong - Lab 01 - ServiceNow IT Service Desk Series*
