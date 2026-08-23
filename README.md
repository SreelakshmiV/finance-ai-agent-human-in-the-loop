# Finance AI Agent — Human-in-the-Loop
> An AI-powered finance decision-support agent designed around policy grounding, controlled refusal, human escalation, and evaluation-driven development.

Prototype & Data Disclaimer

This project is a proof-of-concept developed for learning, experimentation, and demonstration purposes.

- The agent is grounded using publicly available Microsoft documentation together with fictional/sample finance policies created specifically for this prototype.
- Example policies, including the Travel & Expense policy and associated approval thresholds, are simulated and do not represent the policies of any real organisation.
- All finance scenarios, transactions, amounts, users, approval paths, and business examples used in this repository are fictional or test data.
- No live organisational, customer, employee, vendor, financial, or other confidential data is used.
- The workflow demonstrates an architectural pattern for policy-grounded AI decision support and human-in-the-loop controls; it is not connected to a production finance environment.

## 1. The Problem

Finance teams deal with policies, approval rules, exceptions, and operational questions where an AI assistant cannot simply "guess" an answer.
The challenge is to build an agent that can:
- Answer finance questions using defined policy guidance
- Distinguish standard scenarios from exceptions
- Refuse to provide an answer when the available information is insufficient
- Escalate higher-risk or ambiguous cases to a human reviewer
- Return structured outcomes to the calling agent
- Be evaluated systematically rather than judged only through ad-hoc testing
This project explores that problem through a controlled Finance AI Agent MVP.

## 2. The Concept

The agent follows a simple principle:
**Answer when the policy supports the decision.  
Refuse when the policy does not provide sufficient support.  
Escalate when human judgment is required.**
The objective is not to make the AI autonomous at all costs.
The objective is to make the AI **useful, bounded, and auditable**.

## 3. High-Level Architecture

The MVP uses a workflow-based architecture with:

1. Agent entry point
2. Policy / instruction grounding
3. Decision logic
4. Exception detection
5. Human review
6. Structured response to the calling agent

### High-level flow

```text
User / Calling Agent
        │
        ▼
   Finance AI Agent
        │
        ▼
 Policy-grounded reasoning
        │
        ▼
   Decision / Exception?
      ┌─┴──────────┐
      │            │
     No           Yes
      │            │
      ▼            ▼
   Respond      Human Review
                   │
                   ▼
            Structured Outcome
                   │
                   ▼
             Calling Agent


---

## 4. MVP

The MVP was built to demonstrate the complete decision-support pattern rather than just a conversational interface.

- Policy-grounded Finance Agent responses
- Controlled refusal when information is insufficient
- Exception identification
- Human-in-the-loop escalation
- Workflow-based routing and structured outcomes

## 5. Evaluation Approach

The Finance Agent was tested using a structured evaluation set of **63 test scenarios**.
The evaluation was designed to test behaviour across different types of finance requests rather than relying only on successful demonstration cases.
Scenarios included:

- Standard policy-supported questions
- Requests containing policy exceptions
- Requests with insufficient information
- Ambiguous finance scenarios
- Requests that should trigger controlled refusal
- Cases requiring human review
- Attempts to obtain decisions beyond the agent's authority
The purpose of the evaluation was not simply to measure whether the agent generated an answer.
It was designed to test whether the agent made the **appropriate decision about when to answer, refuse, or escalate**.

### An important evaluation finding

Manual review identified false negatives where appropriate controlled-refusal behaviour had been classified as unsuccessful.”
Manual review showed that some of these classifications were false negatives.
For example, a response could be marked incorrect because the agent did not provide the expected answer, even though the agent had correctly refused to make a decision that was unsupported by the available policy or information.
This highlighted an important distinction when evaluating governed AI systems:
> A refusal can be a successful outcome.
For decision-support agents, evaluation therefore needs to consider **behavioural correctness**, not simply answer matching.
This became one of the key learnings from the MVP and will inform the next iteration of the evaluation framework.


## 6. Human-in-the-Loop Design
Not every finance decision should be automated.
The MVP therefore includes a Human Review workflow for scenarios where the agent identifies that a request should not be resolved autonomously.
At a high level:
```text
Finance Request
      |
      v
