# Non-Engagement Letter Agent

This use case shows how PatentClaw could use OpenClaw agentic AI to reduce malpractice risk by ensuring that declined prospective-client matters are formally closed with an attorney-approved non-engagement letter.

The goal is simple: when a law firm decides not to accept a matter, the prospective client should receive clear written notice that the firm does not represent them.

## Why This Use Case

Non-engagement letters are a practical workflow control. The legal work is not complex, but the process is easy to miss. A prospective client may contact the firm, share facts, discuss deadlines, and later assume the firm was protecting their interests unless the firm clearly says otherwise.

An agent can help by watching for declined or inactive intake matters, checking whether a non-engagement letter exists, drafting from a firm-approved template, routing the draft for attorney review, and logging the result.

## Agent Goal

Ensure every declined prospective-client matter has a timely, attorney-approved non-engagement letter and an auditable record of delivery.

## Trigger

The agent runs when a prospective-client record is marked with a status such as declined, conflict, out of scope, no response, not accepted, or referred elsewhere.

The agent can also flag stale intake matters that have had no activity for a firm-defined number of days.

## Workflow

1. A prospective client contacts the firm.
2. Intake information is recorded.
3. An attorney decides the firm will not accept the matter.
4. The agent detects the declined status.
5. The agent checks whether a non-engagement letter has already been sent.
6. If no letter exists, the agent drafts one from a firm-approved template.
7. The attorney reviews, edits, and approves the draft.
8. The letter is sent or queued according to firm policy.
9. The agent logs the template used, approval, delivery method, date, and recipient.

## Inputs and Outputs

| Category | Examples |
| --- | --- |
| Inputs | Prospective client name, contact information, matter type, date of inquiry, declination reason, known deadlines, responsible attorney, firm-approved template |
| Outputs | Draft non-engagement letter, attorney approval task, delivery record, matter note, exception alert |

## Guardrails

The agent does not decide whether to accept or reject a matter. That remains an attorney decision.

The agent should not send a non-engagement letter without attorney approval unless the firm has expressly configured that behavior for a narrow, approved scenario.

The agent should not provide legal advice, evaluate the merits of the prospective client's matter, or make statements about deadlines except through firm-approved template language reviewed by an attorney.

If the intake record mentions an urgent deadline, statute of limitations, filing date, public disclosure date, or response date, the agent should escalate the draft for priority attorney review.

## Example Agent Instruction

```text
When a prospective-client matter is marked declined, conflict, out of scope, not accepted, referred, or inactive beyond the firm threshold, check whether a non-engagement letter has been sent.

If no letter is found, draft a non-engagement letter using the approved firm template, populate known intake information, flag any urgent dates or risk indicators, and route the draft to the responsible attorney for review.

Do not send the letter or communicate with the prospective client unless attorney approval is recorded. Log all actions, sources, template versions, approvals, and delivery records.
```

## Example Audit Log

| Field | Example |
| --- | --- |
| Matter | Prospective Client - ACME Widget Disclosure |
| Status | Declined |
| Trigger | Intake status changed to declined |
| Template | Non-Engagement Patent Inquiry v1.2 |
| Draft Created | 2026-06-29 10:14 AM |
| Risk Flags | Possible public disclosure date mentioned |
| Reviewer | Responsible Attorney |
| Approval Status | Pending |
| Delivery Status | Not sent |

## Sample Log Entry

```text
2026-06-29 10:14 AM
Agent: Non-Engagement Letter Agent
Matter: Prospective Client - ACME Widget Disclosure
Event: Intake status changed to declined
Action: Checked matter file for existing non-engagement letter
Result: No prior non-engagement letter found

2026-06-29 10:15 AM
Action: Drafted non-engagement letter from approved template
Template: Non-Engagement Patent Inquiry v1.2
Risk Flag: Intake notes mention possible public disclosure date
Next Step: Routed draft to responsible attorney for priority review
Delivery Status: Not sent
```

## Why It Fits PatentClaw

Patent inquiries often involve invention disclosures, public-use dates, filing deadlines, ownership questions, and foreign-filing considerations. Even when a firm declines the matter, the firm benefits from a clear record that no attorney-client relationship was formed and that the prospective client was told to seek other counsel.

This is a good first PatentClaw use case because it is narrow, process-driven, auditable, and naturally requires human approval.



