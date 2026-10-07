---
id: <SHORT-ID>              # e.g. recon-smb-enum
title: <what this card does>
module: <CPTS module name>  # where it came from in the path
tags: [situation, tool, protocol]   # describe the SITUATION, not just the tool
status: draft               # draft | verified (verified = I've run every command on a box)
---

## When

One line: the situation where I reach for this card. "I have an open SMB port and no creds."

## Commands

```bash
command --flags target        # what this does, in one line
next-command                  # and this
```

Keep flags I actually use. Drop the ones I never touch. Annotate every line.

## Why it works

3–6 lines, no more. The mechanism, only enough to understand the output and know when it
*won't* work. This is the part I read when a command surprised me — not before.

## Gotchas

- The thing that wasted my time once so it never does again.

## See also

- Other cards, and the HTB module / box this came from.
