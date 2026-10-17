# 0003: Credentials and identities

Status: Accepted

Date: 2026-10-16

## Decision

- The owner pushes from the host shell over SSH, using one write-enabled deploy key per repo, named `<repo>_deploy` with its own SSH alias, loaded by a timed keychain agent.
- The admin credential stays on the host and never enters a container.
- Remote and cloud agent sessions are to act through the Claude GitHub App, to be installed on selected repos only.
- Automatic fixes on pull requests wait until a required check exists and has been proven with a planted failure.

## Reason

The push credential stays outside the local agent's environment, and the App would give remote sessions a distinct, revocable identity, so no personal token is ever handed out.

Known tradeoff, stated plainly: while the deploy keys are loaded, anything running as the owner, including a local coding agent, can use them. The timeout limits the window but does not remove it; a planned dev container with no agent socket would remove it.

Gaps:

- **Gap:** the Claude GitHub App is not installed yet.
- **Gap:** whether the App's pull requests are attributed to the owner or to the App is unverified.
- **Gap:** the dev container does not exist yet.

## Alternatives rejected

- A personal access token.
- A separate bot account.
- Sharing one deploy key across repos (not possible).

## Revisit trigger

- Keys and keychain: when the dev container exists, retire the keychain bridge.
- App identity: when the first cloud-session pull request shows whether it is attributed to the owner or the App, decide the approval count.
- Whole record: when a second contributor joins.
