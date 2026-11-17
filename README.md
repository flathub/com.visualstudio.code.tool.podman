# Podman remote client for Flatpak VS Code

This extension supplies `podman-remote` under `/app/tools/podman/bin` inside
`com.visualstudio.code`. The parent application uses the `stable` branch, so
`runtime-version` must remain `stable`; the extension's `branch` and `sdk`
select its Freedesktop SDK generation.

| Git branch | Extension / SDK version | Maintenance |
| --- | --- | --- |
| `master` | `26.08` | Active |
| `branch/25.08` | `25.08` | Active |
| `branch/24.08` | `24.08` | Historical; no automatic updates |

Freedesktop SDK 24.08 [reached end of life in September 2026](https://freedesktop-sdk.gitlab.io/documentation/wiki/Releases.html).
Its Git branch is retained for reference.

## Source updates

The **Check for updates** workflow runs daily at 00:00 UTC and can be started
manually from Actions. It checks each active Git branch with the external data
checker's `--edit-only` mode, then creates or refreshes one
`automation/podman-<base>` PR per branch. Manual and scheduled runs are serialized.
When adding a supported runtime, update the workflow matrix using an existing
Git branch, and update the table above.

The shared Flathub external data checker is disabled in `flathub.json` because
this repository owns its update workflow. This avoids competing update PRs and
automatic traversal of historical `branch/*` branches.

Review the source tag and pinned commit, and require a successful Flathub test
build before merging a source update. If automatic test builds have been paused
due to inactivity, comment `bot, build` on the PR to request one. Keep feature
changes such as Compose support in separate PRs.
