# Ticket Notes - Lab 08

> **Lab:** Lab 08 - Run a Report and Export Evidence for a Weekly SLA Review
>
> **Module:** ServiceNow Reports
>
> **Completed:** May 2026

---

## Report 1 - Weekly Incident Volume by Priority

### Data Step Configuration

| Field | Value | Notes |
|---|---|---|
| **Report name** | Weekly Incident Summary (initial) - renamed to Weekly Incident Volume by Priority | Renamed after bar chart conversion to reflect specific content |
| **Source type** | Table | Standard for all ITSM reports - not a joined or scripted source |
| **Table** | Incident [incident] | Primary incident table. All incident volume, state, priority, and caller data lives here. |

### Type Step

| Initial type | Final type | Why changed |
|---|---|---|
| List | Bars | List used for data verification. Bars used for the presentation version showing priority distribution visually. |

### Configure Step - Columns Selected

| Column | Purpose |
|---|---|
| Number | Unique incident identifier. Used to reference specific incidents in the service review. |
| Opened | Date the incident was raised. Drives the date filter. |
| Short description | What the incident is about. Essential for the service review audience to understand what is in the queue. |
| Caller | Who reported the incident. Useful for spotting repeat callers or VIP incidents. |
| Priority | P1/P2/P3/P4 classification. The primary grouping field for the bar chart. |
| State | New, In Progress, On Hold, Resolved, Closed. Shows how much of the queue is still open. |
| Category | Network, Software, Hardware, etc. Shows where the volume is coming from by service type. |
| Assignment group | Which team owns each incident. Shows workload distribution. |
| Assigned to | The individual analyst. Useful for identifying overloaded team members. |
| Updated | When the record was last changed. Flags stale incidents that have not been touched. |
| Updated by | Who made the last change. Audit field. |

### Filter Condition

| Field | Operator | Value | Behaviour |
|---|---|---|---|
| Opened | at or after | This week | Dynamic - recalculates from Monday 00:00:00 of the current calendar week on every report run |

**Why "at or after" not "after":** The "at or after" operator is inclusive of the exact boundary moment (Monday 00:00:00). "After" would exclude incidents opened at exactly that moment. For a complete weekly summary, "at or after" captures the full week from its first second.

**Why "This week" not a hardcoded date:** Dynamic relative date values are the foundation of reusable reports. "This week" means the same report returns the correct data every week without maintenance. Alternatives available in ServiceNow: Last week, Last 7 days, This month, Last 30 days, This quarter, Last year.

### Results Summary

| Metric | Value |
|---|---|
| Total incidents returned | 72 |
| Page size | 20 per page (pagination: 1 to 20 of 72) |
| Dominant priority in list | Priority 1 - Critical |
| States observed in first rows | Closed, On Hold, In Progress |
| First three callers | Fred Luddy (x2), Joe Employee |
| First three categories | Network (all three) |
| Bar chart - tallest bar | ~43 incidents |
| Bar chart - second bar | ~28 incidents |

---

## Report 2 - SLA Breached Incidents

### Data Step Configuration

| Field | Value | Notes |
|---|---|---|
| **Report name** | SLA Breached Incidents | Clearly identifies this as a compliance/breach report |
| **Source type** | Table | Standard |
| **Table** | Task SLA [task_sla] | The SLA tracking table - completely separate from Incident [incident] |

### Why Task SLA [task_sla] Not Incident [incident]

The Task SLA table stores one row per SLA agreement per task. It is the only table in ServiceNow that contains:
- Has breached (boolean)
- Business elapsed percentage
- Business time left
- Stage (Achieved/Breached/In Progress/Completed/Cancelled)
- SLA definition name and type

None of these fields exist on the Incident table. A report on the Incident table cannot show SLA compliance data.

### Filter Condition

| Field | Operator | Value | Notes |
|---|---|---|---|
| Has breached | is | true | Boolean - returns only records where the SLA deadline passed without resolution. Automatically set by the ServiceNow SLA engine. |

**Section label visible in screenshot:** "TASK SLA CONDITIONS" - confirms the filter is in the Task SLA table context, not the Incident table context.

### Task SLA Table - Key Fields Reference

| Field | Description | Values |
|---|---|---|
| Task | Linked incident/change number | INC0000060, CHG0030007, etc. |
| SLA definition | Name of the SLA agreement | Priority 1 resolution (1 hour), Network group resolution, etc. |
| SLA definition Type | The contractual tier | SLA, OLA (Operational Level Agreement), UC (Underpinning Contract) |
| SLA definition Target | What is being measured | Resolution, Response |
| Stage | Current SLA status | In Progress, Achieved, Breached, Completed, Cancelled |
| Business time left | Remaining time before breach | 0 Seconds = deadline passed |
| Business elapsed time | Actual time consumed | 1 Day 38 Minutes, 19 Hours 16 Minutes, etc. |
| Business elapsed percentage | Actual time as % of target | 100% = met exactly, over 100% = breached |
| Start time | When the SLA clock started | Usually when incident opened or priority set |
| Stop time | When the SLA clock stopped | When resolved, cancelled, or SLA met |

### Notable Records in the SLA Breach Report

**INC0000060 - Three SLA records, two breached**

This single incident has three rows in the Task SLA report, demonstrating that one incident can breach multiple SLA tiers simultaneously.

