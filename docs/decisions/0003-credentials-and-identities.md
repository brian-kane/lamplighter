# 0003: Credentials and identities

Status: Accepted

Date: 2026-10-16

## Decision

- The owner pushes from the host shell over SSH, using one write-enabled deploy key per repo, named `<repo>_deploy` with its own SSH alias, loaded by a timed keychain agent.
- The admin credential stays on the host and never enters a container.
- Admin actions on GitHub (rulesets, repository settings) happen in the browser; no GitHub account credential is stored in the personal distro.
- Remote and cloud agent sessions act through the Claude GitHub App. The App installation is limited to selected repositories, and the App can also read public repositories. Separately, the owner's claude.ai account is connected to GitHub, and that connection is what lists repositories for cloud sessions. Commits and pull requests made through it carry the owner's GitHub user, per the Claude Code routines documentation.
- The App has read-only access to repository administration, so it cannot change the ruleset. It has write access to code, pull requests, issues, discussions, checks, actions, workflows and repository hooks, so a change to a workflow is reviewed like any other diff.
- Automatic fixes on pull requests wait until a required check exists and has been proven with a planted failure.

## Reason

There is one key per repo because GitHub allows a deploy key on only one repository. The push credential stays outside the local agent's environment, and the App installation can be revoked at any time, so no personal token is ever handed out.

Known tradeoff, stated plainly: while the deploy keys are loaded, anything running as the owner, including a local coding agent, can use them. The timeout limits the window but does not remove it; a planned dev container with no agent socket would remove it.

- **Gap:** the dev container does not exist yet.

## Alternatives rejected

- A personal access token.
- A separate bot account.

## Revisit trigger

- Keys and keychain: when the dev container exists, retire the keychain bridge.
- Admin credential: when the planned repo-creation script needs one, decide how it avoids leaving a credential where the local agent can reach it.
- App identity: if a cloud-session commit or pull request is attributed to anything other than the owner's user, or the App's permissions change.
- App scope: if a cloud session can reach a private repository where the App is not installed, the installation does not limit access and the Decision above changes.
- Whole record: when a second contributor joins.
