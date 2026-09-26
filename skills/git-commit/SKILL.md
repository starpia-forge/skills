---
name: git-commit
description: Review relevant changes in the current repository and create detailed, purpose-focused Conventional Commits in a user-specified language, or the language of existing commit messages when no language is specified. Use when the user asks to commit current changes to Git, such as “Commit the changes” or “Please commit.” Do not use for requests to draft a message without committing, push changes, or create a pull request.
---

# Conventional Commits

Safely select only the changes that belong to the current task and commit them
using a Conventional Commit with a clear purpose in the selected language.

## Usage and Language Selection

Invoke this skill as `$git-commit <commit message language>`. The language is
optional and applies to the commit message, not to the language of these
instructions.

- `$git-commit Korean` or `$git-commit 한국어`: write the message in Korean.
- `$git-commit English`: write the message in English.
- `$git-commit Japanese`: write the message in Japanese.
- `$git-commit`: use the language of existing commit messages.

Before writing the commit message, select its language:

1. Use the language explicitly supplied after `$git-commit` or otherwise
   specified by the user for this commit. Accept language names and recognizable
   language codes; do not restrict the choice to Korean and English. If the
   requested language is unclear, ask the user to clarify.
2. If no language is specified, inspect recent commit messages on the current
   branch with `git log -10 --format=%B`. Infer the language from the natural
   language in subjects and bodies, ignoring Conventional Commits tokens, code
   identifiers, and automatically generated merge or revert boilerplate. Use
   the predominant language among the informative messages; if languages are
   equally represented, use the most recent informative message's language.
3. If there is no commit history or the messages do not provide enough evidence
   to identify a language, ask the user which language to use before committing.
   Do not infer it solely from the conversation language or default to English.

## Commit Procedure

1. Read all `AGENTS.md` instructions that apply to the repository root and the
   current path.
2. Inspect tracked, staged, and untracked changes using `git status --short`,
   `git diff`, and `git diff --cached`. Read untracked file contents when needed.
3. Determine which files belong to the current task based on the conversation
   and the user's request. Do not modify or stage unrelated changes made by the
   user. If the scope cannot be reliably distinguished, ask the user before
   committing.
4. Run lint, tests, builds, or static checks appropriate to the repository
   instructions and the scope of the changes. Unnecessary builds may be skipped
   for documentation-only changes. If a check fails, report the cause and stop
   unless the user explicitly requests a commit despite the failure.
5. Stage changes with `git add -- <paths>`, specifying the paths to commit.
   Do not use commands that cover the entire working tree, such as `git add -A`.
6. Review the final staged changes again using `git diff --cached --check`,
   `git diff --cached --stat`, and `git diff --cached`. Verify that they contain
   no secrets, generated artifacts, or unrelated changes.
7. Write a commit message that follows the rules below, based on the primary
   purpose of the staged diff, and create the commit. Do not amend an existing
   commit without an explicit request from the user.
8. Verify the result using `git status --short` and `git show --stat --oneline -1`.
   Report the commit hash, final message, included changes, checks performed,
   and remaining changes.

If there are no changes to commit, inform the user instead of creating an empty
commit. This skill only creates commits; it does not push, create branches, or
create pull requests.

## Message Rules

Use the following format:

```text
<type>(<optional scope>): <purpose summary in the selected language>

- <Sentence in the selected language explaining the purpose of the change and its main implementation>
- <Sentence in the selected language explaining the affected scope or important behavior changes>
```

- Choose `type` from `feat`, `fix`, `refactor`, `perf`, `test`, `docs`, `build`,
  `ci`, `chore`, or `revert` based on the primary purpose of the commit rather
  than the kinds of files changed.
- `scope` is optional. When used, choose a code identifier with lasting meaning
  in the repository, such as `frontend`, `backend`, or `repo`.
- Write the subject, body, and footer descriptions entirely in the selected
  language, except for standard Conventional Commits tokens and code identifiers.
- Lead the subject with the purpose and outcome of the change rather than a
  list of modifications. Keep it concise and omit the final period.
- Always include a body. Describe the reasons for the change, key implementation
  details, and affected scope concretely, based on the staged diff. Do not
  simply repeat the subject.
- Include only one logical purpose per commit. Leave out changes with separate
  purposes and report them as remaining changes.
- For breaking changes, add `!` after the type or scope and include a
  `BREAKING CHANGE: <description in the selected language>` footer.
- Do not guess unverified information, such as issue numbers, for the footer.

## Example

For `$git-commit English`:

```text
chore(repo): separate frontend and backend workspaces

- Configure npm workspaces to clarify ownership of dependencies and settings for each app
- Add target suffixes to frontend run commands to prevent conflicts with future backend commands
- Create a separate directory for backend server code
```
