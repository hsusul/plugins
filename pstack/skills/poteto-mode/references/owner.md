# Owner

These rules come from the owner of this pstack copy. They beat Autonomy, the Subagents defaults, and every playbook. The owner's own instructions file (`CLAUDE.md`, `AGENTS.md`, `GEMINI.md`) and the active output style beat **Writing the reply** when they conflict.

## Outward actions

- Never push, force-push, open a PR or issue, post a comment, or message anyone without the owner's explicit yes in this session. Autonomy's "Just do it" covers local, reversible work only.
- Before any push, print `git remote -v` and name which remote is the owner's `hsusul/*` fork and which is upstream. Some clones have `origin` as the fork, others as upstream.
- No AI attribution in commits, PR bodies, or issues. Drop any `Co-Authored-By` trailer and any generated-with footer. Disclose AI assistance only where the project's contribution policy asks for it.

## Work in someone else's repo

Run these before choosing a candidate, in order.

1. **Policy gate.** Read the repo's `CONTRIBUTING`, `AGENTS.md`, PR template, and AI policy, and the owner's memory notes for that repo. When outside or agent-authored PRs are closed, the deliverable is a detailed issue with a minimal repro, or nothing. Stop and say so before writing code.
2. **Claim and overlap.** Search open PRs and issues for the same bug. In a clone under `/Volumes/990 Pro/OpenSource`, run `contrib status`, then `contrib overlap <paths>`, then `contrib new <slug>`. Popular repos claim bugs within hours.
3. **Reachability.** A fix needs a caller chain from a real entry point (UI, IPC, CLI, public API) and a repro that fails on upstream main. Maintainers close guards against inputs that cannot reach the code. Quote the caller grep beside the claim.
4. **Volume.** Keep only a few PRs open per repo. Answer maintainer asks before opening more. Tick "Allow edits by maintainers".

## Verification

- Run only the tests, lint, and type checks the project documents. Prefer targeted tests over a full suite that takes over the desktop, such as browser suites that launch Chrome. Report what ran and what did not.
- When the project ships its own verification or perf skill, use it in place of a generic one. For BeeClean perf, that is `beeclean-perf-probe`.

## Environment

- Repos live on the external `/Volumes/990 Pro` drive, which sometimes unmounts. Make WIP commits often, not only before heavy builds. Keep builds on that drive. After an unmount, wait for the remount and retry there.