| SLA definition | Type | Stage | Elapsed time | Elapsed % | Analysis |
|---|---|---|---|---|---|
| Priority 3 resolution (1 day) | SLA | Achieved | 9 Hours | 37.5% | Internal SLA met with 15 hours to spare |
| SAN 001 contract resolution (3.5 hour) | Underpinning Contract | Breached | 1 Day 38 Minutes | 704.1% | Vendor SLA violated - 7x the contracted 3.5-hour target |
| Network group resolution | OLA | Breached | 19 Hours 16 Minutes | 482.07% | OLA violated - 4.8x the operational target |

The pattern here is significant: the internal team met their SLA (Priority 3 within 1 day) but the contractual obligations with the vendor (UC) and the operational agreement with the Network group (OLA) were both severely violated. This points to a supplier or routing issue, not a front-line analyst performance issue.

**INC0008111 - Data quality flag**

| SLA definition | Stage | Elapsed time | Elapsed % | Analysis |
|---|---|---|---|---|
| Priority 3 resolution (1 day) | Completed | 661 Days 14 Hours 54 Minutes | 66,162.13% | Extreme outlier - requires investigation |

An elapsed percentage of 66,162% means this incident remained open in ServiceNow for 661 days against a 1-day SLA target. This is almost certainly a data quality issue - the physical work was completed but the ServiceNow record was never closed. This record should be opened, closed with appropriate notes (actual resolution date, close code, closure notes), and the SLA record should be reviewed for reporting accuracy.

---

## PDF Export - Full Metadata Reference

| Metadata field | Value | Purpose |
|---|---|---|
| Report Title | SLA Breached Incidents | Identifies the report |
| Run Date and Time | 2026-05-06 02:42:14 Pacific Daylight Time | Timestamp - critical for audit chain of custody |
| Run by | System Administrator | Username of whoever generated the export |
| Table name | task_sla | Confirms the data source |
| Group by | Active | The grouping applied at export time |
| Sort Order | Active in ascending order | The row sort sequence |
| Record count | 24 Task SLAs | Total number of records in the export |

The Run Date and Time combined with Run by is the chain of custody. Together they prove who pulled the data and when. This is what makes the PDF export legally and operationally useful as evidence - without it the document is a table of numbers with no verifiable origin.

---

## Analyst Summary Sentence Map

| Sentence | ITIL topic | Data source |
|---|---|---|
| "A total of 72 incidents..." | Total volume and priority distribution | Weekly Incident Volume by Priority report |
| "The SLA breach report...returned 24 records..." | SLA compliance and breach count | SLA Breached Incidents report |
| "The Priority 1 volume and breach count...suggest..." | Trend observation and capacity signal | Synthesis of both reports |
| "It is recommended that the team lead reviews..." | Recommended investigative action | Standard SLA breach investigation process |
| "As an immediate action..." | Immediate operational response | Prioritisation and SLA proximity review |

---

## Report Type Decision Guide

```
USE A LIST WHEN
  The audience needs to see individual records for follow-up
  The purpose is to identify specific incidents to action
  The report will be exported and reviewed record by record
  Examples: SLA breach list, open P1 incidents, unassigned queue

USE BARS WHEN
  The audience needs to compare volumes across categories
  The purpose is to show distribution across a discrete field
  The report will be shown on screen in a meeting
  Examples: Incidents by priority, incidents by state, volume by team

USE PIE WHEN
  The audience needs proportions of a whole
  There are 5 or fewer categories
  Examples: Category distribution, source of incidents

USE LINE WHEN
  The audience needs to see how a metric changes over time
  Week-over-week or month-over-month trend is the goal
  Examples: Weekly incident volume over 12 weeks, avg resolution time

USE SINGLE SCORE WHEN
  One number needs to be prominently displayed on a dashboard
  The metric has a clear KPI threshold
  Examples: Open P1 count, SLA compliance %, CSAT score
```

---

## Key Observations on ServiceNow Reporting Behaviour

**1. The "This week" filter uses the instance timezone, not the user timezone.**
If the instance is US Pacific and the user is in Nigeria (WAT, UTC+1), "This week" starts at Monday 00:00 Pacific which is Monday 08:00 WAT. Incidents logged before 08:00 WAT on Monday would not appear. Use explicit date ranges when timezone precision matters in multi-region instances.

**2. Group by fields must be categorical, not continuous.**
Group by Priority works because there are four discrete levels. Group by Opened (a datetime) would produce one bar per unique timestamp - an unreadable chart. Always choose categorical fields (Priority, State, Category, Assignment group) for Group by, never continuous fields (dates, elapsed times, numeric counters).

**3. The report builder AI question feature is supplementary.**
The "What do you want to see?" natural language input can produce fast starting points but does not guarantee the correct table, filter, or grouping. Manual verification is always required before a report is used in a formal context.

**4. Saved reports at Global scope are visible to all users with report access.**
Standard service desk metrics (volume, SLA) are appropriate to share at Global scope. Sensitive data (headcount, salaries, HR records) must be scoped to a restricted group or application.

**5. The PDF export is a static snapshot.**
Incidents logged after the export will not appear in the PDF. The Run Date and Time field documents when the snapshot was taken. Always export immediately before the meeting to ensure data currency.

**6. Task SLA records are created automatically by the SLA engine.**
Analysts do not create Task SLA records manually - they are generated when incidents are opened or prioritised, based on SLA definitions configured in the instance. When a breach report returns unexpected results, the issue is usually in the SLA definition configuration, not the report filter.

**7. A zero-result report exports as a PDF with only the metadata header.**
Before exporting, always run the report in the browser to confirm it returns data. An empty PDF sent to the team lead at 07:55 before an 08:00 service review is a preventable problem.
