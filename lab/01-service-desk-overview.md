# Service Desk Overview

N3 runs ADBox support work through a Jira Service Management queue.

This page sets the operating model before Jira is configured. It defines how tickets enter the queue, how priority is assigned, how work moves between statuses, and how evidence is handled across the lab.

## Working Model

ADBox provides the Windows domain environment. N3 controls the service desk workflow around that environment.

| Layer    | Role                                                           |
| -------- | -------------------------------------------------------------- |
| ADBox    | Windows domain, clients, DNS, AD users, GPO, RDP, and shares.  |
| N3       | Ticket intake, triage, priority, queue control, notes, and KB. |
| Evidence | Screenshots of Jira state, command output, fixes, and results. |

## Ticket Lifecycle

Each ticket follows the same support path from intake to closure.

| Stage          | Action                                                              |
| -------------- | ------------------------------------------------------------------- |
| Intake         | User symptom, affected device, affected account, and impact logged. |
| Triage         | Request type, category, urgency, impact, and priority assigned.     |
| Placement      | Ticket enters the correct working queue.                            |
| Investigation  | ADBox checks performed on the client, server, account, or policy.   |
| Update         | Ticket notes record findings, attempted fixes, and user impact.     |
| Resolution     | Fix applied and tested against the reported symptom.                |
| Closure        | Resolution summary, evidence link, and next-step note added.        |
| Knowledge Base | Repeatable checks moved into a KB article where useful.             |

## Ticket Fields

The same fields are used across the ticket set so each case can be reviewed in a consistent way.

| Field              | Use                                                                 |
| ------------------ | ------------------------------------------------------------------- |
| Request Type       | Defines the support path, such as sign-in, DNS, RDP, or file access. |
| Affected User      | Identifies the account involved in the issue.                       |
| Affected Device    | Identifies the workstation or server involved in the issue.         |
| Error Message      | Captures the user-facing symptom.                                   |
| Business Impact    | Records whether one user, multiple users, or a service is affected. |
| Urgency            | Records how quickly the issue needs attention.                      |
| Priority           | Combines impact and urgency into the work order.                    |
| Troubleshooting    | Records checks performed and findings.                              |
| Resolution Summary | Records the fix and the confirmed result.                           |

## Priority Model

Priority is based on impact and urgency.

| Priority | Meaning                                    | Example                                          |
| -------- | ------------------------------------------ | ------------------------------------------------ |
| P1       | Multiple users or a core service affected. | Both clients lose domain DNS resolution.         |
| P2       | One user blocked from normal work.         | User cannot sign in to a domain-joined machine.  |
| P3       | Work affected with a workaround available. | User cannot access one shared folder.            |
| P4       | Low-risk request or documentation task.    | KB update or access review note.                 |

## Queue Behaviour

The queue is designed to change during the ticket run.

| Queue State       | Meaning                                                    |
| ----------------- | ---------------------------------------------------------- |
| New               | Ticket has arrived and needs triage.                       |
| Active            | Ticket is being worked.                                    |
| Waiting On User   | User reply or confirmation is needed.                      |
| Waiting On Change | A configuration change or admin action is pending.         |
| Resolved          | Fix has been applied and confirmed.                        |
| Closed            | Resolution summary and evidence have been recorded.        |

## Simulation Pattern

The ticket set runs as one service desk session. New work arrives while other tickets are already active, and higher-impact issues move ahead of lower-priority work.

| Wave | Queue Event                                                 | Ticket Range     |
| ---- | ----------------------------------------------------------- | ---------------- |
| 1    | First issue arrives.                                        | N3-001           |
| 2    | Three more issues arrive together.                          | N3-002 to N3-004 |
| 3    | Two tickets complete, then a higher-impact issue arrives.   | N3-005           |
| 4    | Two more tickets enter the queue.                           | N3-006 to N3-007 |
| 5    | Final technical cases and recurring issue review.           | N3-008 to N3-010 |

## Evidence Rules

Screenshots are used when they prove setup, queue state, technical checks, or completed resolution.

| Evidence Type    | Example                                                   |
| ---------------- | --------------------------------------------------------- |
| Jira Setup       | Project screen, request types, queues, SLA fields.        |
| Queue State      | Multiple active tickets, priority order, status movement. |
| Technical Check  | `ipconfig`, `nslookup`, `gpresult`, Event Viewer, ADUC.   |
| Fix Confirmation | Successful sign-in, resolved lookup, restored access.     |
| Closure          | Jira resolution note, linked screenshot, KB handover.     |

This overview page does not use screenshots because no Jira configuration or ticket work has been performed at this stage.

## Result

The N3 operating model is defined before Jira setup begins.

The next stage creates the Jira Service Management project and captures the first setup evidence.

## Navigation

| Previous                     | Current                  | Next                                      |
| ---------------------------- | ------------------------ | ----------------------------------------- |
| [Project README](../README.md) | 01 Service Desk Overview | [02 Jira Cloud Setup](02-jira-cloud-setup.md) |