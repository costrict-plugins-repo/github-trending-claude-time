# claude-time

Stop hearing "tonight" at breakfast.

A zero-config Claude Code plugin that injects **live local time + timezone** into every prompt and stamps every Claude response with a visible `[HH:MM AM/PM TZ]` marker.

## Why

Claude's context window has no clock. Without help, the model guesses the time from stale conversation history — leading to "let's deploy tonight" when it's 9 AM, or "what did you do this morning" when it's already 11 PM.

`claude-time` fixes this with a single shell hook. No daemons, no subscriptions, no API keys.

## What it does

Every time you submit a prompt, the plugin runs:

```bash
date '+%A, %Y-%m-%d %I:%M %p %Z'
```

…and injects the result into Claude's context as a `UserPromptSubmit` additional-context block. It also instructs Claude to **prepend `[HH:MM AM/PM TZ]` to every response** so you can see when the model's last words actually landed (useful when long tasks stall).

Example injected context:

```
Current local time is Sunday, 2026-05-03 12:01 PM CDT (UTC 2026-05-03T17:01:06Z).
Use this for any time-of-day language…

Message stamping: BEGIN every response with the marker `[12:01 PM CDT]` on its own first line…
```

## Install

### Via marketplace (recommended)

```
/plugin marketplace add nexusbuildsai/claude-time
/plugin install claude-time@claude-time-marketplace
```

### Manual

Drop the contents of `hooks/hooks.json` into your `~/.claude/settings.json` under the `hooks.UserPromptSubmit` array.

## Requirements

- `jq` (pre-installed on macOS, `apt install jq` on Linux)
- `date` (POSIX, ships with every Unix)

That's it. No Python, Node, Docker, API keys.

## Customization

Edit `hooks/hooks.json` to tweak the format string. Common variants:

- 24-hour clock: change `%I:%M %p` → `%H:%M`
- ISO date only: change `%A, %Y-%m-%d %I:%M %p %Z` → `%Y-%m-%d`
- Add seconds: `%I:%M:%S %p`
- Add weekday number / day of year: see `man date`

## License

MIT

## Roadmap

- [ ] Optional Stop-hook log file (`~/.claude/claude-time.log`) for stall forensics
- [ ] Workday awareness ("you're outside office hours, suggest deferring")
- [ ] Multi-timezone display for distributed teams
- [ ] Deadline countdown injection from a `~/.claude/deadlines.yaml`

---

Built by [nexusbuildsai](https://github.com/nexusbuildsai). More AI/automation tools at [permitbystate.com](https://permitbystate.com).
