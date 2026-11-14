# Agent rules (shared)

These apply in every repo. Repo-specific rules live in each repo's own CLAUDE.md. Each machine's `~/.claude/CLAUDE.md` imports this file and adds only what is specific to that machine.

## Boundaries
- Never merge, and never push `main`. Push your own branch and open a draft PR only where the repo's CLAUDE.md allows it ([0010](../docs/decisions/0010-agents-open-pull-requests.md)); everywhere else, never push.
- Use no credentials beyond the push and `gh` access the repo's CLAUDE.md allows.
- Never run anything against production or shared environments.
- Ask before changing CI, hooks, rulesets, or credential configuration.
- Work on a branch. You may rewrite your own unpushed branch, never main or a pushed branch.
- Stop only processes you started, by PID.

## Where each fact lives
- Issue: why the overall change is needed, and what done means.
- Commit body: why this diff exists. Never restate what the diff shows.
- PR/MR description: how the commits form a reviewable unit, how it was checked, what was not checked, and what the reviewer should focus on. Link to the issue or commit for rationale; do not repeat it.
- One home per fact. Link instead of repeating. Update in place.

## Commits
- Subject: `type(scope): summary`, imperative, under 72 characters. Types: feat, fix, docs, refactor, test, chore, ci, build.
- Body: a blank line, then `-` bullets that say why, or give a non-obvious consequence.
- Don't hard-wrap: each bullet is one line, however long.
- No attribution line (Co-Authored-By, "Generated with") in commits or PR/MR descriptions.
- Group changes by blast radius: docs, tooling and test-only changes together; anything on a production path on its own, so it can be reverted independently.
- If you fix something nearby, say so in the message. Do not bundle it silently.
- Reference an issue only on commits that actually address it.

## PR/MR titles and descriptions
- If the repo has a PR template, follow it exactly.
- Otherwise, for one commit, use its subject and body as they are. For several commits, write a short theme title in the same `type(scope): summary` format, one bullet per commit, and one line on how it was checked.
- Write for the reviewer: make the review fast.
- Flag anything non-obvious as a review comment, not as a permanent section.

## Others' work
- An issue someone else develops: findings go in a comment on it, never an edit to its description. Judge by its developer, not its current assignee: an issue is reassigned to its reviewer during review, so one you hold only as reviewer is still theirs. Offer a branch; don't open a PR/MR for it. If they open one, theirs wins over ours.
- Reviewing a teammate's PR/MR: a claim that the change breaks something is run before it is posted when a run is quick, and otherwise marked "from reading". Replies cite what ran.

## Comments
- Default to none. Comment only a hidden constraint, an invariant, a workaround for a specific external bug, or why a simpler version would be wrong.
- Never reference a task, ticket or PR in a comment.

## Docs
- Mark a gap as a gap. Never claim a check or rule is enforced unless something enforces it.
- Docs, rules, templates and investigation packets name roles, not people. Issue, PR/MR and comment text, and reply drafts, may name and @mention people.

## Checks
- A new check is proven by a planted failure: a deliberately broken input it must reject.

## Reports
- Summary first, then details.
- Keep what you verified (commands and output) separate from claims and from anything untested.
- Every claim marked verified carries its pointer: the command and the output line it rests on, or file:line at a named commit.
- Do only what the prompt or issue asks. If an extra run or check would help, propose it instead of doing it.
