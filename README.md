# N3

N3 is a Jira Service Management lab for running a staged Windows domain support queue.

The lab follows a ten-ticket support session covering request intake, customer records, queue routing, priority changes, SLA handling, customer updates, ticket ownership, troubleshooting records, knowledge base handover, and dashboard review.

Technical support work is tested against [ADBox](https://github.com/erwinmagielda/adbox). Jira Service Management records the service desk layer around those issues.

## Environment Configuration

N3 uses [ADBox](https://github.com/erwinmagielda/adbox) as the Windows domain environment behind the Jira tickets.

[ADBox](https://github.com/erwinmagielda/adbox) provides the domain controller, domain users, workstation, DNS path, shared resources, access control, Group Policy, Remote Desktop configuration, and baseline checks used during the support cases.

| Layer                                           | Role                                                                                      |
| ----------------------------------------------- | ----------------------------------------------------------------------------------------- |
| [ADBox](https://github.com/erwinmagielda/adbox) | Windows domain environment used for accounts, DNS, shares, policies, and endpoint checks. |
| Jira Service Management                         | Portal intake, queues, SLAs, customer records, customer replies, and ticket ownership.    |
| N3 Ticket Records                               | Case documentation for triage, investigation, fix, validation, and closure.               |
| Knowledge Base                                  | Reusable support notes created from repeatable ticket patterns.                           |

## Lab Reports

The lab reports document the N3 build path from service desk design to final review.

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

Each record documents one support case from Jira intake through investigation, fix, validation, customer update, and closure.

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

Knowledge base articles are created from resolved ticket patterns such as account lockouts, shared folder access or password reset follow-up, and Group Policy checks.

| KB Area                  | Related Tickets   |
| ------------------------ | ----------------- |
| Account sign-in issues   | N3-1, N3-4, N3-8  |
| Shared folder access     | N3-2, N3-7        |
| Remote Desktop support   | N3-3, N3-10       |
| DNS and domain resources | N3-5, N3-9        |
| Group Policy checks      | N3-6              |

## Repository Layout

The repository separates reports, ticket records, knowledge base notes, and evidence.

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