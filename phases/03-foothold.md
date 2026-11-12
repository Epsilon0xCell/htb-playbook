# Phase 3: Foothold

Purpose: a stabilised shell, or a confirmed foothold primitive on the way to one.

Entry criteria: the Phase 2 exhausted line for the service being exploited, or a logged override with a written reason (a screaming-obvious known vulnerability is the legitimate case).

Steps:

1. Work leads in prioritisation order. Any lead at evidence strength 3 (a working primitive) pre-empts scoring and is exploited now.
2. Start PEASS-ng in the background at foothold, so its output is ready for Phase 5, while manual work continues in the foreground.
3. On foothold, before privilege escalation: check network position (interfaces, routes, ARP, resolver, hosts file, environment, known hosts, stored credentials). Record reachable subnets as new attack surface in the ledger. Loot order on any host: credentials, then routes, then configs, then flags. This feeds the [pivoting module](../modules/pivoting.md).
4. Re-score all leads at the foothold. The decision layer runs again here, not only at Phase 1.
5. Stabilise the shell: a real TTY where the platform allows, a known working directory, and the foothold recorded so it can be re-established from the note alone.

Stuck rule: the [two-signal rabbit-hole rule](../decision-layer.md) replaces the flat clock. When it fires, search writeups and video indexes by service plus technique, as a nudge, in learning mode.

Exit criteria: stabilised shell, with the foothold node marked confirmed by a validator other than the finder, or by a deterministic re-run from clean state.

Checklist:

- [ ] Lead worked in score order (or E=3 pre-emption, stated)
- [ ] PEASS-ng running in background
- [ ] Network position recorded
- [ ] Loot order followed
- [ ] Leads re-scored
- [ ] Foothold confirmed independently
