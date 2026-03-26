# Section 03 — Customer Service & Complaints (Retain)

Business Function: Customer Service / Support  
**Trigger:** A customer complaint or inquiry is received via email, web form, or social media.  
**Prompts in this section:** P06, P07, P08

### Section Purpose
Uses AI to instantly categorize complaints by type and urgency, ensuring high-risk issues (e.g., staff conduct or delivery failures) are routed to the correct department immediately.

Drafts responses that are empathetic but legally safe, avoiding "hollow" apologies or admissions of liability while maintaining a professional tone.

Automatically summarizes complex or high-priority cases for senior management, reducing the time spent reviewing long email threads.

### Customer Service Workflow Chain

Customer complaint received 

P06 · Complaint Triage (Categorizes issue and sets urgency level via JSON) 
│
▼
P07 · Customer Response Draft (Professional reply drafted for human agent review) 
│
▼
P08 · Escalation Summary (Generated for Management only if urgency is "High")

# Prompts


