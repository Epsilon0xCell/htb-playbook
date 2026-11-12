# Phase 5: Privilege Escalation

Purpose: root or SYSTEM, by verified leads, never by scanner output ordering.

Entry criteria: Phase 4 checklist complete or in progress, with the privesc node list scored.

Steps:

1. Manual first pass, in this order: identity (`id`, `whoami /priv` class checks), sudo rights checked against GTFOBins, SUID binaries checked against GTFOBins, capabilities, cron and timers, writable configs, kernel last. The fast manual quick-set: `sudo -l`, SUID, cron, privileges, history and config credentials.
2. PEASS-ng (LinPEAS or WinPEAS) has been running since foothold. Merge its leads with the manual set, then score the merged list with the prioritisation formula.
3. Verify every PEASS-ng lead manually before acting on it. It is lead generation only; by its own documentation it escalates nothing itself. Never let its output ordering dictate priority; scoring does that.
4. Work the scored list. Every lead ends exploited, or struck through with a written reason. A lead that fails silently gets one changed-variable retry, then it is struck through: the reason is the deliverable that stops the next operator re-running it.

After every privilege change, enumeration re-enters from the new vantage point (back to Phase 4).

Exit criteria: root or SYSTEM obtained, or every lead struck through with a reason and the box parked under the rabbit-hole rule.

Checklist:

- [ ] Manual quick-set run before scanner output was read
- [ ] Merged list scored
- [ ] Each lead verified by hand before use
- [ ] Each lead exploited or struck through with a reason
