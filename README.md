# tearit-install

One-command bootstrap for a **tearit-hq** minimal desktop (taskbar +
login/signup + cursword + clock).

```sh
curl -fsSL https://raw.githubusercontent.com/tearitco/tearit-install/main/install.sh | sh -s -- tearit-hq
```

Then run `tearit-hq` (if `~/.local/bin` is on your `PATH`) or
`sh ~/tearit-hq/start.sh`.

## What it does

1. Downloads the payload (`tearitco/tearit-hq-payload`, tarball via
   `curl`, falling back to `git clone`).
2. Unpacks it to `$HOME/<product>` (override with `PREFIX=`).
3. Compiles everything in place (`bootstrap.sh` — needs `gcc`,
   `pkg-config`, `libx11-dev libxext-dev libxft-dev`).
4. Writes a `<product>` launcher into `~/.local/bin` (override `BINDIR=`).

Nothing is hardcoded to a product name — arg 1 flows through to the
install dir and the launcher command.

### Env knobs

| var | default | meaning |
|---|---|---|
| `PREFIX` | `$HOME/<product>` | install root |
| `BINDIR` | `$HOME/.local/bin` | launcher dir |
| `PAYLOAD_REPO` | `tearitco/tearit-hq-payload` | where the payload lives |
| `PAYLOAD_REF` | `main` | branch / tag / sha |
| `FORCE=1` | — | overwrite a non-empty `PREFIX` |
| `NO_BUILD=1` | — | fetch + place only |
| `NO_LAUNCHER=1` | — | don't touch `PATH` |

## Linux only, for now

Windows/macOS build legs come later (the component build scripts
already carry macOS guards).

## Data & legal

See [`tearit-legal.md`](tearit-legal.md) — how user tracking / personal-data collection should be implemented (phased), what is lawful to collect, the email-validation options, and why there is no automatic phone-home yet. Current builds send nothing except the GitHub payload download.
