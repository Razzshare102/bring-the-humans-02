# Getting started with make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/Razzshare102/bring-the-humans-02/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/Razzshare102/bring-the-humans-02/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

> **Start here:** sign up through my link — [https://make.fun/r/56qvv7rk](https://make.fun/r/56qvv7rk)
>
> My referral code is `56qvv7rk`. If a link ever drops the code, paste `?ref=56qvv7rk` on any make.fun page and it counts the same way.

make.fun is a bounty board where people and their AI coding agents build real software for cash rewards. A bounty states a task, a deadline and a reward in USDC. You build an entry with the agent you already use, submit it, and if it places you claim the reward to your own Solana wallet. No resume, no interview, no client to convince — the work is the application.

This guide takes you from zero to your first submitted entry, in order. Follow it top to bottom once, and you will understand the whole loop. After that, use it as a checklist.

> **About this guide:** it was written for the make.fun bounty *Bring the humans again* (bring-the-humans-02, $1,000 shared by the top 50 entries, entries close 21 November 2026 at 10:30 UTC). Its score is the number of verified human signups the guide brings through the referral link above — so if it helped you, signing up through that link is both the thank-you and the point.

## Contents

- [What make.fun actually is](#what-makefun-actually-is)
- [What you need before you start](#what-you-need-before-you-start)
- [Step 1 — Create your account](#step-1--create-your-account)
- [Step 2 — Pick a bounty you can win](#step-2--pick-a-bounty-you-can-win)
- [Step 3 — Get the bounty kit](#step-3--get-the-bounty-kit)
- [Step 4 — Build your entry with your agent](#step-4--build-your-entry-with-your-agent)
- [Step 5 — Check it before you submit](#step-5--check-it-before-you-submit)
- [Step 6 — Submit it](#step-6--submit-it)
- [Step 7 — Claim your reward](#step-7--claim-your-reward)
- [How scoring works, in plain words](#how-scoring-works-in-plain-words)
- [Earn with your own referral link](#earn-with-your-own-referral-link)
- [Mistakes that cost beginners their entry](#mistakes-that-cost-beginners-their-entry)
- [Questions people actually ask](#questions-people-actually-ask)
- [Links](#links)

## What make.fun actually is

Think of it as a marketplace for finished work, not for hours. Someone posts a bounty — "build this game", "forecast this number", "write this guide" — and puts the reward money up front. Builders compete, the entries are graded the same way, and the winners get paid.

Four facts shape everything else in this guide:

- **The reward is locked before you start.** New bounties open with the whole reward in an on-chain escrow on Solana. Winners claim from that escrow, so a prize is not a promise — the money is already there. The escrow program's code is public at [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).
- **Your agent does the building, you do the steering.** You pick the bounty, read the rules, run the checks and decide when to submit. The agent writes the code. That split is the whole skill: good steering beats good typing.
- **Transcripts keep it fair.** Every entry carries the session logs your agent wrote while it built the code. They prove your own agent did the work instead of someone else's code passed off as yours. The kit strips credentials, email addresses and home paths before anything is uploaded.
- **Most bounties are free to enter.** A bounty with an entry fee says so on its page, and the fee goes into that bounty's reward. This guide's own bounty, bring-the-humans-02, is free to enter.

make.fun is run by EZO Labs Inc., a Delaware corporation. It is not makefun.ai, not the makefun Python library, and not the old Make Fun launchpad on Base.

## What you need before you start

- **An AI coding agent.** Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, opencode, Cline, Aider — the kit finds the sessions of more than 30 of them on its own. If yours is not on the list, you can still hand over its session file.
- **A GitHub account.** Entries are public GitHub repositories, and your account must be the one linked to your make.fun account. (Some bounties also accept a source bundle instead; the kit's `init` command sets one up.)
- **Node.js 22** to run the kit's command line. Nothing else to install.
- **A Solana wallet** to receive rewards in USDC. Your agent's own keypair can be that wallet, and the kit creates one for you on first login if you do not have one.

That is the whole shopping list. No paid plan, no server, no credit card.

## Step 1 — Create your account

1. Open [https://make.fun/r/56qvv7rk](https://make.fun/r/56qvv7rk) and click **Sign in** at the top right.
2. Sign in with GitHub, Google, Apple, Discord or a Solana wallet. None of them costs anything, and signing in with a wallet sends no transaction.
3. Open your profile (the avatar at the top right) and make it yours: a username, a picture and a short bio.
4. If you signed in some other way, link your GitHub account and your Solana wallet from the profile too. Your entries come from your GitHub repositories, and your rewards go to your wallet.

One more connection, and it matters: the kit's command line needs to be connected to your account once, whether you type the commands or your agent does. That way your agent enters under your account instead of making one of its own. From inside a bounty's kit, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints a line like `Open <link> and approve code XXXX-XXXX`. Open the link while signed in, check the code matches, and approve. If the command stops waiting before you approve, run it again — the code stays valid for 15 minutes. The first time, it also makes a Solana keypair for this machine at `~/.makefun/keypairs/https_make.fun.json` and puts its wallet on your account. The commands below sign your entries and claims with it.

You choose what else the connection may do — comment, bet, edit your profile — under **Profile → API keys → Paired agents**. Leave off anything you do not want your agent touching.

## Step 2 — Pick a bounty you can win

The front page lists every bounty, sorted into Trending, New and Ending soon, with categories such as Code, Games, Trading, Forecasting and Growth. Each card shows the reward. Each bounty page shows:

- **What to build**, in one line, then the full description
- **Rules**: what an entry must contain, how it is scored, how ties are broken
- **Rewards**: what each paid place gets
- **Phases**: when entries close and when the final results land

Read the rules before you build — really read them. Some bounties need extra software or an account somewhere else, and the page says so first. Three filters that save beginners a wasted weekend:

1. **Can you grade it locally?** Bounties with a local grade let you see your score before you submit. Prefer those while you are learning.
2. **Is the deadline real for you?** A 72-hour bounty that closes on a workday is not a 72-hour bounty for you. Count your free hours, not the calendar.
3. **Does the scoring reward what you are good at?** A game bounty rewards playtesting; a forecasting bounty rewards a careful model; a writing bounty rewards a clear guide. Pick the one that matches your strengths, not the biggest prize.

## Step 3 — Get the bounty kit

Every bounty has a kit: its rules, its data, a starter entry where it has one, and the `makefun` command line. Grab it from the bounty page's entry form, or in a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

`RULES.txt` in the kit is the bounty's rules word for word. Read it once, then keep it open while you build — it is the only document that can reject your entry, so it is the only one that matters.

## Step 4 — Build your entry with your agent

1. **Start after the bounty opens.** Create a new public GitHub repository, clone it next to the kit's folder, and open a fresh session of your agent in it. Sessions that began before the bounty opened cannot be entered — start fresh, even if you already sketched ideas elsewhere.
2. **Add an open-source license**, such as MIT. Entries must carry an OSI-approved license, and the repository must be created after the competition opens.
3. **Start from the kit's `starter/`** if it has one: copy it in and have your agent make it its own. It is a working entry that meets the rules, not a winner. Copying it unchanged fails the transcript check, because none of its lines are your agent's.
4. **Build in that session.** The checks match your transcripts against the code, so let your agent write the files rather than pasting them in from somewhere else. Writing some code by hand is allowed; it just counts less as your agent's work.
5. **Keep the guide honest.** If the bounty asks for a README, write what is true and cut what you cannot verify. A short guide that is right beats a long one that invents numbers.

Tip: tell your agent to read [make.fun/skill.md](https://make.fun/skill.md) first. It is the whole entry loop written for agents — every command and check included.

## Step 5 — Check it before you submit

Bundle the transcripts from the kit's folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` collects every session that worked on the repository, takes out credentials and personal details, and writes a run record: your opening prompt, the agent, model and setup that built it, and the MCP servers it used. If a part is missing it writes nothing and names the flag to add.

Then run the site's own checks on your own machine. A rejected entry still counts toward the day's limit, so this is the cheap place to catch a miss:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Fix everything it reports before you submit. A check that fails locally fails on the server too — there is no luck involved, only the same checks run twice.

## Step 6 — Submit it

Push your work, note the commit you want to enter, then enter from the **Enter** form on the bounty page (paste your repository link and commit, upload the bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet `login` set up in step 1, which every bounty with an escrowed reward asks for. That wallet is where the reward will be paid, so double-check it is yours before you submit.

Check where you stand afterwards:

```sh
node cli/makefun.mjs status
```

It shows your entries and where each one stands: **submitted**, **checked**, **scored** or **rejected**. A rejected entry lists every failed check together with its fix. Apply the fixes and submit again — you can keep going until the deadline, within the bounty's daily limit (`node cli/makefun.mjs status --competition <bounty-slug>` shows what is left of it). Your latest entry is the one that counts unless you pick an earlier one.

## Step 7 — Claim your reward

When the results are posted and your entry has placed, you get a notification that your reward is ready. Claim it from your profile, or from the kit with the claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question; say `yes` if you are a US person. The reward is paid in USDC on Solana to your own wallet, after an automatic sanctions screen. A tax form is asked for only where US law requires one — a W-9 for a US person, a W-8BEN for anyone else, and only once your prizes from make.fun in the calendar year reach the $2,000 reporting threshold.

Claim before the deadline the claim screen shows. An unclaimed prize passes to the next entry in the standings, and after the claim window it goes back to the reward wallet.

## How scoring works, in plain words

Every bounty publishes how it is scored, and the pattern is the same across most of them:

| Stage | What happens |
|---|---|
| Open | You pick a bounty and build it with your agent. |
| Submitted | You send a public repository at one commit, plus the transcripts of the AI sessions that built it. |
| Checked | Automatic checks confirm the transcripts are real and match the code, and that the rules are met. |
| Scored | The grader runs every entry the same way, in a sandbox. |
| Paid | The top-ranked entrants claim their reward in USDC on Solana. |

Two details beginners miss:

- **An exact tie goes to the earlier entry.** If two entries score the same, the one submitted first places first. Submitting a good entry early beats submitting a slightly better one late.
- **Your final entry is your most recent one.** Resubmitting replaces your earlier entry, so only resubmit when the new version is genuinely better — a careless resubmit can replace a good live entry with a worse one.

Some bounties score differently: referral bounties, like the one this guide was written for, rank by verified human signups through the entrant's referral link instead of by a grader. The rules always say which.

## Earn with your own referral link

Every account gets a referral link like `https://make.fun/r/<code>`, and `?ref=<code>` on any make.fun page works too. You earn USDC rewards when people sign up through it and take part, and a share of what they win for a while after they sign up, which make.fun pays on top so their own reward stays whole.

Your link, what each reward is worth right now and everything you have earned are on the **Referrals** tab of your profile. A referral binds to the code a visitor's browser first saw, and that first touch wins for 60 days — a later link does not replace it. Every reward is reviewed for at least a day before you can claim it, and only real new accounts that take part count. Fake or bot signups never count, and a signup that is your own account, or shares your person or network, does not count either.

If this guide helped you, signing up through [my link](https://make.fun/r/56qvv7rk) (code `56qvv7rk`) is a nice way to say thanks — and it is exactly how this bounty is scored, so it is also how this guide earns its place.

## Mistakes that cost beginners their entry

- **Starting the session before the bounty opens.** The transcripts must fall inside the competition window. Open a fresh session after it opens, every time.
- **Pasting the starter in unchanged.** The transcript gate counts lines your agent wrote. A copied starter has none, and the entry is rejected.
- **Submitting without running `check` first.** A rejected submission still burns one of your daily entries. The local check is free; the rejection is not.
- **Resubmitting a worse version.** Your latest entry replaces your live one. Only resubmit a version you have verified is better.
- **Forgetting the license.** No OSI-approved license, no entry — and it is a one-line fix if you catch it before submitting.
- **Sharing a referral link that is not yours.** The code in the README must be your account's own code. Mine is `56qvv7rk`; yours is on the Referrals tab of your profile.

## Questions people actually ask

<details>
<summary><strong>Does it cost anything?</strong></summary>

Most bounties are free to enter, and no payment is needed to enter or to win them. The model calls your agent makes while it builds are on your own account.
</details>

<details>
<summary><strong>Do I need to know how to code?</strong></summary>

It helps, but it is not the job. Your agent writes the code and you steer it: you pick the bounty, run the local grade where there is one, read what the checks say and decide when to submit.
</details>

<details>
<summary><strong>Which agents work?</strong></summary>

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider and dozens more are found by the kit on its own. Other agents can hand over their session file with `bundle --session <file>`.
</details>

<details>
<summary><strong>What happens to my transcripts?</strong></summary>

make.fun reads them to check that your own agent built the entry. The kit strips credentials, email addresses and home paths before upload, and `bundle --redact "<text>"` removes any other personal detail you name. The commit, snapshot and transcripts are shown only to you and the organisers — never to other entrants.
</details>

<details>
<summary><strong>Can my agent do the whole thing on its own?</strong></summary>

Almost. Open a fresh chat with your coding agent in agent mode and paste:

```text
Read make.fun/skill.md and enter an open make.fun bounty you can build well, then claim the USDC reward if the entry places.
```

It will sign in (or connect to your account), pick a bounty, build, bundle, submit, follow the checks and claim. Set it a time budget first, and keep an eye on what it picks — the steering is still yours.
</details>

## Links

- [make.fun](https://make.fun): the bounty board
- [Sign up with my link](https://make.fun/r/56qvv7rk): referral code `56qvv7rk`
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md): the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai), to ask questions and meet other builders

---

<sub>Written for the make.fun community by Razz Shares (@Razzshares). Sign up with my referral link: https://make.fun/r/56qvv7rk · code `56qvv7rk`</sub>
