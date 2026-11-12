# The Decision Layer

The phase spine tells you the order. This layer tells you what to work on next, when to stop working on it, and how deep to go. It replaces the flat "30 minutes then move on" clock, which fails in both directions: it abandons live leads and it funds dead ones.

Budgets and weights here are operator-fit parameters, labelled honestly: no source publishes a validated HTB scoring formula or validated time budgets. Fit them from your own calibration log after about 20 boxes.

## Prioritisation scoring

Score every lead at the end of Phase 1 and at every foothold.

    Priority = (E x C x R) / (H x (1 + K))

- E, evidence strength, 0 to 3: 0 banner only; 1 version matches a known-vulnerability class; 2 misconfiguration or anomaly directly observed (anonymous access, error, leak); 3 working primitive (read, write, or auth bypass partially demonstrated).
- C, chain value, 0 to 3: 0 dead-end information; 1 foothold likely; 2 foothold plus credentials or lateral movement likely; 3 direct privesc or domain path (an ADCS template, DCSync rights, unconstrained delegation).
- R, reuse, 0.5 to 2: does success here unlock other services or hosts (credentials, source, network position). Loot and position value counts.
- H, horizon, 1 to 3: 1 means 3 steps or fewer guessed; 2 means 4 to 6; 3 means unknown, long, or custom development.
- K, novelty cost, 0 to 2: 0 known technique in notes; 1 technique known, not in notes; 2 requires learning, reversing, or a custom exploit.

Rules:

- Work the highest Priority first.
- Any E=3 primitive pre-empts scoring.
- Chain-value-3 AD enumeration runs in parallel regardless of score.
- Ties break toward the lead whose failure is most informative (cheapest decisive test first).
- Log predicted versus actual per node, so the weights can be fitted later.

## Rabbit-hole detection: the two-signal rule

A line is a rabbit hole when ANY TWO of these fire:

- R1: fewer than 1 new record fact per 10 minutes of active work. A record fact is a new file, user, version detail, error class, or response difference.
- R2: three same-family attempts with no change in the response (status, length, timing, or error), counted across everyone working the box, not per person.
- R3: more than 3 incompatible explanations for the node, or no falsifying observation can be stated in one sentence.
- R4: the horizon estimate has doubled since the node was opened.
- R5: the line consumed a fresh-context handoff without a status change.
- R6 (Hard and Insane only): the path is suspiciously well signposted. On Insane, signposting is evidence against the path, because rabbit holes there are designed.

Then: PARK the line with a written revival condition (the single observation that would revive it) and take the next node.

- Two or more parked lines trigger a breadth pass: re-run the coverage ledger and look only for unenumerated surface for one trigger period before deepening anything.
- Everything parked and the breadth pass clean: hint, source re-read, reset, or sleep on it, in tier order. On Easy and Medium: categorical hint, then re-read source or config line by line, then reset, then park the box to tomorrow. On Hard and Insane: the source re-read precedes the hint. Hint levels are categorical (which service or class), then technique, then full.
- Tier backstops per hypothesis: Easy 20 minutes, Medium 25, Hard 40, Insane 60. Plus 20 minutes per attempt-family at every tier.

Persist despite signals when: a primitive is improving (error changing, timing oracle responding, partial read growing); a background crack or spray is still running (switch the foreground, not the job); or each step is producing the next credential mid-chain.

## Reset rule

Reset when: a destructive exploit may have poisoned state and behaviour has diverged from the record; a needed service is down; or unlogged commands ran. At Hard and above, log pre-exploit state before custom or kernel work, and reset liberally on unexplained state change. Persist when the only state change is files you created and can list and delete.

## Difficulty scaling

| Parameter | Easy | Medium | Hard | Insane | Pro Lab |
|---|---|---|---|---|---|
| Assumed chain length | 2 to 3 steps | About 3 | 3 to 5 | 5 or more, or 3 very hard | 10 or more hosts, chained |
| Enumeration depth | Standard; web test menu on signal only | Plus source and artefact hunt, second wordlist tier | Plus full source review if obtainable, pwn and crypto triage if a binary or source is present | Plus: assume designed rabbit holes; keep at least 2 live hypotheses | Full internal enumeration per host; loot to graph mandatory |
| Switch trigger | 20 min per hypothesis | 25 min | 40 min, 20 per attempt family | 60 min, 20 per attempt family; breadth re-check every 90 min | 60 min per host hypothesis; parallelise instead of switching |
| Soft budget before hint or reset decision | About 2 hours | About 4 hours | About 8 hours | Two sessions; sleep on it is legitimate | Days; daily consolidation |
| Hint discipline | After trigger | After 2 triggers on the same phase | One categorical hint, never the exploit | Categorical only; full writeup only after abandoning | Not applicable |
| Who leads | Operator or agent | Agent leads enumeration, operator leads exploit choice | Operator leads, agents parallelise hypotheses | Operator leads; no deepening without a breadth pass | One worker per subnet or host, plus a coordinator |

What changes at high difficulty: expect chained footholds (the foothold gives credentials or context, not a shell), source and config reading as exploitation, custom service logic review, and a second host or privilege boundary hiding inside what looks like privesc.

## Standing rules

- Two-stage nmap, every scan saved structured.
- Re-enumerate after every privilege change.
- NetExec everywhere; never its archived predecessor.
- The per-service pattern is always: fingerprint certainty, anonymous and default, version, misconfiguration, authenticated abuse.
- Reporting is continuous; Phase 7 is review only.
- A finding is confirmed by someone or something other than its finder: a second pair of eyes, or a deterministic re-run from clean state.
- No duplicate attempt without a written delta from the last attempt: what differs, and why it changes the outcome.
- Type, never paste, from writeups. Predict the author's next step before reading it. Writeups are nudges on active boxes and full reads on retired ones.
