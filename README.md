# N3

N3 is a Jira Service Management lab for running a staged Windows domain support queue.

The lab covers the service desk workflow around technical support work: request intake, customer records, queue routing, priority changes, SLA handling, customer updates, ticket ownership, troubleshooting records, knowledge base handover, and dashboard review.

The workflow follows a ten-ticket support session where new issues arrive while other work is already active. Higher-impact incidents move ahead of lower-priority requests, waiting-on-user work is separated from active work, and each ticket keeps its own record for checks, evidence, resolution notes, and closure.

## Environment Configuration

N3 uses [ADBox](https://github.com/erwinmagielda/adbox) as the Windows domain environment behind the Jira tickets.

ADBox provides the domain controller, domain users, workstation, DNS path, shared resources, access control, and baseline checks used during the support cases. N3 sits above that environment as the service desk workflow layer.

## Lab Reports

| Report | Area | Description |
| ------ | ---- | ----------- |
| [01 Service Desk Overview](lab/01-service-desk-overview.md) | Operating model | Defines the N3 workflow, ticket lifecycle, priority model, and evidence rules. |
| [02 Jira Cloud Setup](lab/02-jira-cloud-setup.md) | Jira setup | Creates the Jira Service Management space used for the lab. |
| [03 Request Type Forms](lab/03-request-type-forms.md) | Request intake | Configures the request types used to raise support tickets. |
| [04 Queue Priority Model](lab/04-queue-priority-model.md) | Queues | Builds the working queues used for triage, priority handling, and category routing. |
| [05 SLA Field Setup](lab/05-sla-field-setup.md) | SLAs | Configures first response and completion targets. |
| [06 Customer Account Records](lab/06-customer-account-records.md) | Customers | Adds Jira customer records matching enabled ADBox users. |
| [07 Live Queue Simulation](lab/07-live-queue-simulation.md) | Queue run | Runs the staged ten-ticket service desk simulation. |
| [08 Knowledge Base Handover](lab/08-knowledge-base-handover.md) | KB handover | Documents how resolved ticket patterns become reusable support notes. |
| [09 Dashboard Status Review](lab/09-dashboard-status-review.md) | Dashboard review | Reviews the Jira dashboard and final service desk state after selected resolutions. |

## Ticket Records

Individual ticket records are stored in [`tickets/`](tickets/).

Each ticket record is used for the technical side of the case:

| Area | Purpose |
| ---- | ------- |
| Reported issue | Captures the user-facing ticket details. |
| Triage notes | Records priority, queue placement, and ownership. |
| Technical checks | Documents ADBox/Jira checks performed during investigation. |
| Evidence | Links screenshots and command output used to support the fix. |
| Resolution | Records the fix or fulfilment action. |
| Customer update | Captures the final response back to the requester. |
| Related KB | Links repeatable fixes to knowledge base notes. |

Planned ticket records:

| Ticket | Summary |
| ------ | ------- |
| N3-1 | Cannot sign in on AD-WIN10-01 |
| N3-2 | Cannot access shared folder from AD-WIN10-01 |
| N3-3 | Remote Desktop connection fails to AD-WIN10-01 |
| N3-4 | Account keeps locking after sign-in attempts |
| N3-5 | Cannot reach AD-SRV01 domain resources from AD-WIN10-01 |
| N3-6 | Expected desktop policy missing on AD-WIN10-01 |
| N3-7 | Request access to SupportShare |
| N3-8 | Cannot sign in after password reset |
| N3-9 | Domain name lookup fails on AD-WIN10-01 |
| N3-10 | Request Remote Desktop access for support |

## Knowledge Base

Reusable support notes are stored in [`kb/`](kb/).

Knowledge base articles are created from resolved tickets where the fix pattern is likely to appear again, such as shared folder access, account lockouts, domain resource checks, Remote Desktop access, or DNS lookup problems.

## Repository Layout

| Path | Purpose |
| ---- | ------- |
| `lab/` | Main lab reports. |
| `tickets/` | Individual ticket records and technical case notes. |
| `kb/` | Reusable knowledge base handover articles. |
| `screenshots/lab/` | Evidence screenshots for lab reports. |
| `screenshots/tickets/` | Evidence screenshots for individual ticket investigations. |
| `screenshots/kb/` | Evidence screenshots for KB handover where needed. |

## Current Status

The service desk setup and live queue simulation are in progress.

Completed setup areas include:

| Area | Status |
| ---- | ------ |
| Jira service space | Complete |
| Request types | Complete |
| Queues | Complete |
| SLA goals | Complete |
| Customer account records | Complete |
| Live queue simulation | Complete |
| Ticket investigations | In progress |
| Knowledge base handover | Pending |
| Dashboard review | Pending |

## Start Here

Begin with:

[01 Service Desk Overview](lab/01-service-desk-overview.md)

Then follow the lab reports in order.

## Licence

This project is for portfolio and learning use.