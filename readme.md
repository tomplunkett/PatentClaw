A project using OpenClaw Agentic AI to assist Patent law firm processes.

PatentClaw links:

PatentClaw Introduction: https://youtu.be/R8FDKz2F284

Pitch Deck:  https://github.com/tomplunkett/PatentClaw/blob/main/PatentClawPitchDeck.pdf

Unboxing an HP ZGX Nano AI Station to work on this effort: https://youtu.be/fk7clYWRtQg

Project Abstract: 
This project explores the implementation of OpenClaw, an open-source agentic framework, to assist patent professional workflows. OpenClaw operates as a local or private cloud-based "digital employee" with direct access to file systems, email servers, and specialized patent databases.  We demonstrate how OpenClaw agents can be deployed to assist complex, repetitive tasks that typically consume the billable hours of attorneys and the administrative capacity of legal staff. 

# PatentClaw

PatentClaw explores how agentic AI can help law firms automate workflow processes and reduce malpractice risk.  Patent law is deadline-driven, document-heavy, and highly process-sensitive. Many patent law processes can benefit from agentic-ai assistance.

## Thesis

Law firms need workflows for docketing, conflicts, engagement letters, scope control, billing documentation, complaint handling, client screening, file review, backup coverage, trust-account procedures, information security, and wire-instruction verification.  PatentClaw focuses on operational controls that agentic AI can realistically support. 

## What Agentic AI Adds

PatentClaw is not just a chatbot. It is a controlled agentic workflow system that can monitor matters, retrieve documents, check firm procedures, draft internal work product, flag missing steps, request attorney review, and preserve an audit trail.  The attorney remains responsible for legal judgment, client advice, filings, and final approval.

## Technical Architecture

PatentClaw is designed for local or private-cloud deployment so sensitive client data, invention disclosures, and legal work product remain under firm control.

The reference architecture includes:

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

Example agents might handle intake, conflicts, docket monitoring, patent prosecution, prior art research, billing and scope review, complaint response, information-security checks, and matter closing.


## Design Principles

AI supports process; it does not replace attorney judgment. Important workflow steps should create records. Risk should be flagged early. Critical actions require human approval. Local control matters for confidentiality. The system should be lightweight enough for small firms to actually use.

## Project Vision

PatentClaw asks a practical question:

Can agentic AI help law firms adopt the workflow discipline that insurers, clients, and professional-responsibility systems already expect?


## Disclaimer

This project is for research, education, and workflow-design exploration only. It is not legal advice, insurance advice, or a substitute for professional judgment. Any real-world implementation should be reviewed by qualified attorneys, malpractice-risk professionals, insurance professionals, and technology/security experts.
