# N3

N3 is a Jira Service Management lab for running a staged Windows domain support queue.

The lab covers the service desk workflow around technical support work: request intake, customer records, queue routing, priority changes, SLA handling, customer updates, ticket ownership, troubleshooting records, knowledge base handover, and dashboard review.

The workflow follows a ten-ticket support session where new issues arrive while other work is already active. Higher-impact incidents move ahead of lower-priority requests, waiting-on-user work is separated from active work, and each ticket keeps its own record for checks, evidence, resolution notes, customer updates, and closure.

## Environment Configuration

N3 uses [ADBox](https://github.com/erwinmagielda/adbox) as the Windows domain environment behind the Jira tickets.

[ADBox](https://github.com/erwinmagielda/adbox) provides the domain controller, domain users, workstation, DNS path, shared resources, access control, Group Policy, Remote Desktop configuration, and baseline checks used during the support cases. N3 sits above that environment as the Jira service desk workflow layer.

The table below separates the technical environment from the service desk layer so the repository structure is clear before the lab reports begin.

| Layer                                           | Role                                                                                      |
| ----------------------------------------------- | ----------------------------------------------------------------------------------------- |
| [ADBox](https://github.com/erwinmagielda/adbox) | Windows domain environment used for accounts, DNS, shares, policies, and endpoint checks. |
| Jira Service Management                         | Portal intake, queues, SLAs, customer records, customer replies, and ticket ownership.    |
| N3 ticket records                               | Case documentation for triage, investigation, fix, validation, and closure.               |
| Knowledge base                                  | Reusable support notes created from repeatable ticket patterns.                           |

## Lab Reports

The lab reports document how the N3 service desk was built before and during the ticket run. They cover the Jira space, request forms, queues, SLA fields, customer records, live queue simulation, knowledge base handover, and final dashboard review.

The table below lists the report sequence, the area each report covers, and the purpose of each file.

| Report                                                            | Area             | Description                                                                                             |
| ----------------------------------------------------------------- | ---------------- | ------------------------------------------------------------------------------------------------------- |
| [01 Service Desk Overview](lab/01-service-desk-overview.md)       | Operating Model  | Defines the N3 workflow, ticket lifecycle, priority model, queue behaviour, and support-case structure. |
| [02 Jira Cloud Setup](lab/02-jira-cloud-setup.md)                 | Jira Setup       | Creates the Jira Service Management space used for the lab.                                             |
| [03 Request Type Forms](lab/03-request-type-forms.md)             | Request Intake   | Configures the request types used to raise support tickets through the portal.                          |
| [04 Queue Priority Model](lab/04-queue-priority-model.md)         | Queues           | Builds the working queues used for triage, priority handling, and category routing.                     |
| [05 SLA Field Setup](lab/05-sla-field-setup.md)                   | SLAs             | Configures first response and completion targets for the service desk workflow.                         |
| [06 Customer Account Records](lab/06-customer-account-records.md) | Customers        | Adds Jira customer records matching enabled [ADBox](https://github.com/erwinmagielda/adbox) users.      |
| [07 Live Queue Simulation](lab/07-live-queue-simulation.md)       | Queue Run        | Runs the staged ten-ticket service desk simulation.                                                     |
| [08 Knowledge Base Handover](lab/08-knowledge-base-handover.md)   | KB Handover      | Documents how resolved ticket patterns become reusable support notes.                                   |
| [09 Dashboard Status Review](lab/09-dashboard-status-review.md)   | Dashboard Review | Reviews the Jira dashboard and final service desk state after selected resolutions.                     |

## Ticket Records

Individual ticket records are stored in [`tickets/`](tickets/).

Each ticket record is used for the technical side of the case. The Jira portal description records the user-facing report, while the ticket record documents triage, investigation, evidence, fix, validation, customer communication, and closure.

The table below explains what each ticket record section is used for.

| Area             | Purpose                                                                                                   |
| ---------------- | --------------------------------------------------------------------------------------------------------- |
| Reported Issue   | Captures the user-facing ticket details submitted through Jira.                                           |
| Triage Notes     | Records priority, queue placement, ownership, and handling decision.                                      |
| Technical Checks | Documents [ADBox](https://github.com/erwinmagielda/adbox) and Jira checks performed during investigation. |
| Evidence         | Links screenshots and command output used to support the fix.                                             |
| Resolution       | Records the fix or fulfilment action applied to the issue.                                                |
| Validation       | Confirms the result with PowerShell, client-side checks, or resource access.                              |
| Customer Update  | Captures the final response back to the requester.                                                        |
| Related KB       | Links repeatable fixes to knowledge base notes where useful.                                              |

The table below lists the ten-ticket support session. Linked entries point to completed ticket records in the repository.

| Ticket | Summary                                                                                     |
| ------ | ------------------------------------------------------------------------------------------- |
| N3-1   | [Cannot sign in on AD-WIN10-01](tickets/N3-1-cannot-sign-in.md)                             |
| N3-2   | [Cannot access shared folder from AD-WIN10-01](tickets/N3-2-shared-folder.md)               |
| N3-3   | [Remote Desktop connection fails to AD-WIN10-01](tickets/N3-3-remote-desktop.md)            |
| N3-4   | [Account keeps locking after sign-in attempts](tickets/N3-4-account-lockout.md)             |
| N3-5   | [Cannot reach AD-SRV01 domain resources from AD-WIN10-01](tickets/N3-5-domain-resources.md) |
| N3-6   | Expected desktop policy missing on AD-WIN10-01                                              |
| N3-7   | Request access to Sales shared folder                                                       |
| N3-8   | Cannot sign in after password reset                                                         |
| N3-9   | Domain name lookup fails on AD-WIN10-01                                                     |
| N3-10  | Request Remote Desktop access for support                                                   |

## Knowledge Base

Reusable support notes are stored in [`kb/`](kb/).

Knowledge base articles are created from resolved tickets where the fix pattern is likely to appear again, such as shared folder access, account lockouts, domain resource checks, Remote Desktop access, DNS lookup problems, password reset follow-up, and Group Policy checks.

The table below groups the knowledge base handover areas by the ticket patterns they come from.

| KB Area                  | Related Tickets   | Purpose                                                                                                                  |
| ------------------------ | ----------------- | ------------------------------------------------------------------------------------------------------------------------ |
| Account sign-in issues   | N3-1, N3-4, N3-8  | Disabled accounts, lockouts, and password reset follow-up.                                                               |
| Shared folder access     | N3-2, N3-7        | Group membership checks and shared folder access validation.                                                             |
| Remote Desktop support   | N3-3, N3-10       | Workstation Remote Desktop availability and user access checks.                                                          |
| DNS and domain resources | N3-5, N3-9        | Client DNS checks, internal name resolution, and [ADBox](https://github.com/erwinmagielda/adbox) domain resource access. |
| Group Policy checks      | N3-6              | Expected policy application, refresh checks, and workstation validation.                                                 |

## Repository Layout

The repository separates lab build reports, ticket case records, knowledge base notes, and screenshot evidence.

The table below shows where each type of N3 material is stored.

| Path                   | Purpose                                                    |
| ---------------------- | ---------------------------------------------------------- |
| `lab/`                 | Main lab reports.                                          |
| `tickets/`             | Individual ticket records and technical case notes.        |
| `kb/`                  | Reusable knowledge base handover articles.                 |
| `screenshots/lab/`     | Evidence screenshots for lab reports.                      |
| `screenshots/tickets/` | Evidence screenshots for individual ticket investigations. |
| `screenshots/kb/`      | Evidence screenshots for KB handover where needed.         |

## Start Here

Start with [01 Service Desk Overview](lab/01-service-desk-overview.md), then follow the reports in order from Jira Cloud Setup through Dashboard Status Review, using the footer navigation panel at the bottom of each report.

## Licence

This repository documents the N3 lab project.