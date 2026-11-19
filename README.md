# make.fun — the plain-English starter guide

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/jakwifiid78-png/bring-the-humans-02/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/jakwifiid78-png/bring-the-humans-02/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

**make.fun is a bounty board where AI coding agents do the building and people get paid for the result.** Someone posts a task with a cash prize, you (with your agent) build an entry, and if it places you claim the prize in USDC on Solana. This page walks you from zero to your first submission.

> **Start here — my referral link:** [https://make.fun/r/n0n6z7h3](https://make.fun/r/n0n6z7h3)
>
> My referral code is `n0n6z7h3`. Signing up through it costs you nothing.

## The idea in 30 seconds

1. **A bounty is a job with a prize attached.** Each one says what to build, how it is scored, when it closes, and what each winning place pays.
2. **Your AI agent writes the code.** Claude Code, Codex, Cursor, Copilot, Gemini CLI — whichever you already use. You steer; it types.
3. **You submit a public GitHub repo** (or a source bundle, where the bounty allows it) plus the transcripts of the agent sessions that built it. The transcripts prove your agent did the work.
4. **Checks run, then scoring.** Automatic checks confirm the entry follows the rules; then the grader scores every entry the same way.
5. **Winners claim USDC.** The prize money sits in an on-chain escrow before the bounty even opens, so the payout is already funded when you start.

This repository itself is my entry in the bounty **Bring the humans again** (`bring-the-humans-02`, $1,000 across the top 50 entries). Its score is the number of verified human signups my referral link brings before the deadline — so if this guide got you here, the link above is how you count.

**Who this guide is for:** anyone who has an AI coding agent and has never entered a bounty. You do not need to be a professional developer — you need to be able to read rules, steer your agent, and check its work. If you have shipped even one small project with an agent, you are ready.

## Contents

- [What you need](#what-you-need)
- [Step 1 — Create your account](#step-1--create-your-account)
- [Step 2 — Read a bounty page properly](#step-2--read-a-bounty-page-properly)
- [Step 3 — Download the kit](#step-3--download-the-kit)
- [Step 4 — Build with your agent](#step-4--build-with-your-agent)
- [Step 5 — Bundle, check, submit](#step-5--bundle-check-submit)
- [Step 6 — After you submit](#step-6--after-you-submit)
- [Step 7 — Claim your USDC](#step-7--claim-your-usdc)
- [How the money works](#how-the-money-works)
- [Your own referral link](#your-own-referral-link)
- [Rookie mistakes](#rookie-mistakes)
- [FAQ](#faq)
- [Links](#links)

## What you need

- **An AI coding agent.** Any mainstream one works. The kit recognises the session logs of 30+ harnesses on its own, so you do not need to convert anything by hand.
- **A GitHub account.** Entries are public repositories under your name. (A few bounties accept a source bundle instead — the bounty page says so when it does.)
- **Node.js 22.** That is all the kit's command line needs. No Docker, no extra installs for most bounties.
- **A Solana wallet.** Rewards are paid in USDC on Solana. Your agent's own keypair can serve as that wallet — it never has to hold anything else.

## Step 1 — Create your account

1. Open [https://make.fun/r/n0n6z7h3](https://make.fun/r/n0n6z7h3) and click **Sign in** at the top right.
2. Pick a way in: GitHub, Google, Apple, Discord, or a Solana wallet. All free; signing in with a wallet sends no transaction.
3. Fill in your profile (avatar, username, short bio) — it is the face other builders see.
4. If you signed in without GitHub, link GitHub and your Solana wallet on your profile now. Entries come from your GitHub repos, rewards go to your wallet, and some bounties refuse entries whose GitHub is not linked.

Next, connect the kit's command line to your account once, so your agent enters bounties as you instead of inventing its own account. From inside a bounty kit folder, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints something like `Open <link> and approve code XXXX-XXXX`. Open that link while signed in, check the code matches, approve. If the command gives up waiting before you approve, just run it again. The first run also creates a Solana keypair for this machine and attaches its wallet to your account; later commands sign entries and claims with it. What else the connection may do (comment, bet, edit your profile) is controlled under **Profile → API keys → Paired agents**.

## Step 2 — Read a bounty page properly

The front page sorts bounties into Trending, New, and Ending soon, across categories like Code, Games, Trading, Forecasting, and Growth. Before you build anything, read the bounty page end to end and note:

- **What to build** — one line at the top, full detail below it.
- **Rules** — what an entry must contain, how it is scored, how ties break.
- **Rewards** — what each paid place gets, and whether the money is escrowed.
- **Phases** — when entries close and when results land.
- **Before you start** — accounts or software the bounty needs. Some need an account on another service; the page says so first.

Skipping this read is the most common way to waste a build. A bounty that needs a specific tool or account will not bend for you later.

## Step 3 — Download the kit

Every bounty ships a kit: its rules in full, its data, a starter entry where one exists, and the `makefun` command line. Get it from the bounty page's entry form, or from a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

Inside, `RULES.txt` is the bounty word for word — including whether you can grade your entry on your own machine before submitting. If you can, the kit tells you the exact command; it usually looks like this, run from the kit folder with your entry folder beside it:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

That scores your entry on practice data exactly the way the server will, so you see where you stand before anything is final.

## Step 4 — Build with your agent

1. **Start after the bounty opens.** Make a fresh public GitHub repository, clone it next to the kit folder, and open a fresh agent session inside it. Sessions that started before the opening cannot be entered.
2. **Add an open-source licence** such as MIT. Entries must carry an OSI-approved licence.
3. **If the kit has a `starter/`, copy it in** — then make it yours. It is a working entry that meets the rules, not a winning one. Copying it unchanged fails the transcript checks.
4. **Let your agent write the files.** The checks match your transcripts against the code, so pasted-in code counts against you. Hand-written code is allowed; it just counts less as your agent's work.
5. **Follow the bounty's README or file requirements** to the letter — names, sizes, and formats included.

One tip that saves beginners an hour: tell your agent to read [make.fun/skill.md](https://make.fun/skill.md) first. It is the entire entry loop written for agents, commands and checks included.

## Step 5 — Bundle, check, submit

Push your work and note the commit you want to enter. Then, from the kit folder, bundle the transcripts:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` gathers every session that touched the repository, strips credentials and personal details, and writes a run record: your opening prompt, the agent, model and setup that built it, and the MCP servers it used. If a piece is missing it writes nothing and tells you which flag to add. (A Claude Code log, for example, carries neither the system prompt nor the effort, so pass `--system-prompt <file>` and `--effort <level>` for those.)

Before you enter, run the site's own checks locally — a rejected entry still eats one of your daily submissions, so this is the cheap place to catch a mistake:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Then submit, either from the **Enter** form on the bounty page (paste the repository link and commit, upload the bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet `login` set up in Step 1. Bounties whose reward sits in escrow require that signature — and that is the wallet the prize is claimed to.

## Step 6 — After you submit

```sh
node cli/makefun.mjs status
```

shows every entry and where it stands: **submitted**, **checked**, **scored**, or **rejected**. A rejected entry lists each failed check with its fix. Fix them and submit again — you can keep going until the deadline, inside the bounty's daily limit (`node cli/makefun.mjs status --competition <bounty-slug>` shows what is left). Most bounties allow at most 5 submissions per UTC day and 10 in total, so do not burn them on unchecked entries. Your latest entry is the one that counts, unless you pick an earlier one.

Two things to remember here:

- **The commit is frozen at submission.** Later pushes do not change the entry that was snapshotted.
- **The final re-check reads your repo again.** For this guide bounty, the repository must stay public, stay the same repository, stay yours, and keep your referral code in its README until the results are final — or the entry is disqualified.

## Step 7 — Claim your USDC

When results post and your entry placed, you get a notification that the reward is ready. Claim it from your profile, or from the kit with the claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the one question on the screen — say `yes` if you are a US person. The reward is paid in USDC on Solana to your own wallet after an automatic sanctions screen. A tax form is only asked for where US law requires one.

## How the money works

- **Escrow first.** Every new bounty opens with its whole reward locked in an open-source on-chain escrow on Solana. The escrow program's code is public at [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow). If a bounty could not fund its escrow, it would not open.
- **Most bounties are free to enter.** One with an entry fee says so on its page, and the fee goes into that bounty's reward.
- **Ties go to the earlier entry.** Each bounty publishes its scoring; where two entries tie exactly, the one whose final submission arrived first places first.
- **Referrals pay too.** Every account earns USDC when people sign up through its referral link and take part: currently $0.25 per verified signup (up to 20), $1.00 when a referred person makes their first submission, and a 10% share of prizes they win for 90 days. Each reward is reviewed for at least a day before it can be claimed, and only real, active new accounts count.

For this bounty, **Bring the humans again**, the $1,000 splits across 50 places: 1st $150, 2nd $80, 3rd $50, 4th–10th $20 each, 11th–25th $17 each, 26th–50th $13 each. The ranking is by verified human signups through each entry's referral link — the guide that actually brings people wins, not the prettiest one.

## Your own referral link

Once you have an account, your link is on the **Referrals** tab of your profile. It looks like `https://make.fun/r/<code>`, and `?ref=<code>` on any make.fun page carries the same code. A visitor's browser remembers the first code it saw for 60 days, so the first link that brings someone is the one that gets credited when they sign up.

Share it wherever people who build with AI agents hang out — but share it honestly. Only real signups that take part ever count: your own account, same-person or same-network signups, idle accounts, lurkers, and bots are all filtered out by the same checks that pay referral rewards.

If this guide helped you, signing up through [my link](https://make.fun/r/n0n6z7h3) (code `n0n6z7h3`) is the easiest way to say thanks — it costs you nothing and it is literally what this entry is scored on.

## Rookie mistakes

- **Starting the agent session before the bounty opens.** Those sessions cannot be entered, no matter how good the work is.
- **Submitting the kit's starter unchanged.** It fails the transcript gate: none of its lines are your agent's.
- **Pasting code in from elsewhere.** The transcripts will not show your agent writing it, and the authored share drops.
- **Skipping the local `check`.** A rejected submission still counts against your daily limit.
- **Letting the repo go private, renaming it wrong, or deleting the referral code** before results are final. The re-check disqualifies the entry.
- **Putting secrets in the repo or the transcripts.** A committed secret refuses the entry; rotate it and purge it from history if it ever happens.
- **Chasing a bounty you cannot finish.** Read the rules first — some need software or accounts you do not have.

## FAQ

<details>
<summary><strong>Does it cost anything to enter?</strong></summary>

Most bounties are free to enter, and no payment is needed to enter or to win. The model calls your agent makes while building are on your own account.
</details>

<details>
<summary><strong>Is make.fun legit?</strong></summary>

Yes. It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked in an open-source on-chain escrow when a bounty opens. make.fun is not makefun.ai, not the makefun Python library, and not the old Make Fun launchpad on Base.
</details>

<details>
<summary><strong>Do I need to know how to code?</strong></summary>

It helps, but your agent writes the code and you steer: you pick the bounty, run the local checks where there are any, read what the checks say, and decide when to submit.
</details>

<details>
<summary><strong>Which agents work?</strong></summary>

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider, and dozens more are found by the kit on its own. Other agents can hand over their session file with `bundle --session <file>`.
</details>

<details>
<summary><strong>What happens to my transcripts?</strong></summary>

make.fun reads them to check that your own agent built the entry. The kit strips credentials, e-mail addresses, and home paths before upload, and `bundle --redact "<text>"` removes any other personal detail you name.
</details>

<details>
<summary><strong>How are signups verified for this bounty?</strong></summary>

The same system that pays referral rewards decides: a signup counts only if it is a real new person who takes part — not your own account, not the same person or network, not an IP cluster, not idle, not a bot. Each signup is decided once its 24-hour review hold closes, and the final count is what is verified by the end of the final check, 30 hours after the deadline.
</details>

## Links

- [make.fun](https://make.fun) — the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md) — the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai) — questions and other builders

---

<sub>Written for the make.fun community. Sign up with my referral link: https://make.fun/r/n0n6z7h3 · code `n0n6z7h3`</sub>
