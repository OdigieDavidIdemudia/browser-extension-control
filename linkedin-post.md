# LinkedIn post — ready to paste

**Why this exists:** Medium cross-posts to Twitter/X, *not* LinkedIn. So Medium's built-in
distribution toggle will never reach the platform where security practitioners actually
concentrate. This has to be posted by hand.

---

## Formatting notes before you paste

- **No markdown.** LinkedIn renders plain text — `**bold**` and `#` show up literally.
  Line breaks and spacing are the only formatting you get.
- **First ~3 lines are all most people see.** Everything after "…see more" is opt-in. The
  hook is doing all the work, so don't touch it.
- **Paste as plain text.** If you paste from a code editor it can carry stray formatting.
  Use paste-special → plain text if in doubt.
- **Link goes last**, on its own line. LinkedIn truncates the preview card in the feed.
- Character limit ~3,000. This is ~2,100.

---

## THE POST

---

Someone installed a browser extension on a work machine.

That sentence shouldn't be a security finding. It was ours.

Last year we counted what our users had installed across the estate. We expected a few dozen. We found 412.

Not one of them was malicious. Almost none of them were careless. They were colleagues who needed a PDF reader, a grammar checker, a password manager, a translation tool.

Every single install was, at the time, equivalent to handing a stranger a permanent key to the building.

Because that is what a browser extension is. It runs inside the browser. It can read every page you visit. Watch what you type into a login form. Send any of it anywhere on the internet. It updates itself. For most of that time, it leaves nothing in your endpoint logs.

The first fix everyone proposes is a blocklist.

We tried to argue our way to one. It is the wrong tool.

A blocklist only knows about threats someone has already seen and written down. It won't stop the extension that turns malicious next Tuesday, or the reputable one that gets acquired in six months. You are not building a control — you are building a list, and the list is always behind.

So we inverted it. Nothing installs unless someone reviewed it and approved it, for a stated business reason. Not because it was flagged as bad. Because nobody ever said yes.

The effect we did not expect: the argument stopped. Before, security had to prove something was bad before blocking it, and that is a fight you lose slowly, one extension at a time. Now the default is safe, and people argue for things to be *added*. The exceptions queue emptied almost immediately.

Three things I would tell anyone about to do this:

1. Test the negative case. A policy that looks correct in the Group Policy console proves nothing. Deliberately try to install something that should be blocked.

2. Expect the helpdesk wave. Legitimate tools will get blocked and people will be right to be annoyed. You need a request route and a response-time commitment live *before* the policy ships, not after.

3. Prune the list. Allowlists only grow unless you force them to shrink, and an allowlist nobody understands is worse than no allowlist.

No new vendor. No agent rolled out to 400 machines. The Group Policy setting already existed the whole time. The hard part was never the technology — it was agreeing where the line sits.

I wrote up the full thing — the discovery method, the enrichment step (we open-sourced ours as ExtSafe), and the Group Policy deployment — with my colleague Godwin Enendu:

[INSERT LINK]

What did I miss?

---

## Suggested first comment

Drop this immediately after posting. LinkedIn indexes it, and it earns you a reply which
extends reach:

---

Worth being explicit about what this post is not: the discovery step uses endpoint file
telemetry you already collect, and the enforcement step uses a policy setting Chrome and
Edge have shipped for years. Neither needs procurement.

The genuinely hard part was the middle — deciding which extensions were actually approved,
and building a request process good enough that people used it instead of routing around it.

Full technical reference (sanitised, free to reuse): [INSERT PAGES LINK]

---

## After posting

- Reply to every comment in the first hour — that window drives most of the distribution.
- Repost from your personal profile. Company pages get materially less reach.
- Don't edit the post after 24h; it resets engagement.