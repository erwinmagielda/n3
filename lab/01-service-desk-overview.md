# Service Desk Overview

N3 runs Windows domain support work through a Jira Service Management queue.

This page defines the operating model for the ticket run: how requests enter Jira, how they are triaged, how queue movement works, how technical checks are recorded, and how cases are closed.

## Intake Model

Tickets start as customer-style portal requests. The submitted description records what the requester reports before investigation begins.

| Intake Field                                             | Use                                                              |
| -------------------------------------------------------- | ---------------------------------------------------------------- |
| Affected user                                            | Identifies the person reporting or affected by the issue.        |
| [ADBox](https://github.com/erwinmagielda/adbox) username | Links the ticket to the domain account being checked.            |
| UPN                                                      | Records the email-style domain identity.                         |
| Workstation                                              | Identifies the affected endpoint.                                |
| Target resource                                          | Records the device, share, service, policy, or access target.    |
| Issue                                                    | Captures the user-facing problem.                                |
| Error message                                            | Records the visible error or reported failure.                   |
| Started                                                  | Records when the user noticed the issue.                         |
| Notes                                                    | Adds user context, uncertainty, or extra detail.                 |

## Triage Model

Triage decides the ticket priority, queue placement, owner, and next action.

| Triage Field | Use                                                                |
| ------------ | ------------------------------------------------------------------ |
| Impact       | What user, workstation, account, service, or resource is affected. |
| Urgency      | How quickly the issue needs action.                                |
| Priority     | The working importance assigned from impact and urgency.           |
| Queue        | The Jira view where the ticket should be worked.                   |
| Owner        | The person responsible for the next action.                        |
| Status       | The current state of the ticket.                                   |

## Priority Model

Priority is based on impact and urgency.

| Priority | Meaning                                    | Example                                                   |
| -------- | ------------------------------------------ | --------------------------------------------------------- |
| P1       | Core service path or major impact.         | Core domain name resolution fails from the active client. |
| P2       | One user blocked from normal work.         | User cannot sign in to a domain-joined workstation.       |
| P3       | Work affected with a workaround available. | User cannot access one shared folder.                     |
| P4       | Low-risk request or documentation task.    | KB update or access review note.                          |

Jira priority labels map into the N3 working model.

| Jira Priority | N3 Use                                       |
| ------------- | -------------------------------------------- |
| Highest       | Core service path or major user impact.      |
| High          | User blocked from normal work.               |
| Medium        | Work affected, workaround or local use left. |
| Low           | Low-risk request, fulfilment, or follow-up.  |

## Queue Behaviour

The queue shows what needs triage, what is active, what is waiting, and what has been resolved.

| Queue State | Meaning                                           |
| ----------- | ------------------------------------------------- |
| New         | Ticket has arrived and needs triage.              |
| To Do       | Ticket has been triaged and is waiting for work.  |
| In Progress | Ticket is being actively worked.                  |
| Pending     | User reply or confirmation is needed.             |
| Done        | Fix or fulfilment has been applied and confirmed. |

The main queue views separate active work by status, priority, and request type.

| Queue                 | Use                                                              |
| --------------------- | ---------------------------------------------------------------- |
| New and untriaged     | Fresh unassigned requests waiting for first review.              |
| High priority active  | Highest and High priority unresolved work.                       |
| Waiting on user       | Tickets paused because requester confirmation is needed.         |
| Identity and access   | Sign-in, lockout, access request, and shared folder work.        |
| Network and endpoint  | Network, domain, Remote Desktop, workstation, and policy issues. |
| Resolved this week    | Recently resolved work used for closure review.                  |
| All open              | Fallback view for active work.                                   |
| Assigned to me        | Personal working view for assigned tickets.                      |

## Ticket Lifecycle

Each ticket follows the same path from portal intake to closure.

| Stage          | Action                                                                                                                |
| -------------- | --------------------------------------------------------------------------------------------------------------------- |
| Intake         | User symptom, affected device, affected account, and impact logged.                                                   |
| Triage         | Request type, category, urgency, impact, and priority assigned.                                                       |
| Placement      | Ticket enters the correct working queue.                                                                              |
| Investigation  | [ADBox](https://github.com/erwinmagielda/adbox) checks performed on the client, server, account, policy, or resource. |
| Finding        | Confirmed cause or support finding recorded.                                                                          |
| Resolution     | Primary fix applied through the most suitable support method.                                                         |
| Validation     | PowerShell, client-side checks, or resource access confirm the result.                                                |
| Update         | Internal note and customer-facing reply added to Jira.                                                                |
| Closure        | Ticket moved to Done after the fix and communication are complete.                                                    |
| Knowledge Base | Repeatable checks moved into a KB article where useful.                                                               |

## Ticket Structure

Ticket records document the technical side of each case.

| Section               | Purpose                                                                                       |
| --------------------- | --------------------------------------------------------------------------------------------- |
| Ticket Summary        | Captures the Jira key, requester, account, device, and status.                                |
| Reported Issue        | Records the customer-submitted problem.                                                       |
| Triage                | Explains priority, queue placement, and handling decision.                                    |
| Investigation         | Shows the technical checks performed against [ADBox](https://github.com/erwinmagielda/adbox). |
| Finding               | Summarises the confirmed cause or support finding.                                            |
| Resolution Applied    | Records the primary fix used.                                                                 |
| PowerShell Validation | Confirms the technical state from the command line.                                           |
| Client Validation     | Proves the user-facing issue is resolved.                                                     |
| Alternative Methods   | Documents other valid admin methods for the same task.                                        |
| Jira Notes            | Shows internal handover and customer-facing communication.                                    |
| Closure               | Confirms final Jira status and SLA completion where visible.                                  |
| Result                | Summarises the case outcome.                                                                  |

The primary fix is usually performed through the GUI when that matches first-line support behaviour. PowerShell validation is used where it adds clear technical proof. PowerShell fix commands are documented under Alternative Methods when useful for repeatable administration.

## Simulation Pattern

The ticket set runs as one service desk session, with new work arriving while other tickets are already active.

| Wave | Queue Event                                             | Ticket Range  |
| ---- | ------------------------------------------------------- | ------------- |
| 1    | First issue arrives and is triaged into active work.    | N3-1          |
| 2    | Three more issues arrive while N3-1 is already active.  | N3-2 to N3-4  |
| 3    | Higher-impact domain resource issue enters the queue.   | N3-5          |
| 4    | Two more medium-priority tickets enter the queue.       | N3-6 to N3-7  |
| 5    | Final access and technical cases enter the queue.       | N3-8 to N3-10 |

## Ticket Set

The ticket set covers identity, access, endpoint, Remote Desktop, policy, and domain-resource support.

| Ticket | Summary                                                 | Request Type                       | Support Area          |
| ------ | ------------------------------------------------------- | ---------------------------------- | --------------------- |
| N3-1   | Cannot sign in on AD-WIN10-01                           | Cannot sign in                     | Identity              |
| N3-2   | Cannot access shared folder from AD-WIN10-01            | Shared folder access issue         | Access                |
| N3-3   | Remote Desktop connection fails to AD-WIN10-01          | Remote Desktop issue               | Endpoint and remote   |
| N3-4   | Account keeps locking after sign-in attempts            | Account locked                     | Identity              |
| N3-5   | Cannot reach AD-SRV01 domain resources from AD-WIN10-01 | Network or domain resource issue   | Network and domain    |
| N3-6   | Expected desktop policy missing on AD-WIN10-01          | Workstation or policy issue        | Endpoint and policy   |
| N3-7   | Request access to Sales shared folder                   | Access request                     | Access                |
| N3-8   | Cannot sign in after password reset                     | Cannot sign in                     | Identity              |
| N3-9   | Domain name lookup fails on AD-WIN10-01                 | Network or domain resource issue   | Network and domain    |
| N3-10  | Request Remote Desktop access for support               | Access request                     | Endpoint and remote   |

## Evidence Model

Evidence is used when it proves Jira state, technical state, fix state, validation, or closure.

| Evidence Type      | Example                                                     |
| ------------------ | ----------------------------------------------------------- |
| Jira Setup         | Service space, request types, queues, SLA fields.           |
| Queue State        | Multiple active tickets, priority order, status movement.   |
| Ticket Details     | Customer-submitted request details.                         |
| Technical Check    | ADUC, PowerShell, Event Viewer, `ipconfig`, `nslookup`.     |
| Fix Confirmation   | Enabled account, restored share access, enabled RDP.        |
| PowerShell Check   | Command output confirming account, group, policy, or state. |
| Client Validation  | Successful sign-in, resolved lookup, restored access.       |
| Jira Communication | Internal note and customer-facing reply.                    |
| Closure            | Done state, SLA completion, resolved queue state.           |

Lab reports use wider workflow evidence. Ticket records use focused support-case evidence.

## Navigation

| Previous                       | Current                  | Next                                          |
| ------------------------------ | ------------------------ | --------------------------------------------- |
| [Project README](../README.md) | 01 Service Desk Overview | [02 Jira Cloud Setup](02-jira-cloud-setup.md) |