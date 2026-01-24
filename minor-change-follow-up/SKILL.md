---
name: minor-change-follow-up
description: Follow up on small human-made code changes (renames, loop/condition adjustments, small logic tweaks) by propagating updates to dependent code, tests, and docs without altering the original change; use when a user asks to follow up or update after their changes.
---

# Minor Change Follow Up

## Overview

Incorporate a small upstream adjustment by updating surrounding code, tests, and docs while keeping the user's edits intact and ensuring build, tests, and lint pass.

## Workflow

1. Confirm the change intent
- Read recent edits and summarize intent in one sentence.
- Ask a clarifying question if intent or scope is ambiguous.

2. Preserve the user's edits
- Treat user changes as authoritative; do not revert or rewrite them.
- Only add or adjust dependent code around them.

3. Propagate the change
- Update all references (names, call sites, configs, docs) to match.
- Adjust related logic, conditions, or loops for consistency.

4. Validate correctness
- Ensure code compiles and logic is complete.
- Update unit tests and any expected outputs.

5. Quality gates
- Run or suggest `cargo fmt --all --check` and `cargo clippy --all-targets --all-features -- -D warnings` when appropriate.
- Run or suggest `cargo test` (or targeted tests) and fix failures.
- If tests or lint are not run, state what remains.

## Checklist

- References updated (code and docs)
- Tests updated and passing
- Build and lint clean
- No unintended changes to user edits

## Example triggers

- "I made some adjustment, please follow up."
- "Follow up my changes."
- "Update the code base following my changes."
