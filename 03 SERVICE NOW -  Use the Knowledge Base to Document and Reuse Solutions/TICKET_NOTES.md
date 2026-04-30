# Lab 04 - Ticket Notes

> Agent documentation for KB0010008 creation and INC0010012 resolution
> Date: 2026-04-29 / 2026-04-30
> Authored by: System Administrator

---

## Knowledge Article Record

| Field | Value |
|---|---|
| KB Number | KB0010008 |
| Short description | Users unable to log in due to forgotten password |
| Knowledge base | IT |
| Category | IT |
| Author | System Administrator |
| Workflow State | Published |
| Scheduled publish date | 2026-04-29 11:19:40 |
| Valid to | 2100-01-01 |
| Views | 18 (as of 2026-04-30) |
| Average rating | 0/5 (pending user ratings) |
| Template used | Standard (HTML) |
| Linked incidents | INC0010025 |

---

## Knowledge Article Full Content

### Title
**User Unable to Login: Forgotten Password**

### Introduction
Experiencing trouble accessing your account can be frustrating, especially when you're met with an "Incorrect password" error or find yourself locked out after several attempts. This article outlines the common symptoms of login problems and provides a clear, step-by-step guide to regain access to your system.

### Symptoms
If you are facing any of the following issues, the resolution steps below will help you resolve them quickly:

- **Unable to log into the system** - Your usual credentials are not granting access.
- **"Incorrect password" error** - The system rejects the password you entered, even if you believe it is correct.
- **Account lockout after multiple attempts** - After several failed login attempts, your account becomes locked for security reasons.

### Resolution Steps

**Step 1 - Navigate to the Self-Service Portal**
Open your web browser and go to the company self-service portal URL provided by IT. You do not need to be logged in to access the password reset function.

**Step 2 - Click "Forgot Password"**
On the login screen, click the "Forgot Password" or "Reset Password" link below the login fields.

**Step 3 - Verify Your Identity**
Enter your corporate email address. The system will send a verification code to your registered email or mobile number. Enter the code when prompted.

**Step 4 - Set a New Password**
Create a new password that meets the corporate password policy:
- Minimum 12 characters
- At least one uppercase letter
- At least one number
- At least one special character
- Cannot be the same as the last 5 passwords

**Step 5 - Log In with the New Password**
Return to the login screen and use your username and the newly created password to log in. Your account lockout will be automatically cleared once the password reset is completed.

**Step 6 - Contact the Service Desk if the Issue Persists**
If you are unable to complete the password reset, or if your account remains locked after resetting, contact the Service Desk:
- Portal: Self Service > Get Help
- Phone: [Internal IT Support Number]
- Reference this article: KB0010008

---

## Linked Incident Record

| Field | Value |
|---|---|
| Incident Number | INC0010012 |
| Caller | System Administrator |
| Opened | 2026-04-26 02:25:27 |
| Closed | 2026-04-28 02:30:13 |
| Impact | 3 - Low |
| Urgency | 2 - Medium |
| Priority | 4 - Low |
| State | Resolved |
| Short description | User unable to log in |
| Assignment group | (not assigned - resolved at first contact) |

### Comments (Customer visible)
```
https://dev294020.service-now.com/kb_view.do?sysparm_article=KB0010008
```
Direct link to the self-service knowledge article provided so the user can bookmark and reuse the steps independently.

### Work Notes (Internal)
```
Resolved using Knowledge Article KB0010008. Article linked to this record.
```

### Resolution Code
```
Solution provided
```

### Resolution Notes
```
Users able to log in using self-service portal. Steps documented in Knowledge Article KB0010008.
```

### Activity Log Entry
```
System Administrator                           Comments - 2026-04-30 03:51:28
KB0010008 : Users unable to log in due to forgotten password.
```

---

## Resolution Timeline

```
2026-04-26 02:25:27   INC0010012 opened - "User unable to log in"
2026-04-29 11:19:40   KB0010008 authored and scheduled for publish
2026-04-29            KB0010008 published to IT Knowledge Base - workflow state: Published
2026-04-29            Article appears in Knowledge Search results (17 views accumulated)
2026-04-30 03:51:28   KB0010008 attached to INC0010012 via Related Search > Attach
2026-04-30 03:51:28   Work notes added: "Resolved using Knowledge Article KB0010008"
2026-04-30 03:51:28   Resolution code set to "Solution provided"
2026-04-30 03:51:28   Customer-visible comment added with direct KB article URL
2026-04-28 02:30:13   INC0010012 closed
2026-04-30            Article view count: 18 (incremented after self-service search)
2026-04-30            INC0010025 visible in KB0010008 "Most Recent Tasks" sidebar
```

---

## Observations and Learning Points

### 1. KCS in Practice
This lab demonstrates the core KCS (Knowledge-Centred Service) loop. The trigger was a recurring issue (same password reset call received three times). Rather than resolving silently again, the agent captured the solution in a structured knowledge article. The next occurrence either resolves itself through self-service or takes seconds for an agent to handle by searching and attaching the existing article.

### 2. Bidirectional Traceability
After linking the article to the incident, the relationship is visible from both directions:
- From INC0010012: the activity log shows KB0010008 as a hyperlinked entry
- From KB0010008: the Most Recent Tasks sidebar shows INC0010025 (a subsequent incident of the same type resolved using this article)

This bidirectional linkage is what makes knowledge management auditable and provable.

### 3. Article Template Selection
The Standard template was chosen over the Known Error template because this is a How-To resolution, not a confirmed known error linked to a Problem record. Template choice affects the article's metadata fields and the way it is categorised for search indexing.

### 4. View Count as Deflection Evidence
The article went from 2 views (immediately after publishing) to 18 views within 20 hours. Each view that does not result in a new incident is a deflected ticket. In high-volume environments, a single well-written article on a common issue can deflect dozens of tickets per week.

### 5. Comments vs Work Notes
- The KB article URL was placed in **Comments (Customer visible)** so the user receives the self-service link in their notification
- The internal documentation note ("Resolved using KB0010008") was placed in **Work Notes** so it appears in internal reports but not in customer-facing communications
- This distinction is essential for data hygiene and customer experience

---

## Validation Summary

| Check | Result |
|---|---|
| KB0010008 created in IT knowledge base | Confirmed |
| Article state: Published | Confirmed |
| Article content: Symptoms + Resolution Steps | Confirmed |
| INC0010012 opened with matching short description | Confirmed |
| Related Search surfaced KB0010008 | Confirmed |
| Article attached via Attach button | Confirmed |
| Work notes document KB number | Confirmed |
| Resolution code: Solution provided | Confirmed |
| Customer URL shared in Comments | Confirmed |
| Article appears in Self Service KB search | Confirmed |
| View count incremented after search | Confirmed (17 to 18) |
| Incident visible in article's Most Recent Tasks | Confirmed |

---

*Lab 04 - Knowledge Base Management | ServiceNow PDI | 2026-04-29 to 2026-04-30*