Finance AI Agent
      |
      v
Policy / Decision Assessment
      |
      +----------------------+
      |                      |
Standard case          Exception / ambiguity
      |                      |
      v                      v
Agent response          Human Review
                             |
                             v
                      Reviewer decision
                             |
                             v
                      Structured outcome
The Human Review pattern is intended for situations such as:

Policy exceptions
Higher-risk decisions
Ambiguous requests
Insufficient authority for autonomous decision-making
Cases where human judgement is required
This creates a deliberate boundary between AI decision support and human accountability.

Workflow prototype
A workflow prototype was created to demonstrate:
Agent → Decision Logic → Human Review → Structured Response
The workflow returns the review outcome to the calling agent so the interaction can continue without treating human escalation as a separate disconnected process.
Workflow screenshots will be added here.

7. What the MVP Demonstrates

This project is intentionally focused on the decision and control architecture rather than building a production finance application.
The MVP demonstrates how an AI agent can be designed to:
Ground responses in defined guidance
Recognise the boundary of its authority
Avoid inventing unsupported finance decisions
Refuse safely when required information is unavailable
Detect exceptions
Escalate selected decisions to a human
Return structured outcomes
Be tested using repeatable evaluation scenarios

The broader design principle is:
Automate the decision where appropriate. Escalate the judgement where necessary.

8. Phase 2
The next phase will focus on moving from an MVP decision pattern toward a more robust agent architecture.
Planned areas of exploration include:
Evaluation refinement
Improve the evaluation framework so that controlled refusals and appropriate escalations are recognised as successful outcomes rather than false failures.
Structured policy retrieval
Explore retrieval patterns that allow the agent to reason against larger and more structured policy libraries while maintaining traceability to the governing guidance.
Confidence and exception routing
Introduce stronger routing logic around ambiguity, exceptions, and decision confidence.

Human review improvements
Expand the Human Review workflow to capture structured reviewer outcomes that can be returned to the agent and used for subsequent processing.
Auditability
Explore logging of:

Request
Policy basis
Agent decision
Escalation reason
Human decision
Final outcome

This would provide a stronger audit trail for governed finance-agent use cases.
Additional finance use cases
Extend the architecture to other controlled finance decision-support scenarios while keeping the underlying pattern reusable.

9. Key Learning
Building the agent reinforced an important lesson:
The difficult part of enterprise AI is not getting an LLM to answer a question. It is designing what the system should do when it shouldn't answer the question.
Policy grounding, exception handling, controlled refusal, evaluation and human escalation are therefore treated as first-class components of the architecture rather than safeguards added after the agent is built.

Project Status
MVP / Experimental
This repository documents the architecture, evaluation approach and design learnings from the prototype.
It is intended as a portfolio and learning project rather than a production implementation.

10. MVP Prototype

The MVP demonstrates an end-to-end Finance AI decision-support pattern combining policy-grounded reasoning, controlled refusal, exception identification, and human-in-the-loop escalation.

### Policy-Grounded Finance Action

The agent uses approved finance policy and business rules to support operational finance decisions.
<img width="547" height="681" alt="1  policy grounded AI- creating VPJ" src="https://github.com/user-attachments/assets/0768b834-e45e-468d-ac62-802f816fb013" />

### Policy Query

The agent interprets finance policy questions and provides responses grounded in the available policy documentation.

<img width="893" height="726" alt="2  Policy query" src="https://github.com/user-attachments/assets/ea719b66-c438-42de-b2ae-2dcf8ffacb33" />

### Controlled Refusal

When sufficient policy evidence or required information is unavailable, the agent avoids making an unsupported decision and responds with a controlled refusal.

<img width="538" height="667" alt="3  controlled refusal" src="https://github.com/user-attachments/assets/25f581a5-c8b3-4a12-af83-cfa78a475511" />

### Human-in-the-Loop Escalation

Where a request exceeds defined policy thresholds, the agent routes the exception into a workflow for human review rather than autonomously approving the request.

<img width="1918" height="750" alt="4  WF activity" src="https://github.com/user-attachments/assets/35c888ad-e653-4a09-8907-e151f29398cc" />

