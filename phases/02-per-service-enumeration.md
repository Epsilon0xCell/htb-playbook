# Phase 2: Per-Service Enumeration

Purpose: exhaust each service in a fixed order so no handoff, yours or an agent's, can produce enumeration amnesia.

Entry criteria: Phase 1 coverage complete for the service in question, checked in the per-service ledger.

The pattern, always in this order:

0. Fingerprint certainty first. A banner or version is a claim, not a proof. A scanner checks possible existence; only exploitation confirms.
1. Anonymous and default access check.
2. Version recorded, matched against known vulnerability classes only after step 0.
3. Misconfiguration check.
4. Authenticated abuse, where credentials exist.

Plus, per service: a specialised tool run, or the tool waived with a written reason.

For web services, the artefact and source hunt (web module, step 2) inserts between the anonymous step and the version step.

Exit criteria: an explicit "exhausted" line per service, with the ledger ticked for every step: not run, run clean, or run hit, with the output path.

Checklist, per service:

- [ ] Fingerprint confirmed, not assumed
- [ ] Anonymous and default access tried
- [ ] Version recorded
- [ ] Misconfiguration checked
- [ ] Authenticated abuse tried (or no credentials, stated)
- [ ] Specialised tool run, or waiver written
- [ ] Exhausted line written

Tools: per-service specialised tooling; depth references such as HackTricks are paraphrased and linked, and every technique is verified against the live service before it is believed.
