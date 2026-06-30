# N3

N3 is my Jira Service Management lab for running Windows domain support tickets against ADBox.

The lab turns ADBox technical faults into service desk work: incoming requests, queue triage, priority changes, troubleshooting notes, user updates, resolution summaries, and knowledge base handover.

It is built around a staged support scenario with ten tickets. Some arrive one at a time, some arrive together, and higher-impact incidents interrupt lower-priority work. The goal is to show how I handle mixed service desk work while still proving the technical checks behind each fix.

## ADBox Backend Lab

N3 uses [ADBox](https://github.com/erwinmagielda/adbox) as the technical environment.

ADBox provides the Windows Server domain, writable Domain Controller, DNS service, Active Directory users, Windows 10 clients, Group Policy, Remote Desktop, file sharing, account recovery, and PowerShell checks used throughout the tickets.

N3 records the service desk side of that work: what the user reported, how the issue was triaged, what evidence was gathered, what changed in the queue, what was checked on the endpoint or server, and how the ticket was closed.

## Lab Setup Reports

Section | Report | Coverage
--- | --- | ---
01 | [Service Desk Overview](lab/01-service-desk-overview.md) | N3 scope, Jira purpose, ADBox connection, support workflow, ticket evidence, and lab boundaries.
02 | [Jira Cloud Setup](lab/02-jira-cloud-setup.md) | Jira Cloud Free project setup, service desk access, portal naming, sidebar layout, and first setup screenshots.
03 | [Request Type Forms](lab/03-request-type-forms.md) | Request forms for sign-in, account lockout, DNS, workstation, RDP, file access, GPO, and recurring issue review.
04 | [Queue Priority Model](lab/04-queue-priority-model.md) | Queue structure, impact, urgency, priority choices, active work views, and reprioritisation during intake.
05 | [SLA Field Setup](lab/05-sla-field-setup.md) | Response targets, resolution targets, ticket fields, impact capture, urgency capture, and SLA awareness.
06 | [Live Queue Simulation](lab/06-live-queue-simulation.md) | Ten-ticket scenario with new work, grouped intake, interruptions, completed tickets, and priority changes.
07 | [Knowledge Base Handover](lab/07-knowledge-base-handover.md) | Repeatable support notes created from resolved tickets and recurring technical patterns.

## Ticket Case Records

Section | Ticket | Scenario
--- | --- | ---
001 | [Domain Signin Failure](tickets/N3-001-domain-signin-failure.md) | A user cannot sign in because the workstation is using the wrong DNS path.
002 | [Shared Folder Denied](tickets/N3-002-shared-folder-denied.md) | A user signs in successfully but cannot access a department share.
003 | [Account Lockout Loop](tickets/N3-003-account-lockout-loop.md) | A user keeps locking out after a password change because stale credentials are still being used.
004 | [RDP Access Failure](tickets/N3-004-rdp-access-failure.md) | Remote Desktop support fails because endpoint access settings are incomplete.
005 | [Domain DNS Outage](tickets/N3-005-domain-dns-outage.md) | Multiple clients lose reliable domain name resolution and the ticket jumps ahead of lower-impact work.
006 | [Group Policy Missing](tickets/N3-006-group-policy-missing.md) | A workstation does not receive the expected policy because scope or placement needs checking.
007 | [Network Domain Failure](tickets/N3-007-network-domain-failure.md) | A workstation has network connectivity but cannot use domain services correctly.
008 | [Secure Channel Broken](tickets/N3-008-secure-channel-broken.md) | A domain-joined workstation reports a trust relationship failure.
009 | [Kerberos Time Drift](tickets/N3-009-kerberos-time-drift.md) | Domain authentication fails because the client clock is out of sync.
010 | [Authentication Pattern Review](tickets/N3-010-authentication-pattern-review.md) | Related authentication tickets are reviewed as a recurring support pattern.

## Knowledge Base Articles

Section | Article | Coverage
--- | --- | ---
01 | [Signin Failure Checks](kb/01-signin-failure-checks.md) | User symptom, affected device, domain DNS path, account state, and first checks.
02 | [Account Lockout Checks](kb/02-account-lockout-checks.md) | Lockout symptoms, stale credentials, mapped drives, repeated attempts, and safe closure notes.
03 | [Domain DNS Checks](kb/03-domain-dns-checks.md) | Client DNS settings, domain lookups, server reachability, and ADBox DNS validation.
04 | [RDP Access Checks](kb/04-rdp-access-checks.md) | Remote Desktop settings, access groups, firewall profile, session testing, and support notes.
05 | [Share Permission Checks](kb/05-share-permission-checks.md) | Share path, group membership, NTFS permissions, access testing, and evidence capture.
06 | [GPO Application Checks](kb/06-gpo-application-checks.md) | OU placement, linked policies, forced update, result checks, and client confirmation.
07 | [Time Sync Checks](kb/07-time-sync-checks.md) | Client time, domain controller time, Windows Time service, Kerberos impact, and resync checks.

## Repository Layout

Folder | Purpose
--- | ---
`lab/` | Jira setup, queue design, SLA setup, workflow reports, and live simulation notes.
`tickets/` | Individual ticket records with symptoms, priority, checks, evidence, resolution, and closure.
`kb/` | Knowledge base articles created from repeatable checks and resolved ticket patterns.
`screenshots/` | Evidence for Jira setup, ticket progress, ADBox checks, and completed work.

## Start Here

Start with [Service Desk Overview](lab/01-service-desk-overview.md), then move through Jira setup, request forms, queues, SLA fields, live ticket handling, and knowledge base handover.

## Licence

This project is provided for learning, documentation, and portfolio demonstration purposes.
