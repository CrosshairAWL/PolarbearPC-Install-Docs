# Antigravity Hub and IDE Preffered Settings

My personal choice:

## 1. Default Homepage

**IDE**: Open Settings > Editor Settings then search:
1. `window.restoreWindows` -> **none**.
2. `workbench.startupEditor` -> **welcomePage**.
3. `window.openFoldersInNewWindow` -> **on**.
4. `git.terminalAuthentication` -> **untick it**.

## 2. Privacy

**Hub**: Open Settings, then:
1. General > Permission > This computer -> **Default**
2. General > Permission > Remote -> **Default**
3. Account > General > Enable Telemetry -> **off**
4. **`~/.gemini/config/config.json`** - adjust with (ofc backup it first):
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

## Extension and its Settings

1. **Project Manager** by Allesandro Fragnani to pin workdir. Settings:
    - Open in Current Window If Empty -> **never**.
