---
name: agent-commit
description: Write or revise Git commit messages grounded in task context, explaining why, what changed, and verification, with a body targeting at most 500 characters. Use when preparing a commit, amending its message, or drafting commit text.
---

# Agent Commit

Write for a future maintainer who has the commit but not the conversation.
Explain why the change matters first, then what changed and how it was achieved,
and finally how the results were verified.

## Ground the message

Before drafting, collect the task context: the user's original goal, the observed
problem, accepted decisions and constraints, and the verification performed.
Read the relevant conversation, including corrections and changes of scope.
Consult linked issues, PR descriptions, repository documentation, or recent
history when they contain context needed to explain the change.

Inspect the actual changes being committed to confirm the final implementation;
changed files and diff hunks alone do not explain why the work was needed. For
an amend, inspect the existing commit as well. Omit abandoned approaches unless
they explain a remaining tradeoff. Ground the motivation in collected evidence;
if it is missing, recover it from available context rather than inventing it.

## Write fluent, concise prose

- Start with a short, specific, imperative subject describing the outcome.
- Begin the body with why: the concrete problem, motivation, or desired improvement.
- Next describe what changed and how the implementation achieves that purpose.
  Include technical details that explain the result or a meaningful decision;
  skip file inventories and work chronology.
- Finish with how the results were verified and any material verification limits.
- Keep this order even in a short message. Use natural paragraphs rather than
  mechanical `Why:`, `What:`, and `Verification:` labels; paragraph count is flexible.
- Scale detail to the change. Use bullets when several distinct changes need
  them, and honor explicit user requests and established repository conventions.
- Target a body of at most 500 characters, excluding the title and its separating
  blank line. Count spaces and newlines in the body before finalizing, and trim
  repetition to fit. Keep the motivation, key change, verification, and material
  limits within that budget; honor explicit requests for more detail.

## Describe verification honestly

Say which relevant checks were actually performed and what they established:
for example, isolated endpoint tests, full builds with warnings treated as
errors, or browser checks of a particular flow. Include useful results such as
pass counts when known, without dumping routine command output.

Distinguish tests using mocks or service doubles from live integration checks.
Mention material failures, checks that could not be run, and important behavior
that remains unverified. Do not claim that everything works merely because a
build or a narrow test passed. Reuse still-applicable verification from the
session; do not invent results or run unnecessary checks just to fill the message.

## Example

```text
Restore UIAPI documentation in Scalar

Developers lost the UIAPI reference during the Scalar migration.

Restore its development selector and cookie authentication metadata. Extract
OpenAPI setup into helpers, preserve Swagger URLs, and link devdocs.

53 isolated backend tests passed; two live database tests were skipped.
Live Entra sign-in was not tested.
```

Apply these preferences to the requested Git operation. For a message-only
amend, preserve the commit's file contents even if other changes are staged.
