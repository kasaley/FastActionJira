# Jira for FastAction

[Русская версия](README.md)

Your Jira issues in the [FastAction](https://github.com/kasaley/fastActionVersions) panel:
a list driven by your own filters, the description and comments right there in the notch,
and a feed of what changed.

![The Jira tab](https://github.com/kasaley/fastActionVersions/raw/main/docs/screenshots/tab-com.fastaction.jira.png)

## What it does

- **Issues by your own filters.** Several filters to switch between; write the JQL by hand,
  build it in the picker, take one of the filters you already saved in Jira, or paste a link
  to a board — the assignees chosen in the board header come along with it.
- **The whole issue in the panel**: the description with Jira markup turned into something
  readable, and the latest comments. From there you can open it in the browser or copy
  its key or link.
- **Notifications** about new issues in each filter and about changes to the issues you
  watch. Pressing a notification opens that issue.
- **A feed of what happened** inside the tab, with read marks.
- **Step-by-step setup**: address, sign-in method, token — each step checked as you go.
  If Jira refuses, the wizard sends you back to the step that caused it.

## Installing

**Settings → Plugins** in FastAction: the plugin is in the catalogue and installs in one
press. By hand: download the archive from [releases](../../releases) and pick it in
**Settings → Plugins → Install plugin…**.

On first run the plugin asks for your Jira address and a token. The token is kept in the
macOS keychain, not in the plugin's files.

## What it asks for, and why

| Permission | Why |
| --- | --- |
| `network` | your Jira address only — the one you typed into the plugin's settings |
| `secrets` | to keep the token in the keychain |
| `clipboard` | to copy an issue key or link |
| `notifications` | to tell you about new issues and changes |
| `openURL` | to open an issue in the browser |

No other address is reachable: the sandbox allows exactly the host written in the manifest,
and what is written there is `$setting:site` — the address from your own settings.

## Development

Python 3 is all you need.

```sh
tools/fastplugin check     # the manifest parses and makes sense
tools/fastplugin stamp     # required after every edit to plugin.js
tools/fastplugin package   # build the archive and print its sha256
tools/fastplugin release   # tag, release, and the entry for the catalogue
```

`stamp` is not optional: the app compares the sha256 of the script with the one recorded in
the manifest and refuses to run the plugin when they disagree. That is what stops a plugin
edited after installation from using the permissions you granted earlier.

How plugins work in general: [the author's guide](https://github.com/kasaley/fastActionPlugins/blob/main/docs/PLUGINS.en.md).
The catalogue that carries the release entries: [fastActionPlugins](https://github.com/kasaley/fastActionPlugins).
