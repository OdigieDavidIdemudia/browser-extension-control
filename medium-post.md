mak# MEDIUM POST — READY TO PASTE

Paste the body below into Medium's editor (Medium converts Markdown on paste).
Set the metadata from the tables after the rule.

---

## Title

**Your Users Have Given a Stranger the Keys to Your Bank Account**

*(61 characters — under the 100 limit)*

## Subtitle / deck

**It wasn't a breach. It was 400 browser extensions nobody had ever reviewed.**

*(72 characters — under the 140 limit)*

## Tags

`security` `#infosec` `#group-policy` `#chrome` `#devops`

## Canonical link

Leave **blank**. A canonical link tells Medium the original lives elsewhere and suppresses
your traffic from this URL. If you want Medium indexed, leave it empty. Set it only if you
later publish the same content on your own domain and want Medium to defer to it.

## Subtitle for the card

No subtitle is also fine — Medium generates a card preview from your first image.

---

## Recommended cover image

Use the generated hero so the Medium card renders correctly (Medium will otherwise pick a
random frame or show a blank card):

`https://odigiedavididemudia.github.io/browser-extension-control/assets/cover-neobrutal.png`

Paste it as the first element. Medium uses the first image as the card preview.

### Image placement

| # | Image | Where | Why |
|---|-------|-------|-----|
| 1 | `cover-neobrutal.png` | **First element of the body** | Doubles as the Medium card preview. Vault door, tiles bouncing off the indigo barrier, three approved tiles through the gate. Left third is deliberately empty — that's where Medium overlays the title on the card. |
| 2 | `quantity-vs-allowlist.png` | After "Three layers, none of them a product" | Carries the 412 → few-dozen argument visually. The chaos/three-tiles split does the arguing for you. |
| 3 | `pipeline-neobrutal.png` | Not in the Medium post | Used on the GitHub Pages reference instead — it's the section map for a documentation page, redundant in a narrative piece. |

Paste images as standalone blocks on their own line, with a blank line before and after.
Medium sets its own width; don't resize manually.

**Design note:** all three are neobrutalist — 4px black outlines, flat fills, hard offset
shadows, indigo `#4F46E5` as the single accent on off-white. That matches the design system
the reference page uses. None contain any text, because generated typography comes out
garbled and Medium lets you set real type over the top anyway.

Direct URLs if you prefer hotlinking:
- Cover — `https://odigiedavididemudia.github.io/browser-extension-control/assets/cover-neobrutal.png`
- Quantity — `https://odigiedavididemudia.github.io/browser-extension-control/assets/quantity-vs-allowlist.png`

---

# BODY — paste everything below

---

*Written jointly by **David Idemudia Odige** and **Godwin Enendu**, from work we did together
in our security monitoring and threat intelligence team.*

---

It started with a spreadsheet.

Not an incident, not an alert, not a phishing wave. One of us pulled a list together because
she was curious: how many browser extensions are installed across our estate? She expected a
few dozen. There were four hundred and twelve distinct ones.

Every single one had been installed by a colleague who was trying to do their job.

## The thing nobody had asked

Here is the part that kept us up afterwards. Nobody did anything wrong. Not one of those
four hundred installs was malicious, and almost none of them were careless. They were people
who needed a PDF reader, a grammar checker, a password manager, a translation tool, and a
dozen AI helpers that had exploded onto the scene in the last two years. Every one of those
requests was reasonable.

And every one of those installs was, at the time, equivalent to handing a stranger a key to
the building — permanently, silently, and with no way to revoke it later.

Because that is what a browser extension is. It runs inside the browser. It can read and
rewrite every page you visit. It can watch what you type into a login form. It can send
anything it sees to anywhere on the internet. It updates itself, without asking. And for most
of that time it does all of it without an icon in the tray, a process in the task manager, or
a single line in most endpoint logs.

We had all of this sitting in a regulated environment. For years. With no control on it at
all.

## Why we nearly got this wrong

The first proposal either of us heard was a blocklist. Block the known-bad extensions.
Maintain it quarterly. Respond to the next bad extension when it shows up.

That is a bad idea, and it took us a while to explain why to the people who wanted it.

A blocklist only knows about threats someone has already seen, catalogued, and written down.
Everything else walks straight through. It does not block the extension that turns malicious
next Tuesday. It does not block the perfectly reputable one that gets bought by someone else
in six months. It does not block the fake AI assistant that nobody has reported yet, because
nobody has reported it yet.

You are not building a control. You are building a list, and the list is always behind.

## The decision that mattered

We went the other way. Instead of naming what is forbidden, we named what is permitted.

Nothing installs unless it has been reviewed and approved by someone, for a stated business
reason. Everything else is blocked by default — not because someone flagged it as malicious,
but because nobody ever approved it.

This is the entire change. Everything else is implementation detail.

The psychological effect surprised us. Once we switched to allowlist, the burden of proof
inverted. Previously, security had to prove an extension was bad before blocking it, and
that is a fight you lose slowly, one extension at a time. Afterwards, the default was safe
and security had to argue for something to be *added*. The queue of exceptions dried up almost
immediately.

## Three layers, none of them a product

There was no procurement here. No new vendor, no new licence, no browser management agent
deployed to four hundred machines. It came together in three layers.

**We found what was already there.** It turns out browser extensions sit on disk in a known
location in every user's profile. We already had endpoint telemetry watching file activity.
So we didn't deploy anything to find them — we just asked a question of data we already had.

