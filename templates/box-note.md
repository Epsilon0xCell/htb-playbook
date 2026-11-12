# Box Note Template

Copy this skeleton at Phase 0, before any packet is sent. The record is the truth for the whole box; raw tool output goes to files and is referenced by path, never pasted in bulk.

```text
Box: <name>            IP: <ip>            Difficulty: <tier>
Started: <date time>   Rank context: <where this box sits in your plan>

## Phase 0: Setup
- [ ] Box directory created
- [ ] This note created from the template

## Phase 1: External enumeration
Surface count: <hosts, ports, services>
Scans: <paths to stage 1 and stage 2 outputs>
Per-port subsections: <one per open port>
Attack tree sketch: <hypothesis nodes opened>
Lead scores: <E, C, R, H, K, Priority per lead>

## Phase 2: Per-service enumeration
Per service, in order: fingerprint certainty / anonymous and default /
version / misconfiguration / authenticated abuse / specialised tool or waiver
<service>: <status per step, output paths, exhausted line>

## Phase 3: Foothold
Lead worked: <node id>   Primitive: <what was demonstrated>
Shell stabilised: <how>   Validator: <who or what confirmed it, not the finder>
Network position: <interfaces, routes, resolver, hosts, stored credentials>
Loot: <credentials, then routes, then configs, then flags>

## Credentials ledger
<every credential, with where it came from>

## Phase 4: Internal enumeration
<checklist result from the new context, PEASS-ng output merged>

## Phase 5: Privilege escalation
<scored node list, each lead exploited or struck through with a reason>

## Phase 6: AD path (where applicable)
<chain walked, or every edge struck through with a reason>

## Dead ends
<each dead end in place, with the evidence that killed it and time spent>

## Flags
User: <flag or redaction marker>   Root: <flag or redaction marker>
```
