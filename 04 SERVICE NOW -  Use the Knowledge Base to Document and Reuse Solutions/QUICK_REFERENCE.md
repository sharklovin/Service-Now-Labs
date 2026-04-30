# Quick Reference - ServiceNow Knowledge Management

## Knowledge Record Prefixes

| Prefix | Record Type | Where to Find |
|---|---|---|
| KB | Knowledge Article | Knowledge > Articles |
| KBT | Knowledge Base | Knowledge > Knowledge Bases |

---

## Article Workflow States

```
Draft
  |
  v
Review / Awaiting Approval   <-- skipped in some PDI configs
  |
  v
Published                    <-- searchable by all users
  |
  v
Retired                      <-- no longer searchable; kept for reference
  |
  v
Archived / Deleted
```

---

## Article Templates

| Template | Use Case |
|---|---|
| Standard | How-To guides, FAQs, general IT instructions |
| Known Error article | Linked to a Problem record for confirmed known errors |

---

## Key Navigation Paths

| Task | Navigation |
|---|---|
| Knowledge Center (admin view) | Knowledge > Knowledge Center |
| View all articles | Knowledge > Articles |
| Create new article | Knowledge > Articles > Create New (or Knowledge Center > Create an article) |
| Search as end user | Self Service > Knowledge Base |
| Manage knowledge bases | Knowledge > Knowledge Bases |
| View article feedback | Knowledge > Article Feedback |

---

## How to Link a KB Article to an Incident

**Method 1 - Related Search (recommended):**
1. Open the incident
2. Scroll to Related Search Results below Short description
3. Type keywords in the search box
4. Click Attach on the article result

**Method 2 - Knowledge field on incident form:**
1. Open the incident
2. Locate the Knowledge field (may require form layout customisation)
3. Use the lookup icon to search and select the article

**Method 3 - Copy URL to Comments:**
1. Open the published article and copy the URL
2. Paste into the Comments (Customer visible) field of the incident
3. Add the KB number to Work Notes manually

---

## Completing Resolution Fields Correctly

| Field | What to Put |
|---|---|
| Work Notes | "Resolved using Knowledge Article KB[number]. Article linked to this record." |
| Comments (Customer visible) | Direct URL to the KB article |
| Resolution code | "Solution provided" (for KB-based resolutions) |
| Resolution notes | Plain English summary referencing the KB number |

---

## Common Mistakes to Avoid

| Mistake | Why It Matters |
|---|---|
| Publishing to wrong knowledge base | Article may not be visible to the intended audience |
| Leaving article in Draft | Draft articles do not appear in portal search - users cannot find them |
| Not incrementing valid-to date | Article expires and disappears from search unexpectedly |
| Skipping Work Notes | No internal record of what resolved the issue |
| Copying article URL without testing it | Broken links in Comments frustrate users |
| Creating duplicate articles | Wastes maintenance effort and confuses search results |
| Using "Known Error" template for a How-To | Wrong metadata fields are presented; poor search categorisation |

---

## KCS Practice: Capture - Structure - Reuse - Improve

```
CAPTURE     Always document the solution as you solve the problem.
            Never close an incident on a recurring issue without a KB article.

STRUCTURE   Use templates. Every article needs: Summary, Symptoms, Resolution Steps.
            Consistent structure = better search indexing.

REUSE       Search before you solve. If a KB article exists, use it.
            Attach it to the incident. Do not reinvent solutions.

IMPROVE     Update stale articles. Rate articles after using them.
            Flag articles that need revision. Archive articles that are no longer valid.
```

---

## Article Quality Checklist

Before publishing any KB article:

- [ ] Title is clear and searchable (includes the user-facing symptom, not technical jargon)
- [ ] Short description matches the title
- [ ] Knowledge base is correct (IT, not Knowledge or KCS demo data)
- [ ] Category is set
- [ ] Valid to date is set (do not leave blank)
- [ ] Article body contains: Introduction, Symptoms, Resolution Steps
- [ ] Resolution steps are numbered and in plain English
- [ ] Screenshots or diagrams included where helpful
- [ ] Workflow State is Published

---

*ServiceNow ITSM - Lab 04 Quick Reference | Knowledge Management*
