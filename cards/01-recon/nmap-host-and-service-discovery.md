---
id: recon-nmap-discovery
title: Find live hosts and enumerate services with nmap
module: Network Enumeration with Nmap
tags: [first-contact, no-info-yet, nmap, tcp, udp, scanning]
status: draft
---

## When

First contact with a target or a subnet. I have an IP (or range) and nothing else yet.

## Commands

```bash
# 1. fast full-TCP-port sweep — just find what's open, don't fingerprint yet
nmap -p- --min-rate 5000 -T4 -Pn 10.10.10.10 -oN nmap/all-ports.txt

# 2. deep scan ONLY the open ports from step 1 (say 22,80,445)
nmap -p22,80,445 -sCVt -Pn 10.10.10.10 -oN nmap/services.txt
#   -sC default scripts   -sV version detect   -t for timing already set by -T below if needed

# cleaner, more common form of step 2:
nmap -p22,80,445 -sC -sV -Pn 10.10.10.10 -oN nmap/services.txt

# 3. top UDP ports — slow, run it in the background while I work TCP
sudo nmap -sU --top-ports 100 -Pn 10.10.10.10 -oN nmap/udp.txt

# discover live hosts across a subnet (no port scan, just who's up)
nmap -sn 10.10.10.0/24 -oN nmap/live-hosts.txt
```

## Why it works

Split the work: a `-p-` sweep is fast because it does *nothing* but check which of the 65535
TCP ports answer. Running `-sC -sV` against all 65535 is what makes people wait 40 minutes — so
you only aim the slow scripts/version-detection at the handful that were actually open. `-Pn`
skips host-discovery ping (HTB hosts often drop ICMP, and without `-Pn` nmap calls them "down"
and scans nothing). UDP is a separate scan because UDP has no handshake, so nmap infers state
from absence of a reply — that's why it's slow and noisy; cap it to the top ports.

## Gotchas

- Forgot `-Pn` → "Host seems down. If it is really up... use -Pn." That's the fix, every time.
- `--min-rate` can blow past a fragile lab's rate limit and *lose* open ports. If results look
  thin, re-run step 1 without it before you trust "nothing's open."
- `-oN` to a file from the start. You will want to grep this scan again in two hours.

## See also

- `cards/01-recon/smb-enumeration.md` — once 139/445 shows open.
- HTB module: *Network Enumeration with Nmap*.
