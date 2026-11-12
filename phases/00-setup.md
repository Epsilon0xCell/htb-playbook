# Phase 0: Setup

Purpose: a place for the truth to live before any packet is sent. Every later gate is checked from this record, not from memory.

Entry criteria: a named target (box name and IP).

Steps:

1. Create the box directory.
2. Create the note skeleton from [`templates/box-note.md`](../templates/box-note.md). It carries, in order: setup, external enumeration with scans saved under `scans/`, per-service enumeration, foothold, a credentials ledger (every credential, with where it came from), internal enumeration, privilege escalation, the AD path where applicable, dead ends recorded in place with kill reasons, and flags.
3. Confirm the tunnel and the target route before scanning anything. A scan against a dead tunnel produces confident, wrong negatives.

Exit criteria: box directory and note skeleton exist.

Checklist:

- [ ] Directory created
- [ ] Note skeleton created
- [ ] Tunnel up, target reachable
- [ ] Nothing scanned yet

Tools: the box-note template. No scanning tools run in Phase 0.
