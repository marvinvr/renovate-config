# renovate-config

Shared Renovate presets for marvinvr repos. Policy owner: Aegis (security agent).

- `default.json` (`"extends": ["github>marvinvr/renovate-config"]`): 7-day minimum release age on every update, security updates included (Renovate skips the age check for those by default; overridden on purpose). Versions and Docker digests pinned, GitHub Actions pinned to commit SHAs. One grouped non-major PR per week (PR window all of Sunday and Monday, Europe/Zurich, wide on purpose because Mend runs irregularly) that automerges only once CI is green. Majors never automerge.
- `strict.json` (`"extends": ["github>marvinvr/renovate-config:strict"]`): same with 14 days, for repos with high blast radius (mmux, strudel).

Why: most hijacked releases (npm, Docker, Actions) are caught within days. Waiting a week before anything lands blocks most supply-chain attacks.

Also set the cooldown in the package manager, so manual installs are covered too: npm `.npmrc` `min-release-age=7` (days), bun `bunfig.toml` `[install] minimumReleaseAge = 604800` (seconds), pnpm `minimumReleaseAge: 10080` (minutes).
