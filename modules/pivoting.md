# Module: Multi-Host Pivoting

Mandatory in Pro Labs, Endgame-style ranges, and on any second interface or reachable internal subnet.

1. On every foothold, before privesc: interfaces, routes, ARP, resolver config, hosts file, environment, known hosts, browser and stored credentials. Record reachable subnets as new attack surface in the ledger. Loot order: credentials, routes, configs, flags. A host's value is what it reaches.
2. Choose transport by constraint: SSH credentials mean `ssh -D` dynamic forwarding plus proxychains (simplest); no SSH and web egress only means chisel reverse SOCKS; native tooling without proxychains, plus UDP or ICMP, means ligolo-ng with a TUN interface.
3. ligolo-ng standard build: create the TUN interface, start the proxy, connect the agent, start the tunnel in session, add the route for the target subnet through the TUN device. Through ligolo, scan with `nmap --unprivileged -sT -Pn -n`: the agent converts to full connects, so a SYN scan flag through ligolo is not a real SYN scan on the far side; record results accordingly. The agent's own loopback services are reached by routing 240.0.0.1/32 and targeting 240.0.0.1. Exact commands are in the [command reference](../reference/commands.md).
4. Scan discipline through a pivot: host discovery on the new subnet (top ports, fast), record live hosts in the ledger, then full enumeration per host restarts Phase 1 for that host, with its own record section and its own branch of the hypothesis tree. Never spray or brute-force across a pivot before per-domain password policy checks.
5. Double pivot: a second agent on the deeper host connects to a listener on the first pivot, which forwards to the attacker; a second TUN interface with its own route. One interface and one route per subnet; reusing an interface for two subnets is the classic lost-afternoon bug. Draw the topology map in the record at every hop. At 3 hops, no map means stop and draw it.
6. Stability: tunnels die. Script the rebuild (the commands live in the record), verify the route against a single known-live host before re-scanning, and re-validate credentials per host with NetExec across the tunnel before assuming a path is dead.

Tools: ligolo-ng, chisel, `ssh -D`, proxychains, nmap (through-pivot form), NetExec.
