# Phase 1: External Enumeration

Purpose: map 100 percent of the reachable surface and count it, so coverage can be measured rather than felt.

Entry criteria: Phase 0 exit met.

Steps:

1. Two-stage nmap, always. Stage 1: full TCP port scan at high rate, saved in structured form. Stage 2: version and script scan (`-sCV`) on the open set only. Working forms are in the [command reference](../reference/commands.md).
2. UDP: top-100 always, in parallel with TCP Stage 2. Escalate to top-1000 when TCP yields no lead at evidence strength 2 or above, when difficulty is Hard or above, or when any UDP hit appears. Full UDP sweeps are never a default; run targeted follow-ups on hits (IKE on 500, SNMP on 161, TFTP on 69). Boxes exist whose only foothold was a UDP service while TCP showed only SSH.
3. Optional: RustScan as a front end on multi-host scans. On a single box its saving over a fast nmap is seconds; do not add tooling complexity for single boxes.
4. Optional: AutoRecon as a background baseline only, with a pruned config: port scan, service detection, suggested manual commands. Disable its automatic web content scans; the playbook runs those tiered, in the web module.
5. Close the phase with the decision step: sketch the attack tree, open a hypothesis node per lead, and score every lead with the [prioritisation formula](../decision-layer.md). This scoring is what the flat "work the list top to bottom" approach lacks.

Exit criteria: every open port has a note subsection, the surface is counted, the per-service ledger is opened, and every lead is scored.

Checklist:

- [ ] TCP stage 1 saved, stage 2 saved
- [ ] UDP top-100 run (escalation decision written)
- [ ] Surface counted: hosts, ports, services
- [ ] Attack tree sketched, leads scored

Tools: nmap; RustScan (optional); AutoRecon (background, pruned only).
