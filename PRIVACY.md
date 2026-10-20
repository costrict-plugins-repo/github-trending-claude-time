# Privacy Policy — claude-time

**Last updated:** 2026-05-03

## Summary

**claude-time collects no data. None. Ever.**

## What this plugin does

`claude-time` is a Claude Code plugin consisting of a single `UserPromptSubmit` shell hook. On every prompt you send to Claude Code, the hook runs locally on your machine and:

1. Reads your local system time via the `date` command.
2. Wraps it in a JSON `additionalContext` blob via `jq`.
3. Returns that blob to Claude Code so the model knows the current time.

That is the entire functionality.

## Data collection

- **No telemetry.** The plugin does not phone home.
- **No network requests.** The hook makes zero outbound connections.
- **No analytics.** No usage tracking, no event logging, no metrics.
- **No user data is read, stored, or transmitted** beyond your local system clock and timezone, which never leave your machine.
- **No cookies, no accounts, no identifiers.**

## Third parties

None. The plugin has zero third-party dependencies beyond standard Unix utilities (`date`, `jq`) that are already on your system.

## Where the timestamp goes

The timestamp string is passed to Claude Code as prompt context. From there it is handled by Anthropic per [Anthropic's Privacy Policy](https://www.anthropic.com/legal/privacy). claude-time itself plays no role in that transmission.

## Source code

The full plugin is ~30 lines of shell. You can audit it yourself: <https://github.com/nexusbuildsai/claude-time>

## Contact

Questions: open an issue at <https://github.com/nexusbuildsai/claude-time/issues>
