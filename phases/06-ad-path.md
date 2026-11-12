# Phase 6: The AD Path (Where Applicable)

Purpose: the canonical Active Directory chain, run only where a domain is in scope.

Entry criteria: a domain in scope on the target.

Steps, in order:

1. Unauthenticated enumeration: user list, password policy.
2. Password policy arithmetic before any spray. Check the default policy and Fine-Grained Password Policies, which override it for groups. Spray budget is threshold minus 1 attempts per account per observation window; in practice one password per round, waiting out the window between rounds. Username validation with Kerbrute first: Kerberos pre-authentication enumeration does not increment the bad-password count. On lab platforms the lockout threshold is often None; verify, never assume.
3. AS-REP roasting, password spray (NetExec with `--no-bruteforce`, pairs in order, `--continue-on-success`), and poisoning.
4. First credential validated in NetExec and marked Owned in BloodHound. Use NetExec (nxc); its predecessor CrackMapExec is archived, and old writeups translate mechanically.
5. ADCS sweep early and in parallel: `certipy find -vulnerable` as soon as any domain credential exists, plus a skim of the non-vulnerable output for ACL leads (the ESC4 and ESC5 shapes). The ESC catalogue runs ESC1 to ESC16 in current Certipy. Re-run after every new credential, because templates visible and enrollable differ by principal.
6. Kerberoasting and share spidering.
7. DACL abuse, delegation abuse, shadow credentials.
8. Coercion and relay, only after the relay gate, checked in this order: LDAP signing and channel binding (LDAPS); SMB signing per host; ADCS HTTP EPA and HTTPS; ICPR encryption enforcement (ESC11), because HTTP EPA does not close the ADCS RPC relay path; WebClient and coercion surface. Note: ESC9 and ESC10 are effectively dead on domain controllers with the September 2025 strong certificate binding full enforcement; deprioritise on patched estates, keep on labs.
9. Lateral validation.
10. DCSync as the endgame. DCSync rights may arrive via ACL or delegation nodes; chain-value scoring ensures those nodes outrank generic privesc detours.

Exit criteria: shortest path walked, or every edge struck through with a reason.

Checklist:

- [ ] Policy arithmetic written before any spray
- [ ] Spray stayed inside budget
- [ ] First credential validated and marked Owned
- [ ] ADCS swept early, re-swept per credential
- [ ] Relay gate checked in order before coercion
- [ ] Path walked or edges struck through

Tools: NetExec (nxc), BloodHound with its collectors, Certipy, Kerbrute.
