# Notices

Broadcasts from this dogma source to every repo that syncs it. dogma announces each
entry once per repo (Ask: run the action / later / ignore). Newest first.
Format: `## YYYY-MM-DD (§id) Title`, optional `Action: /command`, then the text.

## 2026-10-02 (§n002) Inherit permissions from the session folder
Action: /dogma:sync
DOGMA-PERMISSIONS.md now has an "inherit permissions" switch (§r3nx, default on) at the top
of the permissions block. dogma picks the file by the target of the action (git -C / cd),
then the credo pinned project, then the folder the session was started in; settings this
file does not define come from the session folder's file. If your DOGMA-PERMISSIONS.md has
no "inherit permissions" line, run /dogma:sync to add it (a missing line counts as on).

## 2026-10-02 (§n001) Stable setting ids in DOGMA-PERMISSIONS.md
Action: /dogma:sync
Every setting in DOGMA-PERMISSIONS.md now carries a fixed id like (§bww9), so the hooks
keep working when a line is reworded. New settings: clean up merged worktrees
automatically (§36ch), run ALL tests only at release (§8eyz), and subagents may commit on
their own worktree branch (never push or merge). Run /dogma:sync to bring the ids and the
new lines into this repo; files without ids keep working through the old text match.
