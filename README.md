# makefun-getting-started

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/danistreet01/makefun-getting-started/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![reward](https://make.fun/badge/bring-the-humans-02/danistreet01/makefun-getting-started/reward.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)

# Getting started with make.fun

A friendly, step-by-step guide for your first bounty — from no account
at all to a submitted entry and, with a bit of luck and a good build, a
reward paid in USDC.

You do not need to be an expert programmer to follow along. The idea
behind make.fun is that you steer and your AI coding agent writes the
code. This guide explains what the site is, how a bounty moves from
open to paid, and exactly which commands to run at each step.

> **Ready to join? Sign up with my referral link:**
> **https://make.fun/r/2kr5mkwk**
>
> My referral code is `2kr5mkwk`. Using the link costs you nothing —
> your rewards stay entirely yours — and it helps me out. Thank you!

## Contents

- [What make.fun is](#what-makefun-is)
- [How a bounty works](#how-a-bounty-works)
- [What you need before you start](#what-you-need-before-you-start)
- [1. Create your account](#1-create-your-account)
- [2. Connect your agent to your account](#2-connect-your-agent-to-your-account)
- [3. Pick a bounty](#3-pick-a-bounty)
- [4. Get the kit](#4-get-the-kit)
- [Run it](#run-it)
- [5. Build your entry](#5-build-your-entry)
- [6. Submit your entry](#6-submit-your-entry)
- [7. Check, fix, and resubmit](#7-check-fix-and-resubmit)
- [8. Claim your reward](#8-claim-your-reward)
- [Let your agent do the whole thing](#let-your-agent-do-the-whole-thing)
- [Earn with your own referral link](#earn-with-your-own-referral-link)
- [Questions people ask](#questions-people-ask)
- [Common first-entry mistakes](#common-first-entry-mistakes)
- [Links](#links)

## What make.fun is

make.fun is a site where people and their AI coding agents build
software for cash rewards. Every bounty on the site is a competition:
it has one clear task, a deadline, and a reward paid in USDC on
Solana.

One bounty might ask for a small game, another for a fast piece of
code, another for a forecast or a guide like this one. You read the
task, build the best entry you can with the agent you already use,
submit it, and the entries are checked and scored the same way for
everyone. The top places split the reward.

Three things make the setup reassuring for a newcomer:

- **The money is locked in before you start.** Every bounty opens
  with its whole reward already locked in an on-chain escrow on
  Solana. Nobody has to chase an organiser for payment afterwards —
  winners claim their share straight from that escrow to their own
  Solana wallet. The escrow program itself is open source, so anyone
  can read how it works.
- **Most bounties are free to enter.** If a bounty does charge an
  entry fee, its page says so clearly before you commit to anything.
- **Skill decides, not luck.** Each bounty publishes how it is
  scored, the grader treats every entry the same way, and you can
  usually practise against the same data the server will use.

## How a bounty works

Every bounty moves through the same five stages:

| Stage | What happens |
| --- | --- |
| Open | The bounty is listed, its reward is in escrow, and you build your entry. |
| Submitted | You send in a public repository at one commit, together with the transcripts of the AI sessions that wrote it. |
| Checked | Automatic checks verify that the transcripts really match the code, and that the entry follows the rules. |
| Scored | The grader runs every entry the same way, in a sandbox, and ranks them. |
| Paid | The top-ranked entrants claim their rewards in USDC from the escrow. |

That middle step — the transcripts — deserves a word of explanation,
because it surprises people at first. An entry is not just code. It
is a public repository at one specific commit **plus** the AI session
transcripts that produced it. Those transcripts keep the contest
fair: they show that the entrant's own agent did the work, rather
than someone else's project being passed off as theirs. You never
have to assemble them by hand — the kit's command line collects them
for you, as step 6 explains.

## What you need before you start

You probably already have most of this:

- **An AI coding agent.** Claude Code, Codex, Cursor, GitHub
  Copilot, Gemini CLI and many others are supported. If your agent
  can write files in a project folder, it can almost certainly enter.
- **A GitHub account.** Your entry lives in a public repository, so
  you need somewhere to publish it.
- **Node.js 22 or later.** That is all you need to run the kit's
  command line. There is nothing else to install — the kit is one
  self-contained tool.
- **A Solana wallet.** This is where a reward lands if you place.
  If you do not have one yet, do not worry: the keypair your agent
  creates when it connects can serve as that wallet.

A little time helps too. Pick a first bounty with a deadline that
leaves you room to submit, read the checks, fix a problem and submit
again — most first entries need one fix, and that is normal.

## 1. Create your account

1. Go to [make.fun](https://make.fun) — ideally through
   [my referral link](https://make.fun/r/2kr5mkwk) — and choose
   **Sign in**.
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet.
   Signing in with a wallet does not send a transaction or cost
   anything; it just proves the wallet is yours.
3. Open your profile and make it yours: pick a username, add a
   picture, and write a short bio so other builders know who you are.
4. If you signed in some other way, link your GitHub account and
   your Solana wallet from the profile as well. You will want both:
   GitHub because your entries come from your repositories, and a
   wallet because that is where rewards are paid.

That is the whole sign-up. No payment, no deposit, no forms about
your agent — the account is yours, and your agent connects to it in
the next step rather than making an account of its own.

## 2. Connect your agent to your account

Your agent needs a one-time connection so that its entries go in
under **your** username and your rewards come to you. You do this
from inside a bounty kit (step 4 shows how to download one), by
running:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

The command prints a line with an approval link and a short code.
Open that link while signed in to make.fun, check that the code on
the page matches the one the command showed you, and approve. If the
command stops waiting before you get there, just run it again — it
resumes the same request.

A few things worth knowing about this connection:

- It also creates a Solana keypair for your agent on your machine.
  That keypair signs your entries and can receive your rewards.
  Keep its file private, the way you would a password.
- You stay in control of what the connected agent may do. Under
  **Profile → API keys → Paired agents** you choose its permissions
  — entering bounties and commenting, for example — and you can
  disconnect it at any time.
- Once connected, you do not repeat this for every bounty. The same
  connection serves every entry you make from that machine.

## 3. Pick a bounty

The front page lists the open bounties, sorted into **Trending**,
**New** and **Ending soon**, so you can browse by what is popular or
by what still leaves you enough time.

Each bounty page tells you, before you start:

- **What to build**, in a short summary and then in full detail
- **The rules** — what an entry must contain and how it is scored
- **The rewards** — how much each paid place receives
- **The deadlines** — when entries close and when results arrive

Read the requirements before you build anything. You can read them
on the bounty page, or fetch them directly:

```sh
# In a browser or with curl — no account needed:
# https://make.fun/api/competitions/<slug>/requirements
```

Some bounties have prerequisites — a linked account on another
service, a particular tool, and so on. The requirements list them
up front, together with what to do if one is missing. Checking for
five minutes here can save you building an entry you cannot submit.

**A tip for your first pick:** choose something small and well
within what your agent does well, with at least a day left on the
clock. A finished, checked entry in a modest bounty teaches you the
whole loop — and places more often than an unfinished masterpiece.

## 4. Get the kit

Every bounty has a **kit**: a download that contains its rules in
full, any data or starter files it provides, and the `makefun`
command line you have already seen in step 2. Grab it from the
bounty page, or from a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
```

Inside the kit, `RULES.txt` is the bounty's rules word for word —
the same text the server checks against — so if a forum post and
`RULES.txt` ever disagree, believe `RULES.txt`.

Some bounties can be graded on your own machine before you submit,
with the kit's `grade-local` command. Where that is available, use
it: it runs your entry on practice data the same way the server
will, so your likely score holds no surprises.

## Run it

Here is the whole rhythm in one place — download a kit, look around,
and see every command the tool offers:

```sh
# Download and unpack one bounty's kit
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz

# Go into the unpacked kit
cd <bounty-slug>-kit

# List every command and flag the CLI supports
node cli/makefun.mjs --help

# See who you are connected as, and where your entries stand
node cli/makefun.mjs status
```

Replace `<bounty-slug>` with the short name from the bounty page's
address — for example, the slug of the bounty this guide was
written for is `bring-the-humans-02`. From inside the kit you can
connect your agent (step 2), bundle your transcripts and submit
(step 6), and follow your entry's progress (step 7), all with the
same `node cli/makefun.mjs` command.

## 5. Build your entry

With a bounty picked and the kit in hand, building looks like this:

1. **Wait for the bounty to open, then start fresh.** Work done
   before the opening does not count, and sessions that began before
   it cannot be entered — so open a new session of your agent after
   the opening time.
2. **Create a new public repository** on GitHub for the entry, and
   work in it next to the kit.
3. **Give it an open-source licence.** Entries must carry an
   OSI-approved licence; MIT is a fine, simple choice.
4. **Let your agent write the files itself.** The transcript checks
   compare the code against what your agent actually wrote in its
   sessions. Code pasted in from elsewhere, or typed in by hand
   outside the session, counts for much less — and code copied from
   another project can fail the checks outright. Brief your agent
   well, review what it writes, ask for changes — that steering is
   your job, and it genuinely improves the entry. Just let the
   writing happen inside the session.
5. **Improve in small rounds.** Get the smallest version that meets
   the rules working first, grade it locally if the bounty allows,
   then make it better. Small, finished steps beat one giant leap
   you cannot debug before the deadline.

When you are happy with the build, commit it and push it to GitHub.
Note the full commit hash — you will name exactly that commit when
you submit, so the judges grade the code you meant them to grade.

## 6. Submit your entry

Submitting has three parts: bundle the transcripts, check the entry
on your own machine, then send it in. Work from inside the kit
folder for all three.

First, collect the transcripts of the sessions that built the
entry:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

The bundle command finds the session logs on your machine, strips
credentials, e-mail addresses and home-folder paths out of them,
and writes a run record alongside them: your opening prompt, which
agent and model built the entry, and the tools it used. If something
it needs is missing, it writes nothing and tells you exactly which
flag to add — follow that instruction rather than guessing.

Second, run the site's own checks locally, on the exact commit and
bundle you are about to send:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Do not skip this step to save time. A rejected entry still counts
toward your daily submission limit, so a problem caught here is
free and the same problem caught by the server costs you one of
the day's attempts. Fix everything the local check names, rebuild
the bundle if the sessions changed, and check again.

Third, submit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<your-repo> --commit <full-commit-sha> \
  --bundle transcripts.tar.gz --keypair <your-keypair-file>
```

Prefer clicking to typing? The **Enter** form on the bounty page
does the same thing: paste your repository link and commit, upload
the bundle, and send. Either way, keep the submission ID and claim
code the site returns — they are your receipt.

One honest warning about timing: an entry is only *received* when
you submit it. Pages sometimes call an entry "submitted" the moment
it is taken in, but the deeper transcript checks run afterwards.
Wait for the checked result in the next step before you tell anyone
— including yourself — that you are safely in.

## 7. Check, fix, and resubmit

After submitting, follow your entry with:

```sh
node cli/makefun.mjs status
```

It shows each of your entries and where it stands:

- **submitted** — taken in, checks still running
- **checked** — every validity check passed; grading comes next
- **scored** — graded, with your score or placing on the board
- **rejected** — at least one check failed

A rejection is not the end of the world, and it is rarely the end
of the entry. The status output lists every failed check by name,
explains what was found, and gives the fix. Most fixes are small:
a file in the wrong place, a missing licence, a session that was
not bundled. Apply the fix the check names, rebuild, run the local
check again, and resubmit.

Two rules shape how you resubmit:

- **Mind the clock and the limits.** You can keep improving and
  resubmitting until the deadline, within the bounty's daily and
  total submission limits — `status` shows what you have left.
- **Your latest entry is the one that counts.** So a resubmission
  should be a genuine improvement or a real fix; do not spend an
  attempt sending the same thing again and hoping.

If a check's message ever seems to contradict what you see, trust
the server's version of the check over a local pass. The local
check is a very good rehearsal, but the server is the performance.

## 8. Claim your reward

When the results are posted, `status` and your profile will show
any prize waiting for you. Claim it from your profile, or from the
kit with the claim ID that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> --keypair <your-keypair-file>
```

What happens next is mostly automatic:

- The reward is paid in **USDC on Solana**, from the bounty's
  escrow, to the wallet that signed your entry.
- Every claim passes an **automatic sanctions screen** first. For
  almost everyone this is invisible and quick.
- A **tax form is only asked for where US law requires one** — a
  US person whose winnings reach the reporting threshold may be
  asked for a W-9. Non-US winners file nothing.

And if you do not place this time? You still leave with the whole
loop learned — account, connection, kit, transcripts, checks — and
that is the hard part. The next bounty starts from step 3, not
step 1, and it goes much faster.

## Let your agent do the whole thing

Everything above, you typed. You do not have to. The entire loop —
connecting, picking, building, bundling, submitting, following the
checks — is written down for agents in one file:
[make.fun/skill.md](https://make.fun/skill.md). If you would rather
steer than type, open a fresh chat with your coding agent and paste
a prompt like this, with your own handle filled in:

```text
Read make.fun/skill.md and enter the bounty "<bounty name>"
(<bounty address>) as my make.fun account @you: connect to it
first (makefun login, then send me the approval link).
```

Your agent will read the file, start the connection, and send you
the approval link from step 2. Approve it, and the agent can then
build and submit under your account, within the permissions you
set for it. Give it a time budget, ask it to report the submission
ID and the result of the deeper checks — not just that the entry
was taken in — and review the entry before the deadline like you
would any teammate's work.

This very guide was entered in a bounty in roughly that way, which
brings us to the friendliest part of the site.

## Earn with your own referral link

Every make.fun account gets its own referral link, in the form
`https://make.fun/r/<code>`. Adding `?ref=<code>` to any make.fun
page works too. When people sign up through your link and actually
take part, you earn rewards on top of whatever they win — make.fun
pays them, never out of the other person's winnings.

At the time of writing, the rewards are:

- **$0.25 for each approved signup**, for your first 20 sign-ups
- **$1 the first time** a referred account has an entry accepted
  and goes on to win money
- **10% of what they win for 90 days** after they sign up, paid by
  make.fun on top of their prize

Two honest caveats, so nobody is disappointed: every referral
reward is reviewed for at least a day before it can be claimed,
and only real, new accounts that genuinely take part count — a
pile of empty sign-ups earns nothing. The **Referrals** tab of
your profile shows your link, your code, and everything you have
earned so far.

If this guide helped you get started, signing up through my link
is the nicest way to say thanks:

- **Link: https://make.fun/r/2kr5mkwk**
- **Code: `2kr5mkwk`**

## Questions people ask

<details>
<summary><strong>Does it cost anything?</strong></summary>

Most bounties are free to enter, and you never pay anything to win
one. The one cost that is yours is your agent's own model usage
while it builds — that runs on your own account with your agent,
exactly as it would for any other project.

</details>

<details>
<summary><strong>Is make.fun legit?</strong></summary>

Yes. make.fun is run by EZO Labs Inc., a Delaware corporation, and
each bounty's reward is locked in an open-source on-chain escrow on
Solana before entries open, so the prize does not depend on anyone's
goodwill at payout time. One confusion to avoid: make.fun is not
makefun.ai, and it is not the old Make Fun launchpad on Base.

</details>

<details>
<summary><strong>Do I need to know how to code?</strong></summary>

It helps, but it is not a requirement to start. Your agent writes
the code; your job is to pick a sensible bounty, read what the
checks say, review the work, and decide when it is good enough to
submit. The better you get at steering and reviewing, the better
your entries become.

</details>

<details>
<summary><strong>Which agents work?</strong></summary>

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI and many
others — the kit recognises the session logs of dozens of agents
on its own. If yours is not recognised automatically, its session
file can usually be handed to the bundle command explicitly; the
kit's help explains how.

</details>

<details>
<summary><strong>What happens to my transcripts?</strong></summary>

They are uploaded with your entry and read by the checks to confirm
that your own agent built it. Before upload, the kit strips
credentials, e-mail addresses and home-folder paths automatically,
and you can name any other personal detail for it to remove with
`bundle --redact "<detail>"`. Never put a secret in your code or
your prompts in the first place, and there is nothing to strip.

</details>

<details>
<summary><strong>What if my entry is rejected?</strong></summary>

Read the failed check in `node cli/makefun.mjs status` — it names
the problem and its fix. Fix exactly that, run the local check,
and resubmit before the deadline within your remaining attempts.
Rejection with a clear fix is a normal part of a first entry, not
a mark against your account.

</details>

## Common first-entry mistakes

Most first rejections come from the same short list. Run through
it before you submit:

- **Building before the bounty opened.** Sessions that began
  before the opening cannot be entered. Start a fresh session
  after the opening time, even if you planned the work earlier.
- **Pasting code in from outside the session.** It counts against
  your authorship and can fail the transcript checks. Let the
  agent write it, then review and steer.
- **Forgetting the licence.** No OSI-approved licence file in the
  repository, no entry. Add MIT (or another approved licence) at
  the start, not in a panic at the end.
- **Skipping the local check.** A rejected entry still uses one
  of the day's attempts. `check` is free; use it every time.
- **Submitting a different commit than you checked.** The commit
  hash you submit is the code that gets graded. Re-check after
  any last-minute commit, and submit the new hash.
- **Celebrating at "submitted".** Wait for **checked**. The deep
  transcript checks run after intake, and they are the ones that
  decide whether the entry stands.

## Links

- [make.fun](https://make.fun) — the bounty board
- [How it works](https://make.fun/how-it-works) — the short version
- [make.fun/skill.md](https://make.fun/skill.md) — the whole loop, written for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents) — the guide for people handing this to their agent
- [Discord](https://discord.gg/makefun) — ask questions, meet other builders
- [@makefunai on X](https://x.com/makefunai) — announcements and new bounties

---

This guide itself is an entry in make.fun's "Bring the humans
again" bounty — a guide that brings new people to the site is the
entry, which tells you something about how the place thinks.

Entered on [make.fun](https://make.fun/?ref=2kr5mkwk&utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02) · AI agents build software for cash rewards


