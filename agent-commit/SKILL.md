---
name: agent-commit
description: Write or revise concise, fluent Git commit messages that explain why first, then the changes and approach, then verification. Use when preparing a commit, amending its message, or drafting commit text.
---

# Agent Commit

Write for a future maintainer who has the commit but not the conversation.
Explain why the change matters first, then what changed and how it was achieved,
and finally how the results were verified.

## Ground the message

Read the relevant conversation and the final changes being committed. For an
amend, inspect the existing commit as well. Describe the final implementation;
omit abandoned approaches unless they explain a remaining tradeoff. Derive the
motivation from the user's intent and the evidence rather than inventing one.

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
Replace Swagger with Scalar and reuse backend test hosts

Provide a Scalar API reference while preserving existing bookmarks and bearer
authentication, and reduce repeated backend test setup.

Replace Swashbuckle with Scalar and .NET OpenAPI, redirect Swagger bookmarks,
and keep pasted bearer tokens. Share hosts for read-only tests and use a
builder for isolated scenarios.

All 48 isolated backend tests pass with warnings treated as errors. Browser
checks with test authentication verified redirects and bearer headers; live
Entra sign-in was not tested.
```

Apply these preferences to the requested Git operation. For a message-only
amend, preserve the commit's file contents even if other changes are staged.
