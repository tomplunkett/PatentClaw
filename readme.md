# PatentClaw

PatentClaw uses OpenClaw agentic AI to assist patent law-firm workflows.

Patent law is deadline-driven, document-heavy, and highly process-sensitive. That makes it a useful test case for agentic AI systems that monitor workflow, retrieve matter context, flag missing steps, preserve audit trails, and route critical decisions back to attorneys.

## Links

PatentClaw Introduction: https://youtu.be/R8FDKz2F284

Pitch Deck: https://github.com/tomplunkett/PatentClaw/blob/main/PatentClawPitchDeck.pdf

HP ZGX Nano AI Station Unboxing: https://youtu.be/fk7clYWRtQg

## Project Abstract

PatentClaw explores the use of OpenClaw, an open-source agentic framework, to assist patent-practice workflows. OpenClaw can operate as a local or private-cloud "digital employee" with controlled access to file systems, email servers, patent resources, databases, templates, and firm workflow records.

The project focuses on operational controls that agentic AI can realistically support: docketing, conflicts, engagement letters, scope control, billing documentation, complaint handling, client screening, file review, backup coverage, trust-account procedures, information security, wire-instruction verification, and potential-claim logging.

PatentClaw is not a replacement for attorney judgment. It is a controlled workflow system that can monitor matters, retrieve documents, check procedures, draft internal work product, flag missing steps, request attorney review, and preserve an audit trail. Attorneys remain responsible for legal judgment, client advice, filings, and final approval.

## Technical Architecture

PatentClaw is designed for local or private-cloud deployment so sensitive client data, invention disclosures, and legal work product remain under firm control.

| Layer | Role |
| --- | --- |
| Compute | Local AI workstation or private-cloud GPU environment, such as an HP ZGX Nano AI Station using NVIDIA Grace Blackwell GB10 architecture |
| Model | Local large language model served through Ollama, with smaller models for embeddings, classification, routing, and retrieval |
| Orchestration | OpenClaw coordinates specialized agents with defined roles, permissions, tools, and review requirements |
| Retrieval | Local RAG over matter files, invention disclosures, prior art, docket records, templates, historical responses, SQL data, and vector databases |
| Tools | Controlled access to files, email, web portals, USPTO resources, messaging systems, databases, templates, docket exports, and audit logs |
| Governance | Sandboxing, policy guardrails, human approval, evidence pointers, action logs, escalation rules, and an independent E-stop |

## Agent Workflow

Agents follow a controlled cycle: detect a new event, retrieve relevant material, compare it against firm procedure, propose or draft the next step, route critical actions for attorney approval, and log what happened.

In a patent-practice setting, agents could support intake, conflicts, docket monitoring, prosecution workflows, prior art research, billing and scope review, complaint response, information-security checks, and matter closing.

## Design Principles

AI supports process; it does not replace attorney judgment. Important workflow steps should create records. Risk should be flagged early. Critical actions require human approval. Local control matters for confidentiality. The system should be practical enough for real legal teams to use.

## Project Vision

PatentClaw asks a practical question:

Can agentic AI help law firms adopt the workflow discipline that insurers, clients, and professional-responsibility systems already expect?

The patent-law example is the starting point. The larger goal is a reusable framework for safer, more reliable legal-practice workflows.

## Disclaimer

This project is for research, education, and workflow-design exploration only. It is not legal advice, insurance advice, or a substitute for professional judgment. Any real-world implementation should be reviewed by qualified attorneys, malpractice-risk professionals, insurance professionals, and technology/security experts.



