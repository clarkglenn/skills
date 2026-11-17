---
name: agent-commit-push
description: Commit the requested changes using agent-commit, then push the current branch. Use when the user asks to commit and push or explicitly invokes agent-commit-push.
---

# Agent Commit Push

Complete the requested Git commit and push using the existing
[agent-commit skill](../agent-commit/SKILL.md). Read and apply that skill for
reviewing the changes, writing the message, and reporting verification; keep
those instructions in agent-commit rather than duplicating them here. If the
sibling path is unavailable, locate the installed agent-commit skill before
continuing.

Invoking this skill authorizes committing and pushing the current task's
changes, subject to the user's stated scope. A request for message text or a
preview alone does not authorize either operation.

## Commit and push

- Inspect the working tree, index, current branch, and push destination. Commit
  only changes belonging to the requested task; preserve unrelated changes.
- Use agent-commit to prepare and create the commit. If the requested work is
  already committed, reuse that commit instead of creating an empty commit.
- Review the outgoing commits before pushing. If the push would include
  unrelated commits whose publication is not authorized, resolve the scope
  with the user first.
- Use the configured upstream or push destination. For a branch without one,
  use the unambiguous intended remote and set its upstream. Ask only when the
  destination cannot be determined from repository configuration and context.
- Push the current branch normally. Force pushes and history rewrites require
  explicit authorization. If rejected, inspect the reason before retrying;
  stop when resolving it requires a new authorization or external change.
- Verify the push succeeded and report the commit hash and remote branch. If
  it fails, preserve the local commit and state that it has not been pushed.
