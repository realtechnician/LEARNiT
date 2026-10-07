---
id: recon-smb-enum
title: Enumerate SMB — shares, users, and null sessions
module: Footprinting
tags: [smb, port-445, port-139, null-session, shares, no-creds, got-creds]
status: draft
---

## When

Ports 139/445 are open. I want shares, users, and anything a null (unauthenticated) session leaks
before I even have credentials.

## Commands

```bash
# no creds yet — try an anonymous/null session
smbclient -N -L //10.10.10.10               # -N no password, -L list shares
enum4linux-ng -A 10.10.10.10                # the one-shot: shares, users, groups, policy
nxc smb 10.10.10.10 --shares                # nxc = netexec (the old crackmapexec), null by default
nxc smb 10.10.10.10 --users                 # pull the user list if RID cycling is allowed

# connect to a specific share anonymously
smbclient -N //10.10.10.10/ShareName
#   inside: ls, cd, get <file>, mget *, recurse ON, prompt OFF   (then mget *)

# once I HAVE creds — swap -N for -u/-p and re-run everything
nxc smb 10.10.10.10 -u bob -p 'Passw0rd!' --shares
smbclient //10.10.10.10/ShareName -U 'bob%Passw0rd!'

# check if those creds are a local admin anywhere (spraying one cred across hosts)
nxc smb 10.10.10.0/24 -u bob -p 'Passw0rd!'   # "(Pwn3d!)" in output = admin on that host
```

## Why it works

SMB has a legacy "null session": connect with an empty username and password. Old or
misconfigured hosts let a null session list shares, users, and password policy — recon gold with
no creds. `enum4linux-ng` just automates every null-session query at once. `netexec` (`nxc`) is
the Swiss-army version: the *same* syntax works null, with creds, with a hash, and across a whole
subnet — which is why it's the tool you lean on from recon all the way into AD. "Pwn3d!" means the
account is local admin on that box, i.e. you can get a shell.

## Gotchas

- `smbclient -L` with no `-N` and no creds will hang on a password prompt — pass `-N` or you wait.
- Null sessions are mostly dead on modern Windows. A blank result here is normal, not failure —
  move on to grabbing creds, then come back and re-run with `-u/-p`.
- `nxc`/`netexec` is the rename of `crackmapexec` — old writeups say `crackmapexec`/`cme`, same tool.

## See also

- `cards/01-recon/nmap-host-and-service-discovery.md` — how 445 showed up.
- `cards/04-ad/` — spraying one cred across the domain is the bridge into Active Directory.
- HTB module: *Footprinting* (SMB section).
