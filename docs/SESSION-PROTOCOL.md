# Session protocol

This document records how work in this repository is planned, handed off and automated. Planning happens in a chat with an AI assistant. A repo agent (an AI coding agent working inside the repository) does the implementation, one slice at a time. A slice is the smallest end-to-end change someone can use. The owner is the person who maintains the repository and reviews, pushes and merges every change. Chats are temporary and the repository is permanent, so anything decided must live in the repo.

## Rules

### 1. Decided means in the repo

A decision exists only once it is in the repo, as a decision record, a roadmap line or a GitHub issue ([0008](decisions/0008-github-issues-for-personal-projects.md)). Brainstorming in chat is not a decision. Each stretch of planning ends with a promotion step that moves what is settled into the repo. Only decisions the owner has explicitly confirmed are promoted, and each one uses the same shape: decision, reason, alternatives rejected and revisit trigger. Everything else stays in chat. Decision records live in [docs/decisions/](decisions/README.md) and are edited in place when a decision changes.

### 2. Build handoffs from the repo

A handoff is the summary carried from one chat to the next, so that the new chat has the context of the old one. A handoff should be generated from the repo, with facts measured using git, plus a few lines of stated intent from the owner; today it is written by hand, as the "Write a handoff for a new chat" row of the table below shows. A handoff is only a snapshot; the repo is the source of truth. Handoffs are private, and anything taken from one is scrubbed before it goes into a public repo.

### 3. Start a new chat at merge boundaries and topic changes

Open a fresh chat after a merge and whenever the topic changes. This keeps cost low and keeps each chat's context small and relevant.

### 4. Automate what has been done by hand and written down

When a recurring manual step has been done by hand and written down, automate it. Any automation that checks or enforces something ships with a planted-failure proof: a deliberately broken input that the check must reject.

## Manual steps and automation status

No rule in this document is enforced by tooling yet; each is a convention, and the table lists which steps are manual and what could automate them.

| Step | Done by | Automation status | Candidate automation |
| --- | --- | --- | --- |
| Promote settled decisions into the repo | owner and chat | none | a promotion prompt template |
| Write a handoff for a new chat | owner and chat | none | a script that measures repo state with git and appends the owner's intent lines |
| Write each repo-agent prompt | chat | none | a prompt template that fixes the opening sentence, rules and report format |
| Review the agent's report for unverified claims | owner and chat | none | a report checklist |
| Write the PR title and body | agent | partly: the agent writes it from instructions in each prompt; no template file or agent-rules file yet | a PR template file |
| Create and configure a new repository (ruleset, merge settings, credentials) | owner | none; done by hand once so far | an exported ruleset file plus a script the owner runs from their own shell |
| Review, push and merge | owner: pushes from the host shell over SSH with the repo's deploy key ([0003](decisions/0003-credentials-and-identities.md)); merges by rebase only ([0001](decisions/0001-rebase-only-merges.md)) | none, by design | none: the owner reads every change |

This file is the one home for the session protocol. Other documents link to it instead of repeating it.
