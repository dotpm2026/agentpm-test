Rules: /opt/agent-pm/plugins/autopilot/skills/light-build/SKILL.md /opt/agent-pm/plugins/autopilot/references/autopilot-common.md /opt/agent-pm/plugins/autopilot/references/review-round.md
RESUME: phase=done worktree=/Users/dot/.agent-pm/board/.state/work/LOC-1/agent/src/dotpm2026/agentpm-test-LOC-1 branch=LOC-1-local-board-txt base_ref=c6ab3ef7a81ce13646aef99eb1ef54444470133b review_round=1 input_sha=bcf348261889

## input

Revise: add a second line to local-board.txt that says exactly: revised once. Keep the first line as it is.

Context: `local-board.txt` already exists at the repo root of `dotpm2026/agentpm-test` with exactly one line "hello from the local board" (previous build, commit c6ab3ef; draft PR #9 open onto main). Keep that first line and its trailing newline as they are; the file must end up exactly two lines:
hello from the local board
revised once

Conventions and git rules:
- Write code, docs and commits in the target repo's conventions (no CLAUDE.md/AGENTS.md in this repo).
- No mutation testing, whatever a reviewer asks: never modify the source to see what happens; no mutmut etc.; never put a known-wrong value into shipped code to force a branch. A test's red step is its failure before its code exists. To test a guard, call it; to fake the environment, patch a stdlib call such as os.listdir, leaving the code under test unmodified. Every brief to a producer or reviewer sub-agent carries this rule.
- The default branch is main. Never merge into or otherwise touch any other branch.

The plan doc stays where autopilot puts it; S7 copies it to where the repo keeps design docs; never `git add -f` it.

Work only in `/Users/dot/.agent-pm/board/.state/work/LOC-1/agent/src/dotpm2026/agentpm-test-LOC-1` on branch `LOC-1-local-board-txt`, with absolute paths; create no other clone, worktree or branch.
Commits merged from `origin/main` are not this build's work.
Your and your producers' local checks, in every phase: only lint and the unit tests of the projects you changed; never integration tests or full suites: the verification reviewer runs them, on the PR's CI when the repo has a `pull_request` workflow, else locally.
Ask for no pull request: the caller opens it, onto `main`.
After S5 and each fix, run exactly `git -C /Users/dot/.agent-pm/board/.state/work/LOC-1/agent/src/dotpm2026/agentpm-test-LOC-1 push -u origin LOC-1-local-board-txt`.

## Verify command

`cmp /Users/dot/.agent-pm/board/.state/work/LOC-1/agent/src/dotpm2026/agentpm-test-LOC-1/local-board.txt /Users/dot/.agent-pm/board/.state/work/LOC-1/agent/tmp/expected-local-board.txt` — exit 0 = pass; expected bytes: `hello from the local board\nrevised once\n`.

## Progress log

- decision: resolver mode=stay; publish=none (not requested, no pull_request workflow); PR #9 managed by caller; verification=local.
- S5 task 1 done: e51c94e red=cmp verify exit 1 before edit (byte 27, line 1)
- S6 panel: pinned=[correctness,requirement-fidelity,doc,verification] verification=local transport=Workflow->Task
- S6 r1 @e51c94e: correctness=PASS requirement-fidelity=PASS doc=PASS verification=PASS (command=cmp local-board.txt /Users/dot/.agent-pm/board/.state/work/LOC-1/agent/tmp/expected-local-board.txt, exit code=0, tests=unknown, failures=0) -> converged
- residual NON-BLOCKING: none (verification evidence only: verify exit 0, worktree frozen before/after, no leaks)
- S7: clean tree, HEAD e51c94e = last all-PASS reviewed_sha; publish=none, no pr.py finish; decision: plan doc copied to Research/ (repo keeps dated design docs there, committed convention per LOC-3 doc) and committed.

## Review items

(none yet)

## Notes

- Repo is a live-test repo: no tests, lint or build; verify via `cmp` above.
- `Research/` keeps dated design/research docs, naming `YYYY-MM-DD-HHMM-<ID>-<slug>.md`; S7 copies the plan doc there.
- local-board.txt pre-edit: exactly `hello from the local board\n` (27 bytes).

## Task list

### Global Constraints

- Target file: `/Users/dot/.agent-pm/board/.state/work/LOC-1/agent/src/dotpm2026/agentpm-test-LOC-1/local-board.txt`.
- Final bytes exactly: `hello from the local board\nrevised once\n`. First line and its trailing newline unchanged.
- No mutation testing; the red step is the verify command failing before the edit.
- Build asks for no PR; caller manages PR #9 onto main. Push only via the exact command in the input, after the S5 commit.

### Task 1: Add revision line to local-board.txt

- Files: `local-board.txt` (modify).
- Consumes / Produces: none crossing tasks.
- Tests to write first: verify command `cmp <worktree>/local-board.txt /Users/dot/.agent-pm/board/.state/work/LOC-1/agent/tmp/expected-local-board.txt`; must exit non-zero before the edit (second line missing).
- Checks it runs: the verify command above (red before, green after).
- Commit message: `Add second line "revised once" to local-board.txt`
