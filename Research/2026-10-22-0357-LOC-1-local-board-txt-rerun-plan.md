Rules: /opt/agent-pm/plugins/autopilot/skills/light-build/SKILL.md /opt/agent-pm/plugins/autopilot/references/autopilot-common.md /opt/agent-pm/plugins/autopilot/references/review-round.md
RESUME: phase=done worktree=/Users/dot/.agent-pm/board/.state/work/LOC-1/agent/src/dotpm2026/agentpm-test-LOC-1 branch=LOC-1-local-board-txt base_ref=ff6b9ff7d528d4fc70ddd67736b7e08266feb206 review_round=0 input_sha=af5d65503f4b

## input

Requirement (the user's, newest, this build): add a third line to local-board.txt that says exactly: third run. Keep the other lines.

Context (earlier built requirements): `local-board.txt` exists at the repo root of `dotpm2026/agentpm-test` (first instruction: exactly one line "hello from the local board", built as c6ab3ef; second: a second line "revised once", built as e51c94e). The file currently holds exactly two lines and must end up exactly three:
hello from the local board
revised once
third run
Keep the first two lines and their newlines unchanged; the third line says exactly "third run".

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

`cmp /Users/dot/.agent-pm/board/.state/work/LOC-1/agent/src/dotpm2026/agentpm-test-LOC-1/local-board.txt /Users/dot/.agent-pm/board/.state/work/LOC-1/agent/tmp/expected-local-board-rerun.txt` — exit 0 = pass; expected bytes: `hello from the local board\nrevised once\nthird run\n`.
CI checks: []

## Progress log

- decision: resolver mode=stay; base_ref=ff6b9ff (HEAD at S1; commits c6ab3ef, e51c94e, ff6b9ff are earlier runs' work on this branch).
- decision(publish): publish=none (not requested, no pull_request workflow); PR #9 managed by caller; verification=local.
- S5 task 1 done: a51da54 red=cmp verify exit 1 before edit (EOF after byte 40, line 2); pushed ff6b9ff..a51da54.
- S6 panel: pinned=[correctness,requirement-fidelity,doc,verification] verification=local transport=Workflow->Task
- S6 r1 @a51da54: correctness=PASS requirement-fidelity=PASS doc=PASS verification=PASS (command=cmp local-board.txt /Users/dot/.agent-pm/board/.state/work/LOC-1/agent/tmp/expected-local-board-rerun.txt, exit code=0, tests=unknown, failures=0) -> converged
- residual NON-BLOCKING: none (verification evidence only: verify exit 0 byte-identical, worktree frozen before/after at a51da54, no leaks; no CI manifests so cmp is the full documented verification)
- S7: clean tree, HEAD a51da54 = last all-PASS reviewed_sha; publish=none, no pr.py finish; decision: plan doc copied to Research/ (repo keeps dated design docs there) and committed, then pushed before the result block so autopilot head == PR head (fixes prior run's gate G2).

## Review items

(none)

## Notes

- Repo is a live-test repo: no tests, lint or build; verify via `cmp` above.
- `Research/` keeps dated design/research docs, naming `YYYY-MM-DD-HHMM-<ID>-<slug>.md`; S7 copies the plan doc there and commits it; commit+push that copy before emitting the autopilot-result so the ready gate sees autopilot head == PR head (prior run failed gate G2 by setting head to the reviewed_sha before the copy commit).
- local-board.txt pre-edit: exactly `hello from the local board\nrevised once\n` (40 bytes).

## Task list

### Global Constraints

- Target file: `/Users/dot/.agent-pm/board/.state/work/LOC-1/agent/src/dotpm2026/agentpm-test-LOC-1/local-board.txt`.
- Final bytes exactly: `hello from the local board\nrevised once\nthird run\n`. First two lines and their newlines unchanged.
- No mutation testing; the red step is the verify command failing before the edit.
- Build asks for no PR; caller manages PR #9 onto main. Push only via the exact command in the input, after the S5 commit.

### Task 1: Add third line "third run" to local-board.txt

- Files: `local-board.txt` (modify).
- Consumes / Produces: none crossing tasks.
- Tests to write first: verify command `cmp /Users/dot/.agent-pm/board/.state/work/LOC-1/agent/src/dotpm2026/agentpm-test-LOC-1/local-board.txt /Users/dot/.agent-pm/board/.state/work/LOC-1/agent/tmp/expected-local-board-rerun.txt`; must exit non-zero before the edit (third line missing).
- Checks it runs: the verify command above (red before, green after).
- Commit message: `Add third line "third run" to local-board.txt`
