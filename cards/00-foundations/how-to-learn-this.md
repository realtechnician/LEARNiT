---
id: found-how-to-learn
title: How to actually learn this — anatomy of a command, and what to memorise
module: Foundations (read first, re-read when you feel behind)
tags: [mindset, memorisation, cheatsheet, decision-map, start-here]
status: verified
---

## When

Read this first. Re-read it the moment you catch yourself thinking *"I should know this
command by heart and I don't"* — because that thought is the trap, and this card is the answer.

## The one thing to get right

**You do not memorise commands. You memorise decisions.**

A strong operator holds three things in their head, and looks up everything else:

1. **The method** — "what do I do now." *445 open → enumerate SMB → try null session → get
   creds → spray them across the subnet.* That chain is in your head. The commands that run
   each step are the easy part once you know the step.
2. **~20 reflex commands** — the handful you type every single box (`nmap` default, `nxc smb`,
   `ls`/`cd` in a shell). You never *studied* these. Reps burned them in for free.
3. **Where everything else lives** — the exact flags, the weird syntax, the one-liners. These
   stay in LEARNiT forever. Even the people who wrote the tools look these up.

Basics by heart, the rest you know where to find. That's the whole game. LEARNiT *is* the
"where to find."

## Anatomy of a command — the skill that actually transfers

Almost every offensive command is the same skeleton:

```
[tool]   [action/mode]   [target]        [auth]            [output]
nxc      smb             10.10.10.10     -u bob -p 'pw'    --shares
nmap     -sC -sV         10.10.10.10                       -oN out.txt
smbclient                //10.10.10.10/Share   -U 'bob%pw'
```

Train this one move: look at any command from a writeup and name each chunk —
*that's auth, that's the target, that's what it does.* Once you can do that, you can bend
**any** command you find to your box without having memorised it. This skill carries across
every tool you'll ever meet. Memorising individual commands does not.

## So where do you start?

**Not with commands. With the decision map.** For a given open port or foothold: what are my
options, and in what order? That map is what CPTS actually tests, and it's what every card's
`When:` line and `tags` encode. The syntax underneath is just the cheatsheet.

| Lives in your head | Lives in LEARNiT (look it up, no shame) |
|---|---|
| The decision — *when* to reach for SMB enum | `enum4linux-ng -A` and its flags |
| The chain — recon → creds → spray → AD | the exact output quirks and one-liners |

## How to study, given the above

- **Do boxes. Look everything up. Let repetition decide what sticks.** Don't sit and memorise —
  the top-20 fall into muscle memory on their own within a month or two of real reps.
- **Keep the other 400 in the cheatsheet on purpose.** Trying to hold them in your head is
  wasted effort the pros don't spend either.
- **When you get stuck, add a card.** The act of writing the card *is* the learning. A gap you
  hit on a box becomes a card, and the card closes the gap next time.
- **One grep, one card read = a real session.** The demon is starting, not the content.

## Gotchas

- Feeling like you "should" have something memorised is not a signal you're behind. It's the
  wrong target. The right target is: did you know *what to do*, and could you find the *how*?
- A flashcard pile of raw commands will rot and demoralise you. A decision map plus a searchable
  cheatsheet will not. Build the second thing — this repo — not the first.

## See also

- `README.md` — the rules this whole repo is built on.
- Every other card: the `When:` line is the decision; the `Commands:` block is the cheatsheet.
