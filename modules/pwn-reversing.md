# Module: Pwn and Reversing Triage

Trigger: a downloadable binary, a raw TCP custom-protocol service, or source showing a native component.

1. `file`, `checksec` (RELRO, canary, NX, PIE, Fortify), `strings -n 6`; run it once; note input points. checksec decides the tree. Record it in the note.
2. Static triage in Ghidra: main, then the input function, then the sink: unbounded `gets`, `read`, `strcpy`, `scanf`; `printf(user)` format string; malloc and free misuse (use-after-free, double-free); signed and unsigned index maths. Note buffer sizes and any win function.
3. Dynamic confirm locally only: cyclic pattern, crash, `cyclic_find` offset. Never guess offsets against the remote; never spray untested payloads at it. A crash may kill a shared or forked service or poison box state; see the reset rule in the decision layer.
4. Technique by mitigation lattice: NX off and no canary means shellcode; NX on means ret2win, ret2libc, or ROP (ROPgadget, ropper); PIE or ASLR means find a leak first (format string, out-of-bounds read) before any ROP; canary means leak it or go byte by byte on a forking server; full RELRO means no GOT overwrite, so pivot to the return address or version-specific targets; a static binary means ret2syscall or SROP.
5. Identify the remote libc from a leak before finalising (leaked address to a libc database). Build with pwntools, verify locally (same binary, `socat` if network-shaped), then one remote run per verified payload.
6. Hand-off rule: if there is no local crash or win in about 30 minutes of triage, or the bug is heap with a glibc version you have no notes for, park it as a node with the full triage record and continue the box's other surfaces. Heap and kernel pwn are a specialist session, not a mid-box grind.
7. Reversing-only path (no exploitable sink): look for flag and checker logic: string comparisons, XOR or RC4 constants, anti-debug, a custom VM. Solve with the Ghidra decompile plus a Python or z3 reimplementation. Record the algorithm, not just the flag.

Tools: `file`, `checksec`, `strings`, Ghidra, pwntools, ROPgadget, ropper, `socat`, z3.
