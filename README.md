<div align="center">
  <a href="README.md">English</a> | <a href="README-ID.md">Bahasa Indonesia</a>
</div>
<br/>

# 🛠️ OpenCode Configuration Files

This repository contains my personal OpenCode configuration files. These settings are optimized for my specific workflow but are designed to be flexible—feel free to use them as a reference or drop them directly into your setup.

## 🚀 How to Use

Follow these steps to apply the configuration:

1. Clone this repository.
2. Copy the files from `.config/opencode/*` to your local OpenCode configuration directory.
3. Run OpenCode.

### Quick Start (Linux/macOS)

```bash
# Copy configuration files
cp -r .config/opencode/* ~/.config/opencode/
```

### Quick Start (Windows)

Configuration path: `C:\Users\$USER$\.config\opencode`

```powershell
# Copy configuration files
Copy-Item -Recurse .config\opencode\* C:\Users\$env:USERNAME\.config\opencode\
```

### Run OpenCode
```bash
opencode
```

## Configuration Directory Structure

![Example Linux Directory Structure](/Screenshoot/config-folder-linux.png)

## 📦 Configuration Files Overview

| File | Description |
|------|-------------|
| [`opencode.json`](/.config/opencode/opencode.json) | Main OpenCode configuration with provider & model definitions |
| [`oh-my-opencode.json`](/.config/opencode/oh-my-opencode.json) | Full Gemini Preset — Agent/Skills orchestration |
| [`oh-my-opencode-best-config.json`](/.config/opencode/oh-my-opencode-best-config.json) | Best Config Preset — Mixed Gemini + Claude orchestration |
| [`antigravity.json`](/.config/opencode/antigravity.json) | Antigravity auth configuration |

## ⚙️ Supported Models (opencode.json)

The `opencode.json` configuration includes the following model definitions:

**Antigravity Models (via Antigravity Auth):**
- **Gemini 3 Pro** — with `low` and `high` thinking level variants
- **Gemini 3 Flash** — with `minimal`, `low`, `medium`, and `high` thinking level variants
- **Claude Sonnet 4.5** — standard mode
- **Claude Sonnet 4.5 Thinking** — with `low` (8K budget) and `max` (32K budget) thinking variants
- **Claude Opus 4.6 Thinking** — with `low` (8K budget) and `max` (32K budget) thinking variants

**Gemini CLI Models (via Google AI Studio / Gemini CLI):**
- Gemini 2.5 Flash
- Gemini 2.5 Pro
- Gemini 3 Flash Preview
- Gemini 3 Pro Preview

## 🎭 Orchestration: oh-my-opencode

I have provided two preset configurations for `oh-my-opencode` Agent/Skills Orchestration. You can swap between them depending on your preferred strategy:

### 1. Full Gemini Preset — [`oh-my-opencode.json`](/.config/opencode/oh-my-opencode.json)

All agents and categories use **Gemini models only** via Antigravity. Optimized for speed and cost-efficiency.

- **Heavy agents** (sisyphus, build, plan, hephaestus, oracle, etc.) → `antigravity-gemini-3-pro` @ `high`
- **Lightweight agents** (sisyphus-junior, librarian, executor, etc.) → `antigravity-gemini-3-flash` @ `medium`–`high`
- **Categories** mapped to appropriate Gemini model tiers

### 2. Best Config Preset — [`oh-my-opencode-best-config.json`](/.config/opencode/oh-my-opencode-best-config.json)

A **mixed strategy** combining Claude Opus 4.6, Claude Sonnet 4.5, and Gemini models for the best quality on each task.

- **Critical agents** (sisyphus, plan, prometheus, security-auditor) → `antigravity-claude-opus-4-6-thinking` @ `max`
- **Implementation agents** (build, hephaestus, metis, reviewer, tester, refactorer) → `antigravity-claude-sonnet-4-5-thinking` @ `max`
- **Exploration/visual agents** (oracle, explore, multimodal-looker, atlas) → `antigravity-gemini-3-pro/flash`
- **Categories** use the strongest model per domain (e.g., `ultrabrain` & `security` → Claude Opus 4.6)

### Usage

Simply copy the content of the desired preset file and replace the content of `oh-my-opencode.json` in your OpenCode config directory.

### 🔧 Key oh-my-opencode Features Configured

Both presets include the following feature settings:

| Feature | Setting | Description |
|---------|---------|-------------|
| `browser_automation_engine` | `playwright` | Browser automation via Playwright |
| `sisyphus_agent` | enabled, planner on | Autonomous agent with planning capability |
| `dynamic_context_pruning` | enabled, detailed | Smart context management with deduplication and error purging |
| `auto_resume` | enabled | Automatically resume interrupted sessions |
| `ralph_loop` | disabled (100 max iter) | Ralph loop control |
| `background_task` | 4 concurrency, 5min timeout | Background task management |
| `notification` | force enabled | Desktop notifications |
| `git_master` | no footer, no co-authored-by | Clean git commit formatting |

## 🔐 Antigravity Auth Config

The [antigravity.json](/.config/opencode/antigravity.json) file represents my personal antigravity auth setup.

| Setting | Value | Description |
|---------|-------|-------------|
| `account_selection_strategy` | `sticky` | Stick with the same account until rate-limited |
| `switch_on_first_rate_limit` | `true` | Automatically switch account on rate limit |
| `max_rate_limit_wait_seconds` | `0` | Don't wait on rate-limited accounts |
| `quota_fallback` | `true` | Fall back to other accounts when quota is exhausted |
| `pid_offset_enabled` | `true` | Use PID offset for account selection |
| `soft_quota_threshold_percent` | `80` | Trigger soft quota warning at 80% usage |
| `quota_refresh_interval_minutes` | `10` | Refresh quota info every 10 minutes |

*   **Reference:** You can use it as a direct reference or modify it.
*   **Customization:** To customize it properly, please refer to the official schema [here](https://raw.githubusercontent.com/NoeFabris/opencode-antigravity-auth/main/assets/antigravity.schema.json).


## 🔐 Antigravity Auth Add Account

To add a new account to your Antigravity configuration, follow these steps:

1.  **Start Login Process**: Run the command `opencode auth login`. Select **Google** as the provider.
    ![Select Provider](/Screenshoot/antigravity-auth-add-account-1.png)

2.  **Select Login Method**: Choose **OAuth with Google (Antigravity)**.
    ![Select Login Method](/Screenshoot/antigravity-auth-add-account-2.png)

3.  **Add New Account**: When prompted to select an account, choose **Add new account**.
    ![Add New Account](/Screenshoot/antigravity-auth-add-account-3.png)

4.  **Complete Authentication**: Follow the instructions to open the link in your browser, authenticate, and paste the redirect URL back into the terminal. Once done, your account will be added.
    ![Success](/Screenshoot/antigravity-auth-add-account-4.png)
