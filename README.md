# LEARNiT

My CPTS theory-and-commands reference. Not a textbook — a **card corpus**, the way KRIS is.
Machines and CTFs I learn on Hack The Box. This repo is the thing I grep *while* I'm on a box,
and the thing I read *after* I get stuck.

Target: HTB **CPTS** (Certified Penetration Testing Specialist). See the study plan in Notion
("CPTS then CRTO — Chris's Plan") for dates and the weekly rhythm. This repo holds the knowledge.

## How I use this

```
rg "<terms>" cards/        # find the card. free, offline, instant. do this constantly
```

Open the card, grab the command, paste it on the box. Read the theory **only if the command
confused you**. That's the whole method.

## The rules this repo is built on (my way)

1. **Command-first.** Every card leads with copy-paste commands, each with a one-line comment.
   The commands are the card. You should never scroll to find the thing you came for.
2. **Theory is minimal and comes second.** The "Why it works" block is 3–6 lines. It exists for
   the moment a command surprised you — not to be read front-to-back. Lab first, read second.
3. **One screen per card.** If a topic won't fit on a screen, it's two cards. Big modules
   (Active Directory, Enterprise Networks) are *many* small cards, not one long one.
4. **Searchable like KRIS.** Consistent frontmatter + tags so `rg` always finds it. Describe the
   *situation* in tags ("got smb creds", "no shell yet"), not just the tool name.
5. **Zero friction to start.** The demon is sitting down, not the content. The minimum viable
   session is: grep one thing, read one card. That counts. Momentum beats volume.

## Layout

```
cards/
  00-foundations/   networking, Linux, the setup you never want to lose time to again
  01-recon/         host discovery, footprinting, service enumeration
  02-web/           attacking common apps, injection, web exploitation
  03-privesc/       Linux and Windows local privilege escalation
  04-ad/            Active Directory enumeration and attacks (the big one)
  05-pivoting/      pivoting, tunnelling, port forwarding
  06-reporting/     documentation and the exam report (half the exam — take it seriously)
templates/CARD.md   copy this to start a new card
```

Each folder maps to a block in the study plan, so "what am I working on this week" and
"where does this card go" have the same answer.

## Scope discipline

Same bar as KRIS: a card earns its place by being something I'll actually reach for on a box.
No card that just restates a man page. No tool I haven't run. If a card is theory with no command,
it belongs in `00-foundations/` and it had better be short.

## Legal line

Everything here is for **authorised** testing only — HTB labs, HTB exam, and engagements I have
written permission for. Techniques, not targets.
