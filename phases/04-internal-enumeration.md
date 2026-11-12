# Phase 4: Internal Enumeration

Purpose: re-run the full local checklist from the new context. Enumeration is a loop, not a step: every foothold and every privilege change re-enters enumeration from the new vantage point.

Entry criteria: foothold node confirmed, and the internal enumeration ledger started.

Steps:

1. Full local checklist from the new context: identity and privileges, users and groups, network state from inside, running services and listening sockets (including ones bound to localhost that external scans never saw), scheduled tasks, installed software, readable configuration, credential material in files and history.
2. Merge the background PEASS-ng output with the manual quick-set into one scored privilege-escalation node list. That merged list is Phase 5's input.
3. Record new surface found from inside (internal services, routes, credentials) in the same coverage-ledger style as Phase 1. A service that only exists internally is new Phase 1 surface for a new vantage point.

Timing bound: the checklist completes, or is well advanced, before the first privilege-escalation attempt; on the reference workflow that means at most about 30 minutes of internal enumeration before privesc work starts. The decision layer governs hypothesis switching inside the phase; it does not extend this start bound.

Exit criteria: checklist complete and the scored privesc node list written.

Checklist:

- [ ] Identity, privileges, users, groups
- [ ] Internal listeners and services
- [ ] Scheduled tasks and timers
- [ ] Configs, histories, credential material
- [ ] PEASS-ng output merged and scored with the manual set
- [ ] New internal surface entered in the ledger
