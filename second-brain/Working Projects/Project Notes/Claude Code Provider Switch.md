---
tags: [project, claude-code, powershell, grok, deepseek, kimi, qwen]
---

# Claude Code Provider Switch

Switch Claude Code (terminal CLI + VS Code extension) between Kimi, Qwen, Grok, and DeepSeek by copying a canonical profile onto `%USERPROFILE%\.claude\settings.json`.

`settings.json` is a **generated copy**. Edit `settings-<profile>.json` (or `settings-kimi-backup.json` for Kimi), then run a launcher. The next switch overwrites live `settings.json`.

**Never put API keys in this note, in git, or in chat.** Keys stay only in the local profile JSON files.

## Launchers

| Script | Canonical profile | Gateway |
|---|---|---|
| `C:\Users\User\.claude\claude-kimi.ps1` | `settings-kimi-backup.json` | Kimi (`https://api.kimi.com/coding/`) |
| `C:\Users\User\.claude\claude-qwen.ps1` | `settings-qwen.json` | Qwen |
| `C:\Users\User\.claude\claude-grok.ps1` | `settings-grok.json` | xAI (`https://api.x.ai`, model `grok-4.7`) |
| `C:\Users\User\.claude\claude-deepseek.ps1` | `settings-deepseek.json` | DeepSeek (`https://api.deepseek.com/anthropic`) |
| `C:\Users\User\.claude\claude-switch.ps1` | all of the above | `-Name kimi\|qwen\|grok\|deepseek` |

## Usage

```powershell
cd $env:USERPROFILE\.claude
.\claude-switch.ps1 -List
.\claude-kimi.ps1
.\claude-qwen.ps1
.\claude-grok.ps1
.\claude-deepseek.ps1
.\claude-switch.ps1 -Name grok
```

Add `-Launch` to start `claude` after switching. Then open a **new** Claude Code session, or VS Code **Developer: Reload Window**.

## Rules the launchers enforce

- Profile JSON must be UTF-8 (not UTF-16). Claude Code silently ignores UTF-16 settings.
- Copy is verified by SHA-256.
- Live `autoCompactEnabled` is forced **on**.
- Placeholder keys (`PASTE…`, `REPLACE…`, `YOUR_…`) are refused. `settings-deepseek.json` still needs a real DeepSeek key before that profile will switch.
- Scripts print gateway / model / key **length** only — never the key.

## Grok status (2026-11-10)

Direct Claude Code → xAI Anthropic `/v1/messages` is **deprecated** on xAI. A simple Messages curl can succeed while Claude Code 2.1.317 still returns:

`API Error: 400 {"code":"invalid-argument","error":"Invalid request content: Invalid message role."}`

Likely cause: Claude Code sends mid-conversation `role: "system"` for unrecognized model IDs such as `grok-4.7`. Changing env vars is **not** a proven fix for that 400. Keep DeepSeek/Qwen/Kimi for Claude Code’s tool loop if Grok still 400s; Grok 4.6 already works in another app.

Proposed (unapplied) Grok settings review file: `C:\Users\User\Desktop\claude-code-grok-proposed-settings.json` (placeholder key only).

## Related

- [[Skill: Qwen Assistant (HTML)]]
- [[How I Like to Work (Claude Code)]]
- [[Personal Skills Repository]]
