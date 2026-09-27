# Learn with OpenCode — WORK-FIRST + SOCRATIC Toolkit v3

An OpenCode ruleset for **learning while working**. By default the AI is a senior pair programmer (fast, gives code). Learning modes that withhold code (Socratic hints, examiner, teach, review) only activate when you call their slash command.

Works with any stack: Laravel / PHP, JS / TS, React, Vue, Tailwind, Python, Go, SQL, Docker, Git, etc.

## How it works

| You type | Effect |
|---|---|
| (just ask a task / bug / feature) | **WORK MODE** — fast solution + why + trade-offs |
| `/hint ...` | Socratic mentor L0–L6, holds back code step by step |
| `/debug ...` | Evidence-based bug analysis (≥2 hypotheses + how to falsify each) |
| `/R ...` or `/review-design ...` | Examiner: challenges your design before you code |
| `/teach ...` | 1 concept per session + 2–3 exercise questions |
| `/read ...` (paste code) | Dissects unfamiliar code line-by-line |
| `/review-code ...` | 4-tier review (CRITICAL / IMPORTANT / IMPROVEMENT / OPTIONAL) |
| `/learn` | Save 1 insight + 1 mistake at end of session |
| `/retrieve` | Warm-up recall at start of a study session |
| `deadline ...` / `urgent ...` | Instant solution, overrides all other modes |

After changing config/commands, **restart your opencode session** so they reload.

## Repo structure

```text
.opencode/system.md          ← main rules (loaded every session via opencode.json)
.opencode/commands/*.md      ← slash commands (filename = command name)
.opencode/archive/           ← legacy rules history (v1, v2, Indonesian originals — optional)
opencode.json                ← registers system.md as instructions
```

## Requirements

- [OpenCode](https://opencode.ai/docs) installed.
- Node.js / Bun (only needed for `.opencode/package.json` plugin support).

## Usage — pick one

### Option A: Use as a starter template (recommended for learning)

```bash
git clone https://github.com/rifqieali/learn-with-opencode.git my-project
cd my-project
opencode
```

`opencode.json` at the root already points to `.opencode/system.md`. Just run `opencode` from this folder (or any sub-folder without its own `opencode.json`).

### Option B: Add to an existing project

```bash
# 1. copy the toolkit into your project
cp -r /path/to/learn-with-opencode/.opencode /path/to/your-project/.opencode

# 2. register it in your project's opencode.json (MERGE if the file already
# has other content — just add "instructions"):
```

```json
{
  "$schema": "https://opencode.ai/config.json",
  "instructions": [".opencode/system.md"]
}
```

- Projects **outside** this workspace → use `cp` (copy). Don't symlink, it will break.
- Sub-folders **inside** the same workspace that have their own `opencode.json` → you may symlink for a single source of truth:
  `ln -s ../.opencode .opencode` from inside the sub-folder, then add `"instructions": [".opencode/system.md"]` to its `opencode.json`.

### Option C: Install globally (all projects)

Copy `system.md` to your global config and reference it by absolute path in `~/.config/opencode/opencode.json`:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "instructions": ["/home/YOU/.config/opencode/rules-mentor.md"]
}
```

Verify with `opencode debug config`. Don't commit personal rules to team repos — keep team conventions in `AGENTS.md` instead.

## Examples

```text
# normal work — code is given directly
how do I fix N+1 on this Eloquent query?

# guided learning — code is withheld step by step
/hint help me think through this N+1 query

# challenge a design before coding
/R I'm planning a queue-based CSV import, here's my design...

# learn a fundamental
/teach middleware + authorization

# review without auto-rewrite
/review-code <paste your code>

/debug Expected 200 with items, got 500. Log: ...
```

## Customization

- **Language / tone:** edit the `Language` line in `.opencode/system.md`.
- **Learning style:** edit the `USER LEARNING PREFERENCES` section in `.opencode/system.md`. It's just an example — replace it with your own sequence or delete it.
- **Deadline keywords:** edit §7 in `system.md` (`deadline`, `urgent`, ...) to match words you naturally use.
- **Add a command:** create `.opencode/commands/my-command.md` with a `description:` frontmatter block — the filename becomes `/my-command`. Restart the session.

## Scope (important)

- These settings are **project-local**. They apply inside this folder. Sub-folders without their own `opencode.json` inherit them automatically. They don't touch your global config (`~/.config/opencode/`).
- They do **not** apply to Cursor / Claude Code (those only read `AGENTS.md`, which this repo intentionally doesn't include — add one if you need it).
- A sub-folder with its own `opencode.json` overrides the root config. Use the symlink pattern from Option B to share one `.opencode` across both.

## Troubleshooting: command doesn't show up

1. Restart your opencode session first (most common cause).
2. Check whether the folder where you launched opencode has its own `opencode.json` — if yes, it overrides the root config. Use the symlink pattern above.
3. Check `opencode.json` is valid JSON and `instructions` points to a file that exists.

## Archive

`.opencode/archive/` holds older iterations (v1 strict mentor, v2 work-while-learning, early Indonesian originals). You don't need them to use the toolkit — they're kept for history and for forking your own variant.

## Contributing

Issues and PRs welcome. Keep it technology-agnostic, work-first, and concise — if a rule slows down real work without clear learning value, it doesn't belong in the default path.

## License

MIT — see [LICENSE](LICENSE). Replace author name/year with your own when you fork.
