# Repository Guidelines

## Project Structure & Module Organization
The repository is intentionally lean: `rdp-manager` is the primary Bash application that renders the curses-style menu, orchestrates JSON persistence under `~/.config/rdp-manager/`, and launches FreeRDP sessions. `freerdp-safe` is a companion wrapper responsible for environment hardening before delegating to `xfreerdp3`. Keep new supporting scripts in the root alongside these entry points and document any additional configuration files they create.

## Build, Test, and Development Commands
No compilation step is required; ensure scripts stay executable via `chmod +x rdp-manager freerdp-safe`. Run the manager locally with `./rdp-manager`, which exercises the full interactive flow. Use `shellcheck rdp-manager freerdp-safe` before opening a PR to catch common Bash pitfalls. When touching the wrapper, dry-run with `./freerdp-safe /cert-ignore /v:example.com` to confirm argument pass-through.

## Coding Style & Naming Conventions
Scripts target GNU Bash—retain the `#!/bin/bash` shebang and Bash-specific constructs (`[[ ]]`, arrays). Indent with four spaces and keep function names in `snake_case` (`show_main_menu`, `cleanup`). Store constants in ALL_CAPS and prefer double quotes to preserve spacing in user data. Guard file operations with existence checks and favor descriptive prompt text over raw `echo` outputs when expanding the menu.

## Testing Guidelines
Automated tests are absent, so lean on scripted checks and manual validation. Populate `~/.config/rdp-manager/connections.json` with throwaway profiles and iteratively run `./rdp-manager` to verify add/edit/delete flows. Confirm that `freerdp-safe` exits cleanly on Ctrl+C and surfaces non-zero FreeRDP exit codes. Document reproduction steps in the PR when fixing bugs.

## Commit & Pull Request Guidelines
Write commits in the imperative mood with focused scope, e.g., `Add smart fullscreen preset`. Squash fixups locally to keep history linear. Pull requests should explain the change, note any config migrations, and list the commands you used for validation (`shellcheck`, interactive run). Attach screenshots or terminal recordings when UI text changes, and link to any relevant issue tracker entries.

## Security & Configuration Tips
Keep server credentials out of version control and sanitize sample configs. Always launch FreeRDP through `freerdp-safe` so environment safeguards (Wayland compatibility, logging level) remain active. Highlight any new flags or environment variables in the README when adding connection capabilities.
