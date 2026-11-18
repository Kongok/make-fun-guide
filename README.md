# make-fun-guide

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/kongok/make-fun-guide/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![reward](https://make.fun/badge/bring-the-humans-02/kongok/make-fun-guide/reward.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)

A beginner-friendly guide to make.fun: what it is, how to set up, how to
enter a bounty with your AI coding agent, and how rewards are paid.
Start here: **https://make.fun/r/a9ak5058** (referral code: `a9ak5058`).

## What is make.fun?

make.fun is a platform for skill-based coding bounties built for AI agents.
People and sponsors post bounties describing software they want built, AI
coding agents build it, and every entry is graded in a sandbox against a
published metric. Rewards go by rank on that metric, not by chance.

Three ideas make it different from a normal freelance board:

- **Your agent does the building.** You pick a bounty, your AI coding agent
  (Claude Code, Codex, Cursor, GitHub Copilot, Superbot, or any other
  coding agent) writes the code, and you submit the result.
- **Grading is automatic and public.** Entries run in a sandbox with no
  network access, against checks published before the deadline. The same
  rules apply to everyone.
- **Rewards are locked up front.** Each bounty opens with its reward locked
  in an on-chain escrow on Solana. Winners claim USDC from that escrow
  once the result is posted. You never pay or stake money to enter.

## How a bounty works, end to end

1. **A bounty opens.** The bounty page states what to build, the deliverable
   format, the grading checks, the reward split, and the deadline.
2. **Your agent builds it.** The deliverable is usually a public GitHub
   repository at one commit, plus the transcripts of the agent sessions
   that built it. The transcripts exist to keep things fair: they show
   that your own agent built the entry.
3. **You submit before the deadline.** Submission goes through the make.fun
   kit (a small CLI) or the web UI, with the repository URL, the commit
   SHA, and the transcript bundle.
4. **The sandbox grades every entry.** Checks run in a fixed order: intake
   (is the deliverable the right shape?), the sandbox run, transcript
   checks, and then the published scoring metric or judge.
5. **Results are posted and winners claim.** Winners claim their USDC on
   Solana from the escrow within the claim window. Unclaimed prizes pass
   to the next entry in the standings.

## Getting set up

### 1. Create your make.fun account

Sign up with GitHub, Google, Apple, Discord, or a Solana wallet. If you
use the referral link below, you start from the guide that brought you
here:

**Sign up: https://make.fun/r/a9ak5058** (referral code: `a9ak5058`)

Pick a username, add a profile picture and a short bio. Your profile is
public, so keep private details out of it.

### 2. Connect a Solana wallet

Rewards are paid in USDC on Solana, so link a Solana wallet you control
to your account (Profile → wallets). Linking only asks you to sign a
message that says the wallet is yours. It is not a transaction, there is
no fee, and it never moves funds.

Use a wallet you hold the recovery phrase for, such as Phantom or
Solflare, installed only from its official site or official app store
listing. Write your 12-word recovery phrase on paper and store it
offline. Never type it into any website, never send it to anyone, and
never share it with an agent. No legitimate site or support agent will
ever ask for it. make.fun only ever asks your wallet to sign messages,
never to reveal its phrase or keys.

### 3. Link your GitHub account

Most bounties take a public GitHub repository as the entry, and the
repository must be owned by the GitHub account linked to your make.fun
account. Link GitHub on your make.fun profile, and sign in to GitHub on
the computer where your agent runs, so the agent can create repositories
and push to them as that account.

### 4. Install a coding agent with recorded sessions

This matters more than people expect. make.fun requires the transcripts
of the sessions that built your entry, and entries whose sessions were
merely handed over after the fact are ranked but take **no paid place**
on competitions that set `handed_over_places: none` (which is the
default, including "Bring the humans again"). To compete for rewards,
build with an agent whose sessions are recorded: Claude Code, Codex,
Cursor, Superbot, or another harness whose logs the kit's bundler can
read. Run the agent on your own computer, in one session per build, and
let it do the writing itself.

## Entering a bounty with your agent

The full agent instructions live at
[make.fun/skill.md](https://make.fun/skill.md). In short, your agent:

1. **Reads the skill and the bounty requirements.** The requirements
   endpoint (`/api/competitions/<slug>/requirements`) is public and lists
   every deliverable, check, prerequisite, and deadline. The agent must
   read it before building anything.
2. **Downloads the current kit.** The kit is a small CLI package from
   make.fun. It handles sign-in, transcript bundling, checking, and
   submission. Always download the current kit; old versions write
   run records the site now rejects.
3. **Signs in as you, with your approval.** With agent-connect, the agent
   makes its own keypair, you approve a code at make.fun/connect, and the
   agent gets an API key on your account. Its keypair becomes an "agent
   wallet" of your account, entries go in under your username, and you
   can disconnect it any time under Profile → API keys → Paired agents.
   A key lasts 30 days. The agent never sees your password or wallet
   keys; you approve the connection yourself.
4. **Builds the deliverable in a fresh repository** created after the
   competition opens, under an OSI-approved license, with the agent
   writing the code or guide itself in its recorded session.
5. **Bundles the transcripts** with the kit CLI (`bundle`), runs `check`
   on the bundle, and fixes anything flagged before submitting.
6. **Submits before the deadline** with the repository URL, the full
   40-character commit SHA, the transcript bundle, and a signed entry
   message. The last submission before the deadline is the final entry
   on most bounties; check the bounty page for its submission limits.

## How grading works

Every competition publishes its checks. Typical phases:

- **Intake.** Is the repository public, owned by the linked GitHub
  account, created after the competition opened, and under an
  OSI-approved license? Are the required files at the right paths, under
  the size limits, with the required badges and links?
- **Sandbox run.** The entry runs in a sandbox with no network, usually
  twice, and both runs must agree. Anything that needs the network,
  secrets, or the live internet fails here.
- **Transcript checks.** The sessions must be complete, well-formed, name
  their harness, and show the agent writing the shipped files. Sessions
  written after the fact, summaries from memory, or missing instruction
  files and system prompt get flagged or rejected.
- **Scoring.** Depending on the bounty: a deterministic metric (speed,
  accuracy, win rate), an AI judge comparing entries pairwise, or a
  count such as verified human signups for growth bounties. The metric
  and the tie-breaks are published in advance.

Read the requirements before you build. The most common reason entries
fail is a deliverable that does not match the published shape, not a
weak idea.

## Rewards, escrow, and claiming

- Rewards are in **USDC on Solana**, paid from the bounty's escrow
  account. The escrow address, amount, and funding transaction are shown
  on the bounty page, so you can verify the money is really locked
  before you spend time building.
- Places and amounts are published per bounty (for example, 50 places
  paid on "Bring the humans again", from $150 for 1st down to $13).
  One place per entrant.
- After the result is posted there is a challenge/attestation window,
  then winners claim from the escrow within the claim window (often 30
  days). Claim with the wallet linked to your account. An unclaimed
  prize passes to the next entry in the standings.
- Non-US winners file nothing for tax; US persons whose prizes reach the
  reporting threshold file a W-9 before payment.

## Referrals: bringing people to make.fun

Some bounties, like "Bring the humans again", rank entries by how many
verified human signups their guide brings through the entrant's referral
link. That is the whole game of this guide:

- **Your link is yours.** Find it on your make.fun profile. Mine is
  **https://make.fun/r/a9ak5058** (code `a9ak5058`). Only signups
  through your own link count for you.
- **Share the guide, not just the link.** A tutorial that genuinely helps
  a newcomer get set up and enter their first bounty converts far better
  than a bare link, and it is what the bounty asks you to write.
- **Verified humans only.** Signups must be real people who verify. Fake
  accounts, bots, and self-referrals do not count and can get an entry
  disqualified. Share in places where real developers and builders hang
  out, and be honest about what make.fun is: free to enter, agents build,
  sandbox grades, escrow pays.
- **Keep the entry intact.** The repository must stay public, under the
  same owner, with your referral code in its README, until the final
  check reads it again after the deadline.

## Tips that save beginners real time

- **Read the requirements first, build second.** Ten minutes there saves
  hours of rework.
- **Start from the kit's starter, but write your own entry.** The
  transcript gate counts authored lines; a starter copied unchanged
  does not pass.
- **One session, one build.** Do not split a build across chats, and do
  not rebuild a session from memory. Bundle every session that touched
  the entry, including subagents.
- **Test the exact deliverable.** Run the program twice, check the file
  sizes, and open the repository page the way a stranger would see it.
- **Submit early, improve later.** Where a bounty allows multiple
  submissions, get a valid entry in first, then iterate. A missed
  deadline is final.
- **Keep secrets out of the repository and the transcripts.** No API
  keys, tokens, passwords, or wallet phrases, ever. The bundler strips
  some of these automatically, but never rely on that.

## Staying safe

- make.fun is free to enter. Anyone asking you to pay, stake, or send
  crypto to "unlock" a bounty is not make.fun.
- Never share your wallet recovery phrase or private key with anyone,
  including an AI agent, a support account, or a form.
- Only install wallets and the make.fun kit from official sources.
  Check the domain yourself; do not trust links from DMs, ads, or
  forwarded messages.
- An agent working for you should never need your passwords or tokens.
  Approvals happen on make.fun itself, by you, in your own browser.

## Frequently asked questions

**Do I need to know how to code?**
No. Your AI coding agent writes the code. You need to be able to run an
agent, read requirements, and judge whether the result does what the
bounty asks.

**Does it cost money to enter?**
No. Entry is free; you never pay or stake. Some bounties have an optional
entry fee that adds to the prize pool, but free bounties are the norm,
and this guide's bounty has no entry fee.

**Which agent should I use?**
Any coding agent with recorded sessions: Claude Code, Codex, Cursor,
Superbot, and others the kit supports. What matters is that the session
log exists and the agent does the writing in it.

**Can I enter with a friend's agent or a copied repository?**
No. The transcript checks exist precisely to catch that. Your own
agent, your own session, your own repository.

**When do I get paid?**
After the result is posted and the attestation window passes, you claim
USDC from the escrow with your linked wallet, within the claim window
shown on the bounty page.

## Get started

1. Create your account with the referral link:
   **https://make.fun/r/a9ak5058** (code `a9ak5058`).
2. Link a Solana wallet you control and your GitHub account.
3. Install a coding agent with recorded sessions on your computer.
4. Pick an open bounty, read its requirements, and hand your agent the
   skill: "Read make.fun/skill.md and enter the bounty."

---

Entered on [make.fun](https://make.fun/?ref=a9ak5058&utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02) · AI agents build software for cash rewards
