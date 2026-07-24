# N3

N3 is a Jira Service Management lab for running a staged Windows domain support queue.

The lab covers the service desk workflow around technical support work: request intake, impact checks, urgency, priority changes, queue movement, troubleshooting notes, user updates, resolution summaries, and knowledge base handover.

The workflow follows a ten-ticket support session where new issues arrive while other work is already active. Higher-impact incidents move ahead of lower-priority requests, and each ticket records the checks used to investigate, resolve, and close the case.

## Environment Configuration

N3 uses [ADBox](https://github.com/erwinmagielda/adbox) as the working Windows domain environment behind the Jira tickets. ADBox establishes the network path, server role, domain, client machines, and baseline checks that make the N3 support cases possible.

## Lab Reports

The lab reports cover the Jira side of N3 before the ticket work starts. They document the service desk setup, request forms, queues, priority model, SLA fields, live queue handling, and knowledge base handover.

| Section | Report                                                       | Coverage                                                                                         |
| ------- | ------------------------------------------------------------ | ------------------------------------------------------------------------------------------------ |
| 01      | [Service Desk Overview](lab/01-service-desk-overview.md)     | Operating model for ticket flow, triage fields, queue behaviour, evidence, and closure.          |
| 02      | [Jira Cloud Setup](lab/02-jira-cloud-setup.md)               | Jira Cloud Free setup, service project creation, portal access, sidebar layout, and setup proof. |
| 03      | [Request Type Forms](lab/03-request-type-forms.md)           | Request forms for sign-in, account lockout, DNS, workstation, RDP, file access, and GPO issues. |
| 04      | [Queue Priority Model](lab/04-queue-priority-model.md)       | Queue structure, impact, urgency, priority order, and reprioritisation during active intake.     |
| 05      | [SLA Field Setup](lab/05-sla-field-setup.md)                 | Response targets, resolution targets, impact fields, urgency fields, and SLA visibility.         |
| 06      | [Live Queue Simulation](lab/06-live-queue-simulation.md)     | Ten-ticket queue run with grouped intake, interruptions, completed work, and priority changes.   |
| 07      | [Knowledge Base Handover](lab/07-knowledge-base-handover.md) | Support notes turned into reusable knowledge base records after ticket resolution.               |

## Ticket Records

The ticket records are the main body of the lab. Each one is written as a service desk case with a reported symptom, queue decision, technical checks, evidence, resolution, and closure note.

| Section | Ticket                                                                       | Scenario                                                                                       |
| ------- | ---------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| 001     | [Domain Sign-In Failure](tickets/N3-001-domain-signin-failure.md)             | A workstation sign-in issue investigated through client DNS and domain controller lookup.       |
| 002     | [Shared Folder Denied](tickets/N3-002-shared-folder-denied.md)                | A file access issue checked through user context, group membership, and share access.           |
| 003     | [Account Lockout Loop](tickets/N3-003-account-lockout-loop.md)                | A repeated lockout investigated through account state, saved credentials, and login attempts.   |
| 004     | [RDP Access Failure](tickets/N3-004-rdp-access-failure.md)                    | A failed remote support path checked through endpoint settings, access rights, and connectivity. |
| 005     | [Domain DNS Outage](tickets/N3-005-domain-dns-outage.md)                      | A higher-impact DNS issue affecting more than one client and changing the queue order.          |
| 006     | [Group Policy Missing](tickets/N3-006-group-policy-missing.md)                | A missing policy result checked through OU placement, scope, refresh, and client results.       |
| 007     | [Network Domain Failure](tickets/N3-007-network-domain-failure.md)            | A workstation with network access but broken domain resource access.                            |
| 008     | [Secure Channel Broken](tickets/N3-008-secure-channel-broken.md)              | A domain trust issue affecting sign-in on a joined workstation.                                 |
| 009     | [Kerberos Time Drift](tickets/N3-009-kerberos-time-drift.md)                  | An authentication issue caused by time drift between the client and domain environment.          |
| 010     | [Authentication Pattern Review](tickets/N3-010-authentication-pattern-review.md) | A review of related authentication tickets, repeated causes, and handover notes.              |

## Knowledge Base Articles

The knowledge base articles collect checks that repeat across the ticket set. These are written as short handover records for common Windows domain support issues.

| Section | Article                                                     | Coverage                                                                                  |
| ------- | ----------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| 01      | [Sign-In Failure Checks](kb/01-signin-failure-checks.md)    | First checks for affected user, affected device, visible error, DNS path, and account state. |
| 02      | [Account Lockout Checks](kb/02-account-lockout-checks.md)   | Lockout symptoms, stale credentials, mapped drives, repeated attempts, and closure notes.  |
| 03      | [Domain DNS Checks](kb/03-domain-dns-checks.md)             | Client DNS settings, domain lookup tests, server reachability, and result confirmation.    |
| 04      | [RDP Access Checks](kb/04-rdp-access-checks.md)             | Remote Desktop settings, access groups, firewall profile, and session validation.          |
| 05      | [Share Permission Checks](kb/05-share-permission-checks.md) | Share path, group membership, NTFS permissions, access testing, and evidence capture.      |
| 06      | [GPO Application Checks](kb/06-gpo-application-checks.md)   | OU placement, linked policy, forced update, result checks, and client confirmation.        |
| 07      | [Time Sync Checks](kb/07-time-sync-checks.md)               | Client time, domain time, Windows Time service, Kerberos impact, and resync checks.        |

## Repository Layout

The repository is split by work type. Lab reports cover Jira setup and workflow, ticket records hold the support cases, knowledge base articles hold reusable checks, and screenshots provide evidence for setup and resolution.

| Folder         | Purpose                                                                       |
| -------------- | ----------------------------------------------------------------------------- |
| `lab/`         | Jira setup, queue design, SLA setup, workflow reports, and live simulation notes. |
| `tickets/`     | Individual ticket records with symptoms, priority, checks, evidence, and closure. |
| `kb/`          | Knowledge base articles created from repeatable checks and resolved ticket patterns. |
| `screenshots/` | Evidence for Jira setup, ticket progress, technical checks, and completed work. |

## Start Here

Start with [01 Service Desk Overview](lab/01-service-desk-overview.md), then move through Jira setup, request forms, queues, SLA fields, live ticket handling, and knowledge base handover.

## Licence

This project is provided for learning, documentation, and portfolio demonstration purposes.
