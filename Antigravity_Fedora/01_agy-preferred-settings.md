# Antigravity Hub and IDE Preffered Settings

My personal choice:

## 1. Default Homepage

**IDE**: Open Settings > Editor Settings then search:
1. `window.restoreWindows` -> **none**.
2. `workbench.startupEditor` -> **welcomePage**.
3. `window.openFoldersInNewWindow` -> **on**.
4. `git.terminalAuthentication` -> **untick it**.

## 2. Privacy

Based on location:

### 2.1. Antigravity Hub

Open Settings, then:
1. General > Permission > This computer -> **Default**
2. General > Permission > Remote -> **Default**
3. Account > General > Enable Telemetry -> **off**

### 2.2. Global Config

1. **`~/.gemini/config/config.json`** - adjust with (ofc backup it first):
```JSON
{
  "userSettings": {
    "artifactReviewMode": "ARTIFACT_REVIEW_MODE_ALWAYS",
    "autoExecutionPolicy": "CASCADE_COMMANDS_AUTO_EXECUTION_OFF",
    "browserJsExecutionPolicy": "BROWSER_JS_EXECUTION_POLICY_DISABLED",
    "enableTerminalSandbox": true,
    "globalPermissionGrants": {
      "allow": [],
      "ask": [
        "read_file(*)",
        "write_file(*)",
        "command(*)",
        "read_url(*)",
        "execute_url(*)",
        "mcp(*)"
      ],
      "deny": [
        "read_file(.git)",
        "read_file(.env)",
        "read_file(.env.local)",
        "read_file(.env.production)"
      ]
    },
    "nonWorkspaceFileAccessPolicy": "AGENT_SETTING_POLICY_ASK",
    "permissionPreset": "AGENT_PERMISSION_PRESET_DEFAULT"
  }
}
```

2. Make rule about non-agent git operation on **`~/.gemini/config/rules/git-skill-policy.md`**:
```
---
trigger: model_decision
description: "Apply whenever creating, editing, reviewing, or running any Git-related skill (such as commit messages, HANDOFF.md, changelogs, PR descriptions, release notes, or diff reviews)."
---

# Global Policy for Git-Related Skills

## 1. Environment Constraints
- `.git` and `.env*` files are hard-blocked by global `deny` rules inside the agent sandbox.
- All file reads, file writes, and terminal commands require manual user approval.
- Never attempt to read `.git/` or execute `git` commands (`git status`, `git diff`, `git log`, `git branch`, `git remote`, `git commit`, `git push`) through agent tools.

## 2. Rules When Designing or Editing Any Git-Related Skill
Every Git-related `SKILL.md` you create or modify must enforce these four patterns:

1. **Explicit Tool Ban:** State clearly in the skill that the agent must never run `git` CLI commands or inspect `.git/` metadata.
2. **User-Supplied Input Contract:** Define the exact, minimal command the user should run in their own external terminal and paste into chat if the context is not already provided:
   - *Commit message / diff review:* `git diff --staged` (and optionally `git status -s`)
   - *Handoff / progress summary:* `git status -s && git log -n 5 --oneline`
   - *Changelog / release notes / PR summary:* `git log <base>..HEAD --oneline` (or `git diff <base>...HEAD --stat`)
3. **Zero-Git Fallback:** Include a fallback path so if the user skips pasting Git output, the skill still works using only the current conversation and the specific files the user explicitly names—without probing random files (`README`, `.gitignore`, etc.).
4. **Output-Only Delivery:** The skill must output ready-to-copy text, Markdown, or a suggested `git` command block for the user to run manually in their own terminal. Never instruct the agent to stage, commit, tag, or push changes.

## 3. Privacy Hygiene for Git Skills
- Never ask the user to paste `git remote -v`, `.git/config`, credentials, tokens, or internal server URLs.
- If pasted diff output appears to contain secrets, private keys, or real client identifiers, stop and flag it to the user before continuing.
```

## 3. Extension and its Settings

1. **Project Manager** by Allesandro Fragnani to pin workdir. Settings:
    - Open in Current Window If Empty -> **never**.
