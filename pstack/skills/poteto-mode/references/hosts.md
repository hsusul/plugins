# Hosts

pstack text names Cursor's tools. Read each name as the role it plays, and use your host's tool for that role. Find your host by the subagent tool you have.

| Role | Cursor | Claude Code | Codex | Antigravity |
|------|--------|-------------|-------|-------------|
| Spawn a subagent | `Task` | `Agent` | `spawn_agent`, then `wait_agent` | the host's subagent call |
| Message a running subagent | resume the `Task` | `SendMessage` | `send_input` | the host's subagent call |
| Ask the user | `AskQuestion` | `AskUserQuestion` | `request_user_input` where enabled, else a plain question that ends your turn | a plain question that ends your turn |
| Todolist | the todo tool | the host's task list | `update_plan` | the host's task list |
| Load a skill | the skill catalog | Read `~/.claude/skills/<name>/SKILL.md` | Read `~/.agents/skills/<name>/SKILL.md` | Read `~/.gemini/config/skills/<name>/SKILL.md` |
| Subagent definitions | `~/.cursor/agents/*.md` | `~/.claude/agents/*.md` | `~/.codex/agents/*.toml` | `~/.gemini/config/agents/*.md` |
| Model rule from `/setup-pstack` | `~/.cursor/rules/pstack-models.mdc` | `~/.claude/pstack-models.md` | `~/.codex/pstack-models.md` | `~/.gemini/config/pstack-models.md` |
| Isolated worker | a cloud agent | `Agent` with `isolation: "worktree"` | a `spawn_agent` worker in its own `git worktree` | a worker in its own `git worktree` |

Read a skill's file even when the catalog hides it. pstack skills opt out of implicit invocation, so a missing catalog entry does not mean the skill is absent.

## Models

Model slugs differ per host. Read the role lines from your host's model rule. With no rule, use these defaults.

| Role | Cursor | Claude Code | Codex | Antigravity |
|------|--------|-------------|-------|-------------|
| Judgment, prose, hardest tasks | `claude-opus-5-5-xhigh` | `opus` | the parent model | the parent model |
| Code and swarm workers | `grok-4.7-xhigh-fast` | `sonnet` | the parent model | the parent model |

Only Cursor takes reasoning-level and fast slugs, and only Cursor has a `readonly` flag. On other hosts skip those adjustments, and keep a read-only role read-only by its brief.

## A second model family

`how`, `why`, `arena`, `interrogate`, and `reflect` want reviewers from more than one model family. Inside one host, a second family comes from another host's CLI or MCP tool. Run it in the reviewer's worktree with the same filled prompt.

- Claude Code reaches GPT through the `codex` MCP tool, or `codex exec "<prompt>"` in Bash.
- Codex reaches Claude through `claude -p "<prompt>"` in a shell.
- Any host reaches Gemini through `gemini -p "<prompt>"` once that CLI has auth.

When no second family is reachable, call the panel single-family in the report.

## Cursor-only skills

These ship in Cursor's `cursor-team-kit` plugin or as Cursor built-ins. Elsewhere, use the replacement.

| Cursor | Replacement |
|--------|-------------|
| `/deslop` | `/simplify`, then `/ponytail-review` |
| `create-skill` | `anthropic-skills:skill-creator` on Claude Code, else the **authoring-a-skill** playbook |
| `control-ui` | the host's browser tool, or `playwright-cli` |
| `control-cli` | the host's shell or terminal tool |
| `/loop` | Claude Code's `/loop`, or the Autonomous run playbook's heartbeat |
| built-in babysit | the Babysit playbook, on every host |
