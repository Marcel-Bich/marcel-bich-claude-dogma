# Notices

Broadcasts from this dogma source to every repo that syncs it. dogma announces each
entry once per repo (Ask: run the action / later / ignore). Newest first.
Format: `## YYYY-MM-DD (§id) Title`, optional `Action: /command`, then the text.

## 2026-10-02 (§n001) Stable setting ids in DOGMA-PERMISSIONS.md
Action: /dogma:sync
Every setting in DOGMA-PERMISSIONS.md now carries a fixed id like (§bww9), so the hooks
keep working when a line is reworded. New settings: clean up merged worktrees
automatically (§36ch), run ALL tests only at release (§8eyz), and subagents may commit on
their own worktree branch (never push or merge). Run /dogma:sync to bring the ids and the
new lines into this repo; files without ids keep working through the old text match.
