# X Writer — Claude Code Skill

A Claude Code skill that analyzes your X/Twitter writing style from your recent posts and generates draft tweets that sound like you.

## What it does

1. **Fetches your recent posts** (up to 100) via the X API
2. **Builds a style profile** — tone, structure, vocabulary, topics, engagement patterns
3. **Suggests topics** based on what you've been posting about and what gets engagement
4. **Researches fresh content** — searches X for high-traction posts and the web for latest data on your chosen topic
5. **Generates 3 draft posts** in your authentic voice, each with a different angle, complete with verified sources
6. **Iterates with you** — edit, regenerate, adjust tone, switch topics

No auto-posting. Human approval always required.

## Setup

### Prerequisites

- An X API Bearer Token ([get one here](https://developer.x.com/en/portal/dashboard)) — Basic tier ($100/mo) or higher required

### Option A: Claude Code (CLI)

Paste this into Claude Code:

```
Install this skill for me: https://raw.githubusercontent.com/TurboGuo/x-writer-skill/main/x-writer-SKILL.md
```

Claude will download the file and save it to `~/.claude/skills/` for you.

Then configure your credentials:

1. Go to **Customize > Skills > x writer > Edit Inline** (or open `~/.claude/skills/x-writer-SKILL.md` directly)
2. Replace `YOUR_BEARER_TOKEN_HERE` with your X API Bearer Token
3. Replace `YOUR_X_HANDLE_HERE` with your X handle (no @ sign)
4. Save — you're ready to go

### Option B: Claude Desktop / Claude.ai (Web)

1. Copy the entire contents of [`x-writer-SKILL.md`](https://raw.githubusercontent.com/TurboGuo/x-writer-skill/main/x-writer-SKILL.md)
2. Open a new conversation in Claude Desktop or claude.ai
3. Paste it as your first message, then follow up with:
   ```
   Use the skill above. My Bearer Token is already set in the config.
   ```

> **Tip:** On Claude Desktop, you can also save it as a **Project** prompt so you don't need to paste it every time. Go to **Projects > New Project**, paste the skill content into the **Instructions** field, and start conversations from that project.

> **Note:** Claude Desktop and claude.ai do not have filesystem access, so the skill cannot run `curl` commands directly. Claude will instead guide you through the API calls or ask you to paste your recent tweets for style analysis. For the full automated experience (fetch + analyze + draft), use Claude Code.

### After Setup

Just ask Claude to write posts for you. The skill triggers on phrases like "draft tweets", "write posts in my style", "x writer", etc.

## Usage examples

- "Draft some tweets for me"
- "Write posts in my style about AI agents"
- "Generate X content"
- "Ghostwrite tweets"
- "Help me post on X"

## Security Considerations

> **Read this before using the skill.** There are a few risks to be aware of.

| Risk | Description | Mitigation |
|------|-------------|------------|
| **Plaintext API token** | Your X API Bearer Token is stored directly in the skill `.md` file. If you commit/push this file with your real token, it will be exposed publicly. | **Never commit the skill file with your real token.** Add `x-writer-SKILL.md` to `.gitignore` after configuring it. Rotate your token immediately if leaked. |
| **Token in shell history** | The skill runs `curl` commands with your Bearer Token as a flag. These may be logged in `~/.zsh_history` or `~/.bash_history`. | Periodically clear sensitive entries from your shell history, or prefix commands with a space (if `HIST_IGNORE_SPACE` is enabled) to prevent logging. |
| **Temp files are world-readable** | Fetched posts are saved to `/tmp/xwriter_posts.json`. On shared or multi-user systems, other users can read `/tmp/`. | Acceptable on personal machines. On shared systems, consider changing the output path to a user-owned directory with restricted permissions. |
| **Style profile persistence** | The optional Step 7 saves your style profile to a predictable path, which could be read by other local users. | Only save if needed. Use a path inside your home directory with `chmod 600`. |
| **X API rate limits / cost** | The skill calls the X API on every run. Excessive use can hit rate limits (429) or rack up costs on paid tiers. | The skill fetches at most 100 tweets per run. Be mindful of how often you trigger it. |

## How it works under the hood

The skill uses the X API to pull your recent posts, then performs a detailed style analysis covering tone, structure, vocabulary, topic clusters, and engagement patterns. When generating drafts, it matches your exact voice — post length, emoji usage, hashtag habits, language mixing, and more. Each draft includes verified source URLs for any data claims.

## License

MIT
