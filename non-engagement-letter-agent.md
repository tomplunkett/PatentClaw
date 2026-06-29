# Non-Engagement Letter Agent

This use case shows how PatentClaw could use OpenClaw agentic AI to reduce malpractice risk by ensuring that declined prospective-client matters are formally closed with an attorney-approved non-engagement letter.

The goal is narrow and practical: when a law firm decides not to accept a matter, the prospective client should receive clear written notice that the firm does not represent them.

## Why This Use Case

Non-engagement letters are a good first agentic workflow because the legal task is bounded, the risk is real, and the required controls are easy to understand.

A prospective client may contact the firm, share facts, mention deadlines, and assume the firm is protecting their interests unless the firm clearly says otherwise. The agent helps prevent that gap by checking whether a non-engagement letter exists, drafting from an approved template, routing the draft for attorney approval, and logging the result.

## Agent Goal

Ensure every declined prospective-client matter has one of three auditable outcomes:

1. A non-engagement letter was already sent.
2. A draft has been created and routed for attorney approval.
3. The matter is blocked because required information or attorney review is missing.

## Trigger

The agent runs when an intake matter is marked declined, conflict, out of scope, not accepted, referred elsewhere, or inactive beyond a firm-defined threshold.

## Workflow

1. Intake matter changes status.
2. Agent checks the matter file for an existing non-engagement letter.
3. If no letter exists, agent loads the approved template.
4. Agent drafts the letter using only intake-record facts.
5. Agent flags urgent dates, public disclosures, possible reliance, or missing information.
6. Attorney reviews, edits, and approves.
7. Letter is sent or queued according to firm policy.
8. Agent logs the template, approval, delivery method, date, recipient, and risk flags.

## Sandbox Controls

| Control Area | Requirement |
| --- | --- |
| Matter access | Read only the relevant prospective-client intake record and related intake documents |
| Templates | Read only from approved non-engagement templates |
| File writes | Write only to the matter draft folder, approval queue, and append-only audit log |
| Email access | No external sending unless attorney approval is recorded |
| Internet access | Disabled by default |
| Deletion | Agent cannot delete matter records, templates, drafts, approvals, or logs |
| Legal judgment | Agent cannot accept, reject, or evaluate representation |
| Escalation | Urgent dates, public disclosures, possible reliance, or missing contact data require attorney review |

Example policy:

```yaml
agent: non_engagement_letter_agent

read_allowed:
  - /matters/prospective_clients/{matter_id}/intake.json
  - /matters/prospective_clients/{matter_id}/documents/
  - /templates/non_engagement/
  - /policies/non_engagement_policy.md

write_allowed:
  - /matters/prospective_clients/{matter_id}/drafts/
  - /matters/prospective_clients/{matter_id}/audit_log.jsonl
  - /approval_queue/non_engagement/

network_allowed:
  - internal_approval_system
  - internal_email_outbox_after_approval

network_denied:
  - public_internet
  - external_email_direct_send

forbidden_actions:
  - accept_or_decline_representation
  - provide_legal_advice
  - send_client_communication_without_approval
  - edit_firm_templates
  - delete_matter_records
```

## Approval Model

The agent should be state-based and require attorney approval before any client communication.

| State | Meaning |
| --- | --- |
| `draft_created` | Agent generated a draft from an approved template |
| `risk_flagged` | Agent found an urgent date or other risk indicator |
| `attorney_review_required` | Draft is waiting for attorney review |
| `approved_to_send` | Attorney approved the exact communication |
| `sent` | Letter was delivered through an approved channel |
| `closed` | Matter record includes delivery confirmation |
| `blocked` | Missing information or unresolved risk prevents sending |

Attorney approval should capture the approving attorney, timestamp, template version, final document hash, delivery method, recipient, and risk flags reviewed.

## Prompt Design

### System Prompt

```text
You are the Non-Engagement Letter Agent for a law firm workflow system.

You do not decide whether the firm accepts or declines representation.
You do not provide legal advice.
You do not send client communications.
You draft only from approved firm templates.
You must flag urgent dates, possible reliance, public disclosure dates, filing deadlines, and other risk indicators for attorney review.
Every action must be logged.
```

### Workflow Prompt

```text
Determine whether this declined prospective-client matter has a documented non-engagement letter.

Use only the intake record, matter documents, approved templates, and firm policy.
If no non-engagement letter exists, draft one from the approved template.
Do not invent facts.
Mark missing information clearly.
Flag urgent dates or risk indicators.
Return a structured result for attorney review.
```

## Minimum Tool Set

| Tool | Purpose |
| --- | --- |
| `get_intake_record` | Load matter metadata and status |
| `search_matter_file` | Check whether a non-engagement letter already exists |
| `read_template` | Load approved firm template |
| `create_draft` | Generate draft letter in a controlled folder |
| `create_approval_task` | Route draft to responsible attorney |
| `append_audit_log` | Record action, sources, and result |
| `queue_delivery` | Queue sending only after approval |

## Structured Output

```json
{
  "matter_id": "PC-2026-0142",
  "status": "declined",
  "non_engagement_letter_found": false,
  "draft_created": true,
  "template_used": "Non-Engagement Patent Inquiry v1.2",
  "risk_flags": ["possible public disclosure date mentioned"],
  "missing_information": ["mailing address"],
  "approval_required": true,
  "recommended_priority": "high",
  "next_action": "route_to_responsible_attorney"
}
```

## Example Audit Log

```json
{
  "timestamp": "2026-06-29T10:14:00-05:00",
  "agent": "non_engagement_letter_agent",
  "matter_id": "PC-2026-0142",
  "trigger": "status_changed_to_declined",
  "sources_checked": [
    "intake.json",
    "matter_documents/",
    "prior_correspondence/"
  ],
  "template_used": "Non-Engagement Patent Inquiry v1.2",
  "action": "draft_created",
  "risk_flags": [
    "possible public disclosure date mentioned"
  ],
  "approval_status": "pending",
  "delivery_status": "not_sent"
}
```

## Test Scenarios

| Scenario | Expected Behavior |
| --- | --- |
| Declined matter, no letter | Draft letter and route for approval |
| Declined matter, letter already sent | Log that no action is needed |
| Matter mentions public disclosure date | Draft letter and flag priority review |
| Missing contact information | Mark draft incomplete or block delivery |
| No attorney approval | Do not send external communication |

## Why It Fits PatentClaw

Patent inquiries often involve invention disclosures, public-use dates, filing deadlines, ownership questions, and foreign-filing considerations. Even when a firm declines the matter, the firm benefits from a clear record that no attorney-client relationship was formed and that the prospective client was told to seek other counsel.

This is a strong first PatentClaw use case because it is narrow, process-driven, auditable, and naturally requires human approval.