**We made the list mean something.** Four hundred and twelve bare identifiers are useless.
An identifier like `nkbihfbeogaeaoehlefnkodbefgpgknn` tells you absolutely nothing about
whether to trust it. We resolved every single one against public extension intelligence to
attach a name, a description, a publisher, and a risk signal, then had humans sort them into
approve, reject, or *pending*.

That middle stage was the one we expected to skip, because it looks like something you can
do by hand when someone finds time. You cannot. A few hundred identifiers is already well
past what manual research sustains, and the moment you let it slide you end up approving
whatever nobody got round to looking at. So between us we built the boring half into a small
tool — [ExtSafe](https://github.com/OdigieDavidIdemudia/ExtSafe), open source, MIT — that
takes the identifier list, resolves each entry, and hands back a spreadsheet with name,
description, risk rating, source link and resolution status for each one.

What it deliberately does not do is decide. It produces evidence. The approve/reject call is
still a person talking to the person who asked for the tool, and that conversation is the
entire point.

That third bucket mattered more than we expected. It gave us somewhere to put things that
weren't ready for a decision yet. Without it, every ambiguous request had to be silently
approved or silently denied, and both of those quietly destroyed trust in the process.

**We enforced it with policy that already existed.** Chrome and Edge both ship native Group
Policy controls. One setting, `ExtensionInstallAllowlist`, permits the approved identifiers
and blocks everything else. We copied the policy templates into our central store, listed
the approved IDs, and linked the policy to our workstation OUs.

Four hundred and twelve extensions. A few dozen made the approved list. The rest stopped
being installable.

## The moment we knew it worked

Policies that appear correctly in the policy console are not proof of anything. They have
been seen. So we tested the negative case, deliberately: on a managed endpoint, we tried to
install extensions that were *not* on the allowlist.

Both browsers refused the install, and — this is the detail we care about — they attributed
it to administrative policy rather than throwing a generic error. The block happened at the
point of download, which means the extension code never executed. Not "you can install this
but it will warn you". It never ran.

The detail that made us happiest: we picked well-known, entirely reputable extensions as
test cases. Google Translate. DeepL. A mainstream password manager. All blocked. Because none
of them were approved.

That is the allowlist working exactly as designed, and it is also the bit we would warn any
organisation about, below.

## What nobody warns you about

People noticed immediately, and they were right to.

Within a week we had tickets from people trying to install tools they had used for years,
all blocked, all legitimate. A colleague who had used the same translator daily for four
years suddenly couldn't. Nobody was being paranoid. The control was working, and it felt
exactly like an outage.

If you deploy this, you need three things before the policy goes live, not after:

1. A **known route** for people to request an extension, with a stated business justification.
2. A **response-time commitment**. Without one, teams route around you instead of through
   you, and you will not see it in your compliance reporting.
3. **Change control** on the list itself, so adding an extension is a recorded decision
   rather than a favour.

A policy without those is a helpdesk queue with extra steps.

## What we'd do differently

A few things, now that we've lived with this.

**Re-audit sooner than feels necessary.** Quarterly is the number we'd recommend, and it
feels too frequent for about two quarters. Extension risk decays quietly — publishers get
acquired, legitimate projects get abandoned and resold. An allowlist ages the same way, and
nothing announces that it has gone stale.

**Prune aggressively.** Allowlists only ever grow unless you make them shrink. Ours did. We
ended up maintaining entries nobody could explain, which is worse than useless: nobody can
evaluate the next request against a list nobody understands.

**Say what it doesn't do.** The control covers managed workstations. It says nothing about
BYOD, unmanaged devices, or the extensions a user installs in a profile that never syncs.
Being explicit about that boundary early prevents the moment somebody discovers a gap you
never claimed to cover.

**Separate restricting from mandating.** We wanted users to *have* certain approved tools,
not just be blocked from others. Those are two different policy settings with different
change-management consequences, and we initially conflated them. Don't.

## The part we keep coming back to

None of the technology here was difficult. There was no novel attack to defend against, no
product to evaluate, no budget to find. The Group Policy setting was sitting there, fully
supported, the entire time.

What took the effort was the unglamorous middle: deciding what was actually approved, agreeing
who could approve it, and building a process good enough that people used it instead of
resenting it. Most of that was arguing with each other about where the line should sit, which
is what you would expect from two people who did not fully agree at the start.

Four hundred and twelve extensions were installed in our environment before anyone asked.
If you work somewhere that hasn't asked, the number you get will probably surprise you too.

---

## Full reference implementation

The complete, sanitised technical reference — discovery method, enrichment schema, ADMX
deployment procedure, validation steps, and operational process — is published here:

**[odigiedavididemudia.github.io/browser-extension-control](https://odigiedavididemudia.github.io/browser-extension-control/)**

It contains no environment-specific identifiers, detection queries, policy paths, or
organisation details, and is free to reuse.

---

## POST-PUBLISH CHECKLIST

- [ ] Paste body, set title/dek/tags, upload cover image
- [ ] Turn on **Publish to Twitter/LLinkedIn** if you want cross-posting
- [ ] Verify the Pages link renders as a clickable hyperlink (Medium auto-links bare URLs)
- [ ] Note: daily.dev indexes new content passively — you do not submit it manually.
      Expect it to appear in the feed within roughly 24–72h if it's picked up.